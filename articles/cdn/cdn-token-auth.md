---
title: "使用權杖驗證保護 Azure CDN 資產 | Microsoft Docs"
description: "了解如何使用權杖驗證來保護對 Azure CDN 資產的存取。"
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: 837018e3-03e6-4f9c-a23e-4b63d5707a64
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/03/2017
ms.author: mezha
ms.openlocfilehash: 700f4c49bbcda1eccbcc7eafc703e625697fa2b4
ms.sourcegitcommit: 38c9176c0c967dd641d3a87d1f9ae53636cf8260
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2017
---
# <a name="securing-azure-content-delivery-network-assets-with-token-authentication"></a>使用權杖驗證來保護 Azure 內容傳遞網路資產

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>概觀

權杖驗證是一種機制，可讓您防止「Azure 內容傳遞網路」(CDN) 將資產提供給未經授權的用戶端。 執行權杖驗證通常是為了防止內容「熱連結」(hotlinking)，在熱連結中，不同的網站 (通常是留言板) 會在未經許可的情況下使用您的資產。 熱連結會影響您的內容傳遞成本。 藉由在 CDN 上啟用權杖驗證，就會由 CDN 邊緣 POP 先驗證要求之後，再由 CDN 傳遞內容。 

## <a name="how-it-works"></a>運作方式

權杖驗證會藉由提出要求需包含權杖值 (其中包含關於要求者的編碼資訊) 的要求，來驗證要求是由受信任的網站所產生。 只有在編碼資訊符合需求時，才會將內容提供給要求者，否則會拒絕要求。 您可以使用下列一或多個參數來設定需求：

