---
title: Monitorar com o SCOM
description: Siga estas etapas para configurar os pacotes de gerenciamento do System Center Operations Manager (SCOM) para o sistema de plataforma de análise. Os pacotes de gerenciamento são necessários para monitorar o sistema de plataforma de análise do SCOM.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 67029d235a1bc65b5ee0ab6f01f51dea42ebcc8b
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401305"
---
# <a name="configure-system-center-operations-manager-scom-to-monitor-analytics-platform-system"></a>Configurar System Center Operations Manager (SCOM) para monitorar o sistema de plataforma de análise
Siga estas etapas para configurar os pacotes de gerenciamento do System Center Operations Manager (SCOM) para o sistema de plataforma de análise. Os pacotes de gerenciamento são necessários para monitorar o sistema de plataforma de análise do SCOM.  
  
## <a name="BeforeBegin"></a>Antes de começar  
**Pré-requisitos**  
  
System Center Operations Manager 2007 R2 deve estar instalado e em execução.  
  
Os pacotes de gerenciamento devem ser instalados e configurados. Consulte [instalar os pacotes de gerenciamento do scom &#40;o sistema de plataforma de análise&#41;](install-the-scom-management-packs.md) e [importar o pacote de gerenciamento do SCOM para o PDW &#40;analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md).  
  
## <a name="ConfigureRunAsProfile"></a>Configurar o perfil executar como no System Center  
Para configurar o System Center, você precisa executar as seguintes etapas:  
  
-   Crie uma conta Executar como para o usuário de domínio do **Inspetor do APS** e mapeie-a para a conta do Inspetor de **APS da Microsoft.**  
  
-   Crie uma conta Executar como para o usuário **monitoring_user** APS e mapeie-a para a **conta de ação APS da Microsoft**.  
  
Aqui estão instruções detalhadas sobre como executar as tarefas:  
  
1.  Crie a conta Executar como do **Inspetor de APS** com o tipo de conta do **Windows** para o usuário de domínio do **Inspetor do APS** .  
  
    1.  Navegue até o painel **Administração** , clique com o botão direito do mouse em**contas** de **configuração** -> executar como e selecione **criar conta Executar como...**  
  
        ![ConfigureScomCreateRunAsAccount](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  A caixa de diálogo **Assistente para criação de conta Executar como** será aberta. Na página **Introdução** clique em **Avançar**.  
  
    3.  Na página **Propriedades gerais** , selecione **Windows** do **tipo de conta Executar como** e especifique "Inspetor de APS" como o **nome de exibição**.  
  
        ![CreateRunAsAccountWizardGeneralProperties](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  Na página **credenciais** , ![CreateRunAsAccountWizardCredentials](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  Na página **segurança de distribuição** , selecione **menos seguro** e clique no botão **criar** para concluir.  
  
        ![CreateRunAsAccountWizardDistributionSecurity](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  Se você decidir usar a opção **mais segura** , será necessário especificar manualmente os computadores nos quais as credenciais serão distribuídas. Para fazer isso, depois de criar a conta Executar como, clique nela com o botão direito do mouse e selecione **Propriedades**.  
  
        2.  Navegue até a guia **distribuição** e **adicione** os computadores desejados.  
  
            ![RunAsAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  Defina o perfil da **conta do Inspetor de APS da Microsoft** para usar a conta Executar como do Inspetor de **APS** .  
  
    1.  Navegue até **Administração** -> **Executar como perfis de configuração** -> ****.  
  
        ![AdministrationRunAsConfigurationProfiles](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  Clique com o botão direito do mouse em **conta do Inspetor de APS da Microsoft** na lista e selecione **Propriedades**.  
  
        ![MicrosoftApsWatcherAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  A caixa de diálogo **Assistente de perfil executar como** será aberta. Ignore a página **introdução** clicando em **Avançar**.  
  
    4.  Na página **Propriedades gerais** , clique em **Avançar**.  
  
    5.  Na página **contas Executar como** , clique no botão **Adicionar...** e selecione a conta Executar como do **Inspetor de APS** criada anteriormente.  
  
        ![RunAsProfileWizardAdd](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  Clique em **salvar** para concluir a atribuição de perfil.  
  
3.  Aguarde até que a descoberta de dispositivos APS seja concluída.  
  
    1.  Navegue até o painel **monitoramento** e abra a exibição de estado**Microsoft Analytics Platform System** -> **appliances** do **dispositivo** -> de SQL Server.  
  
        ![SqlServerApplianceMicrosoftApsAppliances](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  Aguarde até que o dispositivo seja exibido na lista. O nome do dispositivo deve ser igual a um especificado no registro. Após a conclusão da descoberta, você deverá ver todos os dispositivos listados, mas não monitorados. Para habilitar o monitoramento, siga as próximas etapas.  
  
    > [!NOTE]  
    > As próximas etapas podem ser concluídas em paralelo enquanto você aguarda a conclusão da descoberta inicial do dispositivo.  
  
4.  Crie outra nova conta Executar como para consultar os APS para a recuperação de dados de integridade.  
  
    1.  Comece a criar uma nova conta Executar como, conforme descrito na etapa 1.  
  
    2.  Na página **Propriedades gerais** , selecione tipo de conta de **autenticação básica** .  
  
        ![CreateRunAsAccountWizardGeneralProperties2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  Na página **credenciais** , forneça credenciais válidas para acessar DMVs do estado de integridade APS.  
  
        ![CreateRunAsAccountWizardCredentials2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  Configure o perfil de **conta de ação do Microsoft APS** para usar a conta Executar como recém-criada para a instância APS.  
  
    1.  Navegue até as propriedades da **conta de ação do Microsoft APS** conforme descrito na etapa 2.  
  
    2.  Na página **contas Executar como** , clique em **Adicionar...** e 
    3.  Selecione a conta Executar como recém-criada.  
  
        ![RunAsProfileWizardAdd2](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>Próxima etapa  
Agora que você configurou os pacotes de gerenciamento, está pronto para começar a monitorar o dispositivo. Para obter mais informações, consulte [monitorar o dispositivo usando System Center Operations Manager &#40;&#41;do sistema de plataforma de análise ](monitor-the-appliance-by-using-system-center-operations-manager.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
