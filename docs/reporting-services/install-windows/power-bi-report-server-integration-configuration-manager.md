---
description: Integração de servidor de relatório do Power BI (Configuration Manager)
title: Integração do Servidor de Relatórios do Power BI (Gerenciador de Configurações) | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.date: 09/17/2017
ms.openlocfilehash: 47964ebf5702542452227589e1426948825cc216
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92678869"
---
# <a name="power-bi-report-server-integration-configuration-manager"></a>Integração de servidor de relatório do Power BI (Configuration Manager)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

A página  **Integração do Power BI** no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager é usada para registrar o servidor de relatório no locatário gerenciado do Azure AD (Active Directory) desejado, a fim de permitir que os usuários do servidor de relatório fixem itens de relatório com suporte nos dashboards do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] . Para obter uma lista dos itens com suporte que podem ser fixados, veja [Fixar itens do Reporting Services nos dashboards do Power BI](../../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md).

## <a name="requirements-for-power-bi-integration"></a><a name="bkmk_requirements"></a> Requisitos para integração do Power BI

Além de uma conexão de Internet ativa para que você possa navegar até o serviço do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] , estes são os requisitos para concluir a integração do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)].

- **Azure Active Directory:** sua organização deve usar o Azure Active Directory, que fornece gerenciamento de identidades e diretórios para serviços e aplicativos Web do Azure. Para obter mais informações, confira [O que é Azure Active Directory?](/azure/active-directory/fundamentals/active-directory-whatis)

- **Locatário gerenciado:** o painel do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] ao qual você deseja fixar itens de relatório devem ser parte de um locatário gerenciado do Azure AD.  Um locatário gerenciado é criado automaticamente na primeira vez em que sua empresa assina os serviços do Azure, como o Microsoft 365 e o Microsoft Intune.   Não há suporte para locatários virais no momento.  Para obter mais informações, confira as seções “O que é um locatário do Azure AD” e “Como obter um diretório do Azure AD” em [O que é um diretório do Azure AD?](/previous-versions/azure/azure-services/jj573650(v=azure.100)#BKMK_WhatIsAnAzureADTenant)

- O usuário que executando a integração do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] precisa ser um membro do locatário do Azure AD, um administrador de sistema do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e um administrador de sistema para o banco de dados de catálogo ReportServer.

- O usuário que executa a integração do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] precisa iniciar o Configuration Manager do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com a conta usada para instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]ou a conta do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em execução em

- Os relatórios dos quais você deseja fixar devem usar credenciais armazenadas. Isso não é um requisito da própria integração do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] , mas do processo de atualização para os itens fixados.  A ação de fixar um item de relatório cria uma assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para gerenciar o agendamento de atualização dos blocos no [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] exigem credenciais armazenadas. Se um relatório não usar credenciais armazenadas, um usuário poderá ainda assim fixar itens de relatório, mas quando a assinatura associada tentar atualizar os dados para o [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)], você verá uma mensagem de erro semelhante à seguinte na página **Minhas Assinaturas** .

    PowerBI Delivery error: dashboard: IT Spend Analysis Sample, visual: Chart2, error: A ação atual não pode ser concluída. As credenciais da fonte de dados do usuário não atendem aos requisitos para executar esse relatório ou conjunto de dados compartilhado. A credencial da fonte de dados do usuário.

Para obter mais informações sobre como armazenar credenciais, consulte a seção “Configurar as credenciais armazenadas para uma fonte de dados específica ao relatório” em [Armazenar as credenciais em uma fonte de dados do Reporting Services](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md).

Um administrador pode examinar os arquivos de log do  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para saber mais.  Ele verá mensagens semelhantes à seguinte. Uma ótima maneira de examinar e monitorar arquivos de log do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é usar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Power Query nos arquivos.  Para saber mais e para assistir a um vídeo curto, veja [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md).

- subscription!WindowsService_1!1458!09/24/2015-00:09:27:: e ERROR: Erro de Entrega do PowerBI: painel: Amostra de Análise de Gastos de TI, visual: Gráfico2, erro: A ação atual não pode ser concluída. As credenciais da fonte de dados do usuário não atendem aos requisitos para executar esse relatório ou conjunto de dados compartilhado. Ou as credenciais de fonte de dados do usuário não estão armazenadas no banco de dados de servidor de relatório ou a fonte de dados do usuário está configurada para não exigir credenciais, mas a conta de execução autônoma não foi especificada.

