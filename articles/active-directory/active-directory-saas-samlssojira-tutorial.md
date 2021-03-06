---
title: "教學課程：Azure Active Directory 與 SAML SSO for Jira by resolution GmbH 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SAML SSO for Jira by resolution GmbH 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: cde5983710185d1e46a5601b16bbfb1c0fcae382
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a>教學課程：Azure Active Directory 與 SAML SSO for Jira by resolution GmbH 整合

在本教學課程中，您將了解如何整合 SAML SSO for Jira by resolution GmbH 與 Azure Active Directory (Azure AD)。

SAML SSO for Jira by resolution GmbH 與 Azure AD 整合提供下列優點：

- 您可以在 Azure AD 中控制誰可以存取 SAML SSO for Jira by resolution GmbH
- 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 SAML SSO for Jira by resolution GmbH (單一登入)
- 您可以在 Azure 入口網站中集中管理您的帳戶

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 SAML SSO for Jira by resolution GmbH 整合，您需要下列項目：

- Azure AD 訂用帳戶
- SAML SSO for Jira by resolution GmbH 單一登入已啟用的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫新增 SAML SSO for Jira by resolution GmbH
2. 設定並測試 Azure AD 單一登入

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-the-gallery"></a>從資源庫新增 SAML SSO for Jira by resolution GmbH
若要設定 SAML SSO for Jira by resolution GmbH 到 Azure AD 的整合，您必須從資源庫將 SAML SSO for Jira by resolution GmbH 新增至受管理 SaaS 應用程式的清單。

**若要從資源庫新增 SAML SSO for Jira by resolution GmbH，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![應用程式][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![應用程式][3]

4. 在搜尋方塊中，輸入 **SAML SSO for Jira by resolution GmbH**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. 在結果窗格中，選取 SAML SSO for Jira by resolution GmbH，然後按一下新增 按鈕以新增應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SAML SSO for Jira by resolution GmbH 設定及測試 Azure AD 單一登入。

若要讓單一登入運作，Azure AD 必須知道 SAML SSO for Jira by resolution GmbH 與 Azure AD 中互相對應的使用者。 換句話說，必須在 Azure AD 使用者和 SAML SSO for Jira by resolution GmbH 中的相關使用者之間建立連結關聯性。

在 SAML SSO for Jira by resolution GmbH 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。

若要使用 SAML SSO for Jira by resolution GmbH 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 SAML SSO for Jira by resolution GmbH 測試使用者](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - 讓連結至 Azure AD 之 SAML SSO for Jira by resolution GmbH 中 Britta Simon 的對應使用者表示使用者。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 SAML SSO for Jira by resolution GmbHl 應用程式中設定單一登入。

**若要使用 SAML SSO for Jira by resolution GmbH 設定 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 入口網站的 [SAML SSO for Jira by resolution GmbH] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. 如果您想要以「IDP 起始模式」設定應用程式，請在 [SAML SSO for Jira by resolution GmbH 網域和 URL] 區段上執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    a. 在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<server-base-url>/plugins/servlet/samlsso`

    b. 在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<server-base-url>/plugins/servlet/samlsso`

4. 按一下 [顯示進階 URL 設定]。 如果您想要以 **SP** 起始模式設定應用程式：

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > 這些都不是真正的值。 使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。 請連絡 [SAML SSO for Jira by resolution GmbH 用戶端支援小組](https://www.resolution.de/go/support)以取得這些值。 

5. 在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 **SAML SSO for Jira by resolution GmbH 系統管理入口網站**。

8. 將滑鼠停留在 cog 上，然後按一下 [附加元件]。
    
    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. 系統會將您重新導向至 [系統管理員存取] 頁面。 輸入 [密碼]，然後按一下 [確認] 按鈕。

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. 在附加元件索引標籤區段下，按一下 [尋找新的附加元件]。 搜尋 **SAML Single Sign On (SSO) for JIRA**，然後按一下 [安裝] 按鈕以安裝新的 SAML 外掛程式。

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. 外掛程式將會開始安裝。 按一下 [關閉] 。

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. 按一下 [管理] 。

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. 按一下 [設定] 來設定新的外掛程式。

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. 在 [SAML SingleSignOn 外掛程式組態] 頁面上，按一下 [新增額外的識別提供者] 按鈕以進行識別提供者的設定。

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. 在這個頁面上執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    a. 新增識別提供者的**名稱** (例如 Azure AD)。
    
    b.這是另一個 C# 主控台應用程式。 新增識別提供者的**描述** (例如 Azure AD)。

    c. 按一下 [XML]，然後選取您從 Azure 入口網站下載的**中繼資料**檔案。

    d. 按一下 [載入] 按鈕。

    e. 它會讀取 IdP 中繼資料，並且填入螢幕擷取畫面中反白顯示的欄位。 

16. 按一下 [儲存設定] 按鈕以儲存設定。

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. 若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    a. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。

    b.這是另一個 C# 主控台應用程式。 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。

    c. 選取 [顯示密碼] 並記下 [密碼] 的值。

    d. 按一下 [建立] 。
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a>建立 SAML SSO for Jira by resolution GmbH 測試使用者

若要讓 Azure AD 使用者登入 SAML SSO for Jira by resolution GmbH，必須將他們佈建到 SAML SSO for Jira by resolution GmbH。  
在 SAML SSO for Jira by resolution GmbH 中，佈建是手動工作。

**若要佈建使用者帳戶，請執行下列步驟：**

1. 以系統管理員身分登入 SAML SSO for Jira by resolution GmbH 公司網站。

2. 將滑鼠停留在 cog 上，然後按一下 [使用者管理]。

    ![新增員工](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. 系統會將您重新導向至 [系統管理員存取] 頁面，以輸入**密碼**，然後按一下 [確認] 按鈕。

    ![新增員工](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. 在 [使用者管理] 索引標籤區段下，按一下 [建立使用者]。

    ![新增員工](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. 在 [建立新的使用者] 對話方塊中，執行下列步驟：

    ![新增員工](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    a. 在 [電子郵件地址] 文字方塊中，輸入像是 Brittasimon@contoso.com 的使用者電子郵件地址。

    b.這是另一個 C# 主控台應用程式。 在 [全名] 文字方塊中，輸入像是 Britta Simon 的使用者全名。

    c. 在 [使用者名稱] 文字方塊中，輸入像是 Brittasimon@contoso.com 的使用者電子郵件。

    d. 在 [密碼] 文字方塊中，輸入使用者的密碼。

    e. 按一下 [建立使用者]。   

### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 SAML SSO for Jira by resolution GmbH 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**若要將 Britta Simon 指派至 SAML SSO for Jira by resolution GmbH，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [SAML SSO for Jira by resolution GmbH]。

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。

當您按一下 [存取面板] 中的 [SAML SSO for Jira by resolution GmbH] 圖格時，您應該會自動登入 SAML SSO for Jira by resolution GmbH 應用程式。
如需存取面板的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