- Country (國家/地區)︰允許或拒絕來自以其[國碼/地區碼](https://msdn.microsoft.com/library/mt761717.aspx)指定之國家/地區的要求。
- URL：只允許與指定資產或路徑相符的要求。
- Host (主機)︰允許或拒絕在要求標頭中使用指定主機的要求。
- Referrer (訪客來源)︰允許或拒絕來自指定訪客來源的要求。
- IP address (IP 位址)︰只允許來自特定 IP 位址或 IP 子網路的要求。
- Protocol (通訊協定)︰根據用來要求內容的通訊協定來允許或拒絕要求。
- Expiration time (到期時間)︰指派日期和時段，以確保連結只能在有限的時段內維持有效。

如需詳細資訊，請參閱[設定權杖驗證](#setting-up-token-authentication)中每個參數的詳細設定範例。

產生加密的權杖之後，您需將它以查詢字串的形式，附加在檔案 URL 路徑結尾。 例如： `http://www.domain.com/content.mov?a4fbc3710fd3449a7c99986b`。

## <a name="reference-architecture"></a>參考架構

以下工作流程圖說明 CDN 如何使用權帳驗證來與您的 Web 應用程式搭配運作。

![CDN 權杖驗證工作流程](./media/cdn-token-auth/cdn-token-auth-workflow2.png)

## <a name="token-validation-logic-on-cdn-endpoint"></a>CDN 端點上的權杖驗證邏輯
    
以下流程圖說明當 CDN 端點上已設定權杖驗證時， Azure CDN 如何驗證用戶端要求。

![CDN 權杖驗證邏輯](./media/cdn-token-auth/cdn-token-auth-validation-logic.png)

## <a name="setting-up-token-authentication"></a>設定權杖驗證

1. 從 [Azure 入口網站](https://portal.azure.com)，瀏覽至您的 CDN 設定檔，然後按一下 [管理] 來啟動補充入口網站。

    ![CDN 設定檔 [管理] 按鈕](./media/cdn-rules-engine/cdn-manage-btn.png)

2. 將滑鼠移至 [HTTP 大型] 上，然後按一下飛出視窗上的 [權杖驗證]。 接著，您便可以依下列方式設定加密金鑰和加密參數：

    1. 在 [Primary Key] \(主要金鑰\) 方塊中輸入唯一加密金鑰，並視需要在 [Backup Key] \(備份金鑰\) 方塊中輸入備份金鑰。

        ![CDN 權杖驗證安裝識別碼](./media/cdn-token-auth/cdn-token-auth-setupkey.png)
    
    2. 使用加密工具來設定加密參數。 使用加密工具時，您可以根據到期時間、國家/地區、訪客來源、通訊協定及用戶端 IP (任意組合) 來允許或拒絕要求。 

        ![CDN 加密工具](./media/cdn-token-auth/cdn-token-auth-encrypttool.png)

       請在 [Encrypt Tool] \(加密工具\) 區域中，為下列一或多個加密參數輸入值：  

       - **ec_expire**：會為權杖指派一個到期時間，在此時間之後，權杖就會過期。 在到期時間之後提交的要求都會遭到拒絕。 這個參數使用 Unix 時間戳記，是以自標準 Epoch `1/1/1970 00:00:00 GMT` 算起的秒數為依據。 (您可以使用線上工具在標準時間與 Unix 時間之間轉換)。例如，如果您想要讓權杖在 `12/31/2016 12:00:00 GMT` 到期，請使用 Unix 時間戳記值 `1483185600`，如下所示。 
    
         ![CDN ec_expire 範例](./media/cdn-token-auth/cdn-token-auth-expire2.png)
    
       - **ec_url_allow**：可讓您為特定資產或路徑量身打造權杖。 若要求的 URL 是以特定的相對路徑開頭，它會限制對該要求的存取。 URL 會區分大小寫。 請利用以逗號分隔每個路徑的方式來輸入多個路徑。 您可以視需求而定，設定不同的值來提供不同層級的存取。 
        
         例如，就 URL `http://www.mydomain.com/pictures/city/strasbourg.png` 而言，會針對下列輸入值允許下列要求：

         - 輸入值 `/`：允許所有要求。
         - 輸入值 `/pictures`：允許下列要求：
            - `http://www.mydomain.com/pictures.png`
            - `http://www.mydomain.com/pictures/city/strasbourg.png`
            - `http://www.mydomain.com/picturesnew/city/strasbourgh.png`
         - 輸入值 `/pictures/`：只允許包含 `/pictures/` 路徑的要求。 例如： `http://www.mydomain.com/pictures/city/strasbourg.png`。
         - 輸入值 `/pictures/city/strasbourg.png`：只允許此特定路徑和資產的要求。
    
       - **ec_country_allow**：只允許來自一或多個指定國家/地區的要求。 來自其他所有國家/地區的要求將會遭到拒絕。 請使用國碼/地區碼，並以逗號分隔每個國家/地區。 例如，如果您只想允許來自美國和法國的存取，請在方塊中輸入 US, FR，如下所示。  
        
           ![CDN ec_country_allow 範例](./media/cdn-token-auth/cdn-token-auth-country-allow.png)

       - **ec_country_deny**：拒絕來自一或多個指定國家/地區的要求。 來自其他所有國家/地區的要求將會獲得允許。 請使用國碼/地區碼，並以逗號分隔每個國家/地區。 例如，如果您想要拒絕來自美國和法國的存取，請在方塊中輸入 US, FR。
    
       - **ec_ref_allow**︰只允許來自指定訪客來源的要求。 訪客來源會識別連結到所要求之資源的網頁 URL。 請勿在訪客來源參數值中包含通訊協定。 以下是允許作為參數值的輸入類型：
           - 主機名稱或主機名稱和路徑。
           - 多個訪客來源。 若要新增多個訪客來源，請以逗號分隔每個訪客來源。 如果您指定訪客來源值，但因瀏覽器設定而導致不會在要求中傳送訪客來源資訊，系統預設將會拒絕這些要求。 
           - 遺漏訪客來源資訊的要求。 若要允許這些類型的要求，請輸入 "missing" 文字或輸入空白值。 
           - 子網域。 若要允許子網域，請輸入星號 (\*)。 例如，若要允許 `consoto.com` 的所有子網域，請輸入 `*.consoto.com`。 
           
          以下範例說明可針對下列要求允許存取權的輸入：來自 `www.consoto.com` 的要求、來自 `consoto2.com` 底下所有子網域的要求，以及訪客來源為空白或遺漏的要求。
        
          ![CDN ec_ref_allow 範例](./media/cdn-token-auth/cdn-token-auth-referrer-allow2.png)
    
       - **ec_ref_deny**︰拒絕來自指定訪客來源的要求。 實作與 ec_ref_allow 參數相同。
         
       - **ec_proto_allow**︰只允許來自指定通訊協定的要求。 例如 HTTP 或 HTTPS。
            
       - **ec_proto_deny**︰拒絕來自指定通訊協定的要求。 例如 HTTP 或 HTTPS。
    
       - **ec_clientip**︰僅限指定要求者的 IP 位址才能存取。 支援 IPV4 和 IPV6。 您可以指定單一要求 IP 位址或 IP 子網路。
            
         ![CDN ec_clientip 範例](./media/cdn-token-auth/cdn-token-auth-clientip.png)

    3. 輸入完加密參數值之後，請從 [Key To Encrypt] \(要加密的金鑰\) 清單中選取要加密的金鑰類型 (如果您已同時建立主要金鑰和備份金鑰)、從 [Encryption Version] \(加密版本\) 清單中選取加密版本，然後按一下 [Encrypt] \(加密\)。
        
    4. 視需要使用解密工具來測試您的權杖。 將權杖值貼到 [Token to Decrypt] \(要解密的權杖\) 方塊中。 從 [Key To Decrypt] \(要解密的金鑰\) 下拉式清單中選取要解密的加密金鑰類型，然後按一下 [Decrypt] \(解密\)。

    5. 視需要自訂要求遭拒時傳回的回應碼類型。 從 [Response Code] \(回應碼\) 下拉式清單中選取代碼，然後按一下 [Save] \(儲存\)。 預設選取的回應碼是 **403** (禁止)。 針對特定回應碼，您還可以在 [Header Value] \(標頭值\) 方塊中輸入您錯誤頁面的 URL。 

    6. 產生加密的權杖之後，您需將它以查詢字串的形式，附加在 URL 路徑中檔案的結尾。 例如： `http://www.domain.com/content.mov?a4fbc3710fd3449a7c99986b`。

3. 在 [HTTP Large] \(HTTP 大型\) 底下，按一下 [Rules Engine] \(規則引擎\)。 您需使用此規則引擎來定義路徑，以套用功能、啟用權杖驗證功能，以及啟用其他與權杖驗證相關的功能。 如需詳細資訊，請參閱[規則引擎參考](cdn-rules-engine-reference.md)。

    1. 選取現有規則或建立新規則，以定義您想要套用權杖驗證的資產或路徑。 
    2. 若要在規則啟用權杖驗證，請從 [Features] \(功能\) 下拉式清單中選取 [[Token Auth] \(權杖驗證\)](cdn-rules-engine-reference-features.md#token-auth)，然後選取 [Enabled] \(啟用\)。 如果您要更新規則，請按一下 [Update] \(更新\)，或如果您要建立規則，請按一下 [Add] \(新增\)。
        
    ![CDN 規則引擎權杖驗證啟用範例](./media/cdn-token-auth/cdn-rules-engine-enable2.png)

4. 在規則引擎中，您還可以啟用其他權杖驗證相關功能。 若要啟用下列任何功能，請從 [Features] \(功能\) 下拉式清單中選取該功能，然後選取 [Enabled] \(啟用\)。
    
    - **[Token Auth Denial Code](cdn-rules-engine-reference-features.md#token-auth-denial-code)** \(權杖驗證拒絕碼\)：決定當要求遭拒時傳回給使用者的回應類型。 這裡設定的規則會覆寫權杖型驗證頁面之 [Custom Denial Handling] \(自訂拒絕處理\) 區段中設定的回應碼。
    - **[Token Auth Ignore URL Case](cdn-rules-engine-reference-features.md#token-auth-ignore-url-case)** \(權杖驗證忽略 URL 大小寫\)︰決定用來驗證權杖的 URL 是否區分大小寫。
    - **[Token Auth Parameter](cdn-rules-engine-reference-features.md#token-auth-parameter)** \(權杖驗證參數\)︰會將出現在所要求 URL 中的權杖驗證查詢字串參數重新命名。 
        
    ![CDN 規則引擎權杖驗證設定範例](./media/cdn-token-auth/cdn-rules-engine2.png)

5. 您可以存取 [GitHub](https://github.com/VerizonDigital/ectoken).中的原始程式碼來自訂權杖。
可用的語言包括：
    
- C
- C#
- PHP
- Perl
- Java
- Python    

## <a name="azure-cdn-features-and-provider-pricing"></a>Azure CDN 功能和提供者定價

如需相關資訊，請參閱 [CDN 概觀](cdn-overview.md)。
