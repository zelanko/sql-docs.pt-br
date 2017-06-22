---
title: "Integração do servidor de relatórios de BI (Configuration Manager) de energia | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- pbi
- power bi
- power bi integration
ms.assetid: 902b7c31-7399-4855-90f2-42f89d847fff
caps.latest.revision: 22
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 5ece1f5e492f4508d6c014709a953bfb4d29815a
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---

# <a name="power-bi-report-server-integration-configuration-manager"></a>Integração de servidor de relatório do Power BI (Configuration Manager)

[!INCLUDE[ssrs-appliesto-sql2016-preview](../../includes/ssrs-appliesto-sql2016-preview.md)]

A página  **Integração do Power BI** no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager é usada para registrar o servidor de relatório no locatário gerenciado do Azure AD (Active Directory) desejado, a fim de permitir que os usuários do servidor de relatório fixem itens de relatório com suporte nos dashboards do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] . Para obter uma lista dos itens com suporte que podem ser fixados, veja [Fixar itens do Reporting Services nos dashboards do Power BI](../../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md).

![rs_powerbi_icon](../../reporting-services/media/ssrs-powerbi-icon.png "rs_powerbi_icon")

##  <a name="bkmk_requirements"></a> Requisitos para integração do Power BI

Além de uma conexão de Internet ativa para que você possa navegar até o serviço do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] , estes são os requisitos para concluir a integração do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)].

- **Azure Active Directory:** sua organização deve usar o Azure Active Directory, que fornece gerenciamento de identidades e diretórios para serviços e aplicativos Web do Azure. Para saber mais, confira [O que é o Azure Active Directory?](https://azure.microsoft.com/en-us/documentation/articles/active-directory-whatis/)

- **Locatário gerenciado:** o painel do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] ao qual você deseja fixar itens de relatório devem ser parte de um locatário gerenciado do Azure AD.  Um locatário gerenciado é criado automaticamente na primeira vez em que sua empresa assina os serviços do Azure, como o Office 365 e o Microsoft Intune.   Locatários virais não têm suporte atualmente.  Para obter mais informações, confira as seções “O que é um locatário do Azure AD” e “Como obter um diretório do Azure AD” em [O que é um diretório do Azure AD?](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant)

- O usuário que executando a integração do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] precisa ser um membro do locatário do Azure AD, um administrador de sistema do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e um administrador de sistema para o banco de dados de catálogo ReportServer.

- O usuário que executa a integração do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] precisa iniciar o Configuration Manager do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com a conta usada para instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]ou a conta do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em execução em

- Os relatórios dos quais você deseja fixar devem usar credenciais armazenadas. Isso não é um requisito da própria integração do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] , mas do processo de atualização para os itens fixados.  A ação de fixar um item de relatório cria uma assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para gerenciar o agendamento de atualização dos blocos no [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] exigem credenciais armazenadas. Se um relatório não usar credenciais armazenadas, um usuário poderá ainda assim fixar itens de relatório, mas quando a assinatura associada tentar atualizar os dados para o [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)], você verá uma mensagem de erro semelhante à seguinte na página **Minhas Assinaturas** .

        PowerBI Delivery error: dashboard: IT Spend Analysis Sample, visual: Chart2, error: The current action cannot be completed. The user data source credentials do not meet the requirements to run this report or shared dataset. Either the user data source credential.

Para obter mais informações sobre como armazenar credenciais, consulte a seção "Configurar credenciais armazenadas para uma fonte de dados específica do relatório" na [armazenar credenciais em uma fonte de dados do Reporting Services](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md).