- notification!WindowsService_1!1458!09/24/2015-00:09:27:: e ERROR: Erro de processamento da assinatura fcdb8581-d763-4b3b-ba3e-8572360df4f9: Erro de Entrega do PowerBI: painel: Amostra de Análise de Gastos de TI, visual: Gráfico2, erro: A Ação atual não pode ser concluída. As credenciais da fonte de dados do usuário não atendem aos requisitos para executar esse relatório ou conjunto de dados compartilhado. Ou as credenciais de fonte de dados do usuário não estão armazenadas no banco de dados de servidor de relatório ou a fonte de dados do usuário está configurada para não exigir credenciais, mas a conta de execução autônoma não foi especificada.

## <a name="to-integrate-and-register-the-report-server"></a><a name="bkmk_steps2integrate"></a> Para integrar e registrar o Servidor de Relatório

Conclua as seguintes etapas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager. Para obter mais informações, consulte [Gerenciador de Configurações do Servidor de Relatório](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).

1. Selecione a página de integração do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] .

2. Selecione **Registrar no Power BI**.

    >[!Note]
    > Certifique-se de que a porta 443 não está bloqueada.

3. Na caixa de diálogo de entrada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] , insira as credenciais que você usa para entrar no [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)].

4. Depois que o registro tiver sido concluído, a seção **Detalhes do registro do Power BI** anotará a ID de Locatário do Azure e as URLs de Redirecionamento.  As URLs são usadas como parte do processo de entrada e comunicação do painel do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] para se comunicar de volta com o servidor de relatório registrado.

5. Selecione o botão **Copiar** na janela **Resultados** para copiar os detalhes do registro na área de transferência do Windows e salvá-los para referência futura.

## <a name="unregister-with-power-bi"></a><a name="bkmk_unregister"></a> Cancelar o registro com o Power BI

**Cancelar o registro:** o cancelamento do registro do servidor de relatório do Azure Active Directory resultará no seguinte:

- O link **Minhas Configurações** não será mais visível na barra de menus do portal da Web.

- Os itens de relatório que já tiverem sido fixados continuarão fixados nos painéis; no entanto, os blocos não serão atualizados no painel.

- As assinaturas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que estavam atualizando os blocos ainda existirá no servidor de relatório, mas, ao serem executados em seu agendamento configurado, mostrarão uma mensagem de erro semelhante à seguinte.

    **Não foi possível carregar a extensão de entrega desta assinatura.**

Na página do **Power BI** do Configuration Manager, selecione o botão **Cancelar registro no Power BI** .

##  <a name="update-registration"></a><a name="bkmk_updateregistration"></a> Atualizar registro

Use **Atualizar Registro** se a configuração do seu servidor de relatório tiver sido alterada. Por exemplo, se você deseja adicionar ou remover as URLS que seus usuários usam para navegar até o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)].

- No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager, selecione a **URL do Portal da Web**

     Selecione **Avançado**.

- Selecione **Adicionar** para adicionar uma nova identidade HTTP para [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] e selecione **OK**.

     O ícone [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] será alterado para indicar que a configuração do servidor foi alterada.  ![ssrs_powebi_icon_warning](../../reporting-services/install-windows/media/ssrs-powebi-icon-warning.png "ssrs_powebi_icon_warning")

- Na página **Integração do Power BI** , clique em **Atualizar Registro**.

     Você precisará fazer logon no Azure AD. A página será atualizada e você verá a nova URL listada nas **URLs de redirecionamento**.

##  <a name="summary-of-the-power-bi-integration-and-pin-process"></a><a name="bkmk_integration_process"></a> Resumo do processo de fixação e integração do Power BI

Esta seção resume as etapas básicas e as tecnologias envolvidas ao integrar seu servidor de relatório com o [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] e fixar um item de relatório em um painel.

 **Integrar:**

1. No Configuration Manager, quando você seleciona o botão **Registrar-se no Power BI** , será solicitado que você entre no Azure Active Directory.

2. O Aplicativo Cliente do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] está registrado em seu locatário gerenciado.