Um administrador pode examinar os arquivos de log do  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para saber mais.  Ele verá mensagens semelhantes à seguinte. ![Observação](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "Observação") uma ótima maneira de analisar e monitorar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] arquivos de log é usar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Power Query nos arquivos.  Para saber mais e para assistir a um vídeo curto, veja [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md).

    subscription!WindowsService_1!1458!09/24/2015-00:09:27:: e ERROR: PowerBI Delivery error: dashboard: IT Spend Analysis Sample, visual: Chart2, error: The current action cannot be completed. The user data source credentials do not meet the requirements to run this report or shared dataset. Either the user data source credentials are not stored in the report server database, or the user data source is configured not to require credentials but the unattended execution account is not specified.

    notification!WindowsService_1!1458!09/24/2015-00:09:27:: e ERROR: Error occurred processing subscription fcdb8581-d763-4b3b-ba3e-8572360df4f9: PowerBI Delivery error: dashboard: IT Spend Analysis Sample, visual: Chart2, error: The current action cannot be completed. The user data source credentials do not meet the requirements to run this report or shared data set. Either the user data source credentials are not stored in the report server database, or the user data source is configured not to require credentials but the unattended execution account is not specified.

##  <a name="bkmk_steps2integrate"></a> Para integrar e registrar o Servidor de Relatório

Conclua as seguintes etapas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager. Para obter mais informações, consulte [Reporting Services Configuration Manager](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).

1. Selecione a página de integração do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] .

     ![rs_powerbi_integration](../../reporting-services/install-windows/media/ssrs-powerbi-integration.png "rs_powerbi_integration")

2. Selecione **Registrar no Power BI**.

3. Na caixa de diálogo de entrada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] , insira as credenciais que você usa para entrar no [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)].

4. Depois que o registro tiver sido concluído, a seção **Detalhes do registro do Power BI** anotará a ID de Locatário do Azure e as URLs de Redirecionamento.  As URLs são usadas como parte do processo de entrada e comunicação do painel do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] para se comunicar de volta com o servidor de relatório registrado.

5. ![Observação](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "Observação") selecionar o **cópia** no botão de **resultados** janela para copiar os detalhes do registro para a área de transferência do Windows para que possa salvá-los para referência futura.

##  <a name="bkmk_unregister"></a> Cancelar o registro com o Power BI

**Cancelar o registro:** o cancelamento do registro do servidor de relatório do Azure Active Directory resultará no seguinte:

- O **minhas configurações** link não será visível na barra de menu do portal da web.

- Os itens de relatório que já tiverem sido fixados continuarão fixados nos painéis; no entanto, os blocos não serão atualizados no painel.

- As assinaturas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que estavam atualizando os blocos ainda existirá no servidor de relatório, mas, ao serem executados em seu agendamento configurado, mostrarão uma mensagem de erro semelhante à seguinte.

    **Não foi possível carregar a extensão de entrega desta assinatura.**

Na página do **Power BI** do Configuration Manager, selecione o botão **Cancelar registro no Power BI** .

##  <a name="bkmk_updateregistration"></a> Atualizar registro

Use **Atualizar Registro** se a configuração do seu servidor de relatório tiver sido alterada. Por exemplo, se você deseja adicionar ou remover as URLS que seus usuários usam para navegar até o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)].

- No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager, selecione a **URL do Portal da Web**

     Selecione **Avançado**.

- Selecione **Adicionar** para adicionar uma nova identidade HTTP para [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] e selecione **OK**.

     O ícone [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] será alterado para indicar que a configuração do servidor foi alterada.  ![ssrs_powebi_icon_warning](../../reporting-services/install-windows/media/ssrs-powebi-icon-warning.png "ssrs_powebi_icon_warning")

- Na página **Integração do Power BI** , clique em **Atualizar Registro**.

     Você precisará fazer logon no Azure AD. A página será atualizada e você verá a nova URL listada nas **URLs de redirecionamento**.

##  <a name="bkmk_integration_process"></a> Resumo do processo de fixação e integração do Power BI

Esta seção resume as etapas básicas e as tecnologias envolvidas ao integrar seu servidor de relatório com o [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] e fixar um item de relatório em um painel.

 **Integrar:**

1. No Configuration Manager, quando você seleciona o botão **Registrar-se no Power BI** , será solicitado que você entre no Azure Active Directory.

2. O Aplicativo Cliente do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] está registrado em seu locatário gerenciado.

3. Seu locatário gerenciado dentro do Azure Active Directory é onde o aplicativo cliente do Power BI é criado.

4. O registro inclui uma URL de redirecionamento que é usada quando os usuários entram no servidor de relatório.  A ID do aplicativo e as URLS são salvas no banco de dados ReportServer. A URL de redirecionamento é usada durante as chamadas de autenticação do Azure para que a chamada possa retornar para o servidor de relatório. Por exemplo, quando os usuários entrarem ou fixar itens em um painel.

5. A ID do aplicativo e as URLS são exibidas no Configuration Manager.

 ![ssrs_pbiflow_integration](../../reporting-services/install-windows/media/ssrs-pbiflow-integration.png "ssrs_pbiflow_integration")

 **Quando um usuário fixar um item de relatório em um painel:**

1. Os usuários visualizam relatórios no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] e na primeira vez que clicarem para fixar um item de relatório do [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)].

2. Eles serão redirecionados para a página de logon do Azure AD. Eles também podem entrar por meio da página [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] **My Settings** page. Quando os usuários entram no locatário gerenciado do Azure, uma relação é estabelecida entre a sua conta do Azure e as permissões do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  Para saber mais, confira [Minhas Configurações para integração do Power BI &#40;portal Web&#41;](http://msdn.microsoft.com/en-us/85c2fac7-80bf-45b7-8654-764b5f5231f5).

3. Um token de segurança do usuário é retornado para o servidor de relatório.

4. O token de segurança do usuário é salvo no banco de dados ReportServer.

5. Uma lista de grupos e painéis aos quais o usuário tem acesso são recuperados do serviço do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] .  O usuário seleciona o grupo de destino e o painel, e configura a frequência de atualização dos dados no bloco do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] .

6. O item de relatório é fixado no painel.

7. Uma assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é criada para gerenciar a atualização agendada do item de relatório para o bloco do painel. A assinatura usa o token de segurança que foi criado quando o usuário se conectou.

     **Observação:**  o token é válido para **90 dias**, depois disso, os usuários precisam fazer logon novamente para criar um novo token. Quando o token tiver expirado, os blocos fixos ainda estarão exibidos no painel, mas os dados não serão atualizados.  As assinaturas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usadas para os itens fixados gerarão um erro até que um novo token de usuário seja criado. Veja [Minhas Configurações para integração do Power BI &#40;portal Web&#41;](http://msdn.microsoft.com/en-us/85c2fac7-80bf-45b7-8654-764b5f5231f5). para obter mais informações.

Na segunda vez que um usuário fixar um item, as etapas de 1 a 4 são ignoradas e, em vez disso, a ID do aplicativo e as URLS serão recuperadas do banco de dados ReportServer e o fluxo continuará com a etapa 5.

![ssRS-pin-to-powerbi-flow](../../reporting-services/install-windows/media/ssrs-pin-to-powerbi-flow.png)

 **Quando uma assinatura é acionada para atualizar um bloco do painel:**

1. Quando a assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é acionada, o relatório é renderizado.

2. O token de usuário é recuperado do banco de dados ReportServer.

3. O estado do item de relatório e os dados são enviados com o token para o serviço do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)].

4. O token é enviado para o Azure AD para validação. Se o token for válido, os dados do item de relatório serão enviados para o bloco do painel e a propriedade de data do bloco será atualizada.

5. Se o token não for válido e o erro será retornado e registrado no servidor de relatório.  Nenhum status ou outra informação é enviada para o painel.

![ssRS-subscription-to-powerbi-flow](../../reporting-services/install-windows/media/ssrs-subscription-to-powerbi-flow.png)

<iframe width="560" height="315" src="https://www.youtube.com/embed/QhPQObqmMPc" frameborder="0" allowfullscreen></iframe>

## <a name="next-steps"></a>Próximas etapas

[Minhas configurações para integração do Power BI](http://msdn.microsoft.com/en-us/85c2fac7-80bf-45b7-8654-764b5f5231f5)  
[Fixar itens do Reporting Services nos painéis do Power BI](../../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)   
[Painéis no Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