3. Seu locatário gerenciado dentro do Azure Active Directory é onde o aplicativo cliente do Power BI é criado.

4. O registro inclui uma URL de redirecionamento que é usada quando os usuários entram no servidor de relatório.  A ID do aplicativo e as URLS são salvas no banco de dados ReportServer. A URL de redirecionamento é usada durante as chamadas de autenticação do Azure para que a chamada possa retornar para o servidor de relatório. Por exemplo, quando os usuários entrarem ou fixarem itens em um painel.

5. A ID do Aplicativo e as URLS são exibidas no Gerenciador de Configurações.

 ![ssrs_pbiflow_integration](../../reporting-services/install-windows/media/ssrs-pbiflow-integration.png "ssrs_pbiflow_integration")

 **Quando um usuário fixar um item de relatório em um painel:**

1. Os usuários visualizam relatórios no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] e na primeira vez que clicarem para fixar um item de relatório do [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)].

2. Eles serão redirecionados para a página de logon do Azure AD. Eles também poderão entrar por meio da página  **Minhas configurações** do [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]. Quando os usuários entram no locatário gerenciado do Azure, uma relação é estabelecida entre a sua conta do Azure e as permissões do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  Para obter mais informações, consulte [Minhas Configurações para integração do Power BI &#40;portal da Web&#41;](../my-settings-for-power-bi-integration-web-portal.md).

3. Um token de segurança do usuário é retornado para o servidor de relatório.

4. O token de segurança do usuário é salvo no banco de dados ReportServer.

5. Uma lista de grupos e painéis aos quais o usuário tem acesso são recuperados do serviço do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] .  O usuário seleciona o grupo de destino e o painel, e configura a frequência de atualização dos dados no bloco do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] .

6. O item de relatório é fixado no painel.

7. Uma assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é criada para gerenciar a atualização agendada do item de relatório para o bloco do painel. A assinatura usa o token de segurança que foi criado quando o usuário se conectou.

     O token é válido por **90 dias** e, após esse período, os usuários precisam fazer logon novamente para criar um novo token de usuário. Quando o token tiver expirado, os blocos fixos ainda estarão exibidos no painel, mas os dados não serão atualizados.  As assinaturas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usadas para os itens fixados gerarão um erro até que um novo token de usuário seja criado. Consulte [Minhas Configurações para integração do Power BI &#40;portal da Web&#41;](../my-settings-for-power-bi-integration-web-portal.md). para obter mais informações.

Na segunda vez que um usuário fixar um item, as etapas de 1 a 4 são ignoradas e, em vez disso, a ID do aplicativo e as URLS serão recuperadas do banco de dados ReportServer e o fluxo continuará com a etapa 5.

![Diagrama mostrando o que ocorre quando um usuário fixa o item de um relatório em um dashboard.](../../reporting-services/install-windows/media/ssrs-pin-to-powerbi-flow.png)

 **Quando uma assinatura é acionada para atualizar um bloco do painel:**

1. Quando a assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é acionada, o relatório é renderizado.

2. O token de usuário é recuperado do banco de dados ReportServer.

3. O estado do item de relatório e os dados são enviados com o token para o serviço do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)].

4. O token é enviado para o Azure AD para validação. Se o token for válido, os dados do item de relatório serão enviados para o bloco do painel e a propriedade de data do bloco será atualizada.

5. Se o token não for válido e o erro será retornado e registrado no servidor de relatório.  Nenhum status ou outra informação é enviada para o painel.

![Diagrama mostrando o que ocorre quando uma assinatura é acionada para atualizar um bloco do dashboard.](../../reporting-services/install-windows/media/ssrs-subscription-to-powerbi-flow.png)

   <iframe width="560" height="315" src="https://www.youtube.com/embed/QhPQObqmMPc" frameborder="0" allowfullscreen></iframe>

## <a name="considerations-and-limitations"></a>Considerações e limitações

* Locatários virais e governamentais não têm suporte.

## <a name="next-steps"></a>Próximas etapas

[Minhas configurações para integração do &#40;portal Web&#41; do Power BI](../my-settings-for-power-bi-integration-web-portal.md)  
[Fixar itens do Reporting Services nos painéis do Power BI](../../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)
[Painéis no Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)