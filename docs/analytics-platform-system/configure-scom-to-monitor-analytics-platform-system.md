---
title: Configurar o SCOM para monitorar o Analytics Platform System | Microsoft Docs
description: Siga estas etapas para configurar os pacotes de gerenciamento do System Center Operations Manager (SCOM) para o Analytics Platform System. Os pacotes de gerenciamento necessários para monitorar o Analytics Platform System do SCOM.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2dae92263d7be76490a51ea7027f79ab5fcd6118
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62509681"
---
# <a name="configure-system-center-operations-manager-scom-to-monitor-analytics-platform-system"></a>Configurar o System Center Operations Manager (SCOM) para monitorar o Analytics Platform System
Siga estas etapas para configurar os pacotes de gerenciamento do System Center Operations Manager (SCOM) para o Analytics Platform System. Os pacotes de gerenciamento necessários para monitorar o Analytics Platform System do SCOM.  
  
## <a name="BeforeBegin"></a>Antes de começar  
**Pré-requisitos**  
  
System Center Operations Manager 2007 R2 deve ser instalado e em execução.  
  
Os pacotes de gerenciamento devem ser instalados e configurados. Ver [instalar os pacotes de gerenciamento do SCOM &#40;Analytics Platform System&#41; ](install-the-scom-management-packs.md) e [importar o pacote de gerenciamento do SCOM para PDW &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md).  
  
## <a name="ConfigureRunAsProfile"></a>Configurar o perfil executar como no System Center  
Para configurar o System Center, você deve executar as seguintes etapas:  
  
-   Criar conta executar como para o **Inspetor de APS** usuário de domínio e mapeá-lo para o **conta da Microsoft APS observador.**  
  
-   Criar conta executar como para o **monitoring_user** usuário APS e mapeá-lo para o **conta de ação do Microsoft APS**.  
  
Aqui estão as instruções detalhadas sobre como realizar as tarefas:  
  
1.  Criar o **Inspetor de APS** conta executar como com **Windows** conta de tipo para o **APS observador** usuário de domínio.  
  
    1.  Navegue até a **Administration** painel, clique com botão direito em **configuração Executar como** -> **contas** e selecione **criar conta executar como...**  
  
        ![ConfigureScomCreateRunAsAccount](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  O **criar Assistente executar como conta** caixa de diálogo será aberta. Sobre o **Introdução** , clique em **próxima**.  
  
    3.  No **propriedades gerais** página, selecione **Windows** da **tipo de conta executar como** e especifique o "Inspetor de APS" como o **nome de exibição**.  
  
        ![CreateRunAsAccountWizardGeneralProperties](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  Sobre o **credenciais** página, ![CreateRunAsAccountWizardCredentials](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  No **segurança do Distribution** página, selecione **menos seguro** e clique no **criar** botão para concluir.  
  
        ![CreateRunAsAccountWizardDistributionSecurity](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  Se você decidir usar o **mais seguro** opção, você precisa especificar manualmente os computadores para os quais credenciais serão distribuídas. Para fazer isso, depois de criar a conta executar como, clique com botão direito nele e selecione **propriedades**.  
  
        2.  Navegue até a **distribuição** guia e **Add** desejado de computadores.  
  
            ![RunAsAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  Defina a **conta da Microsoft APS observador** perfil para usar **APS observador** conta executar como.  
  
    1.  Navegue até **Administration** -> **executar como configuração** -> **perfis**.  
  
        ![AdministrationRunAsConfigurationProfiles](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  Clique com botão direito **conta da Microsoft APS observador** na lista e selecione **propriedades**.  
  
        ![MicrosoftApsWatcherAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  O **Assistente executar como perfil** caixa de diálogo será aberta. Ignorar a **Introduction** página clicando **próxima**.  
  
    4.  Sobre o **propriedades gerais** , clique em **próxima**.  
  
    5.  Sobre o **contas executar como** , clique no **adicionar...**  botão e selecione criado anteriormente **APS observador** conta executar como.  
  
        ![RunAsProfileWizardAdd](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  Clique em **salvar** para concluir a atribuição de perfil.  
  
3.  Aguarde até que a descoberta de dispositivos de APS estiver concluída.  
  
    1.  Navegue até a **monitoramento** painel e abrir o **SQL Server Appliance** -> **Microsoft Analytics Platform System**  ->   **Dispositivos** exibição de estado.  
  
        ![SqlServerApplianceMicrosoftApsAppliances](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  Aguarde até que o dispositivo aparece na lista. O nome do dispositivo deve ser igual àquele especificado no registro. Após a descoberta estiver concluída, você deve ver todos os dispositivos listados, mas não monitorado. Para habilitar o monitoramento, siga as próximas etapas.  
  
    > [!NOTE]  
    > As próximas etapas podem ser concluídas em paralelo, enquanto aguardam a descoberta inicial do dispositivo concluir.  
  
4.  Crie outra nova conta executar como para consultar APS para recuperação de dados de integridade.  
  
    1.  Começar a criar uma nova conta executar como, conforme descrito na etapa 1.  
  
    2.  Sobre o **propriedades gerais** página, selecione **autenticação básica** tipo de conta.  
  
        ![CreateRunAsAccountWizardGeneralProperties2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  Sobre o **credenciais** página, forneça credenciais válidas para acessar o estado de integridade APS DMVs.  
  
        ![CreateRunAsAccountWizardCredentials2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  Configurar o **conta de ação do Microsoft APS** perfil para usar a conta executar como criada recentemente para a instância APS.  
  
    1.  Navegue até a **conta de ação do Microsoft APS** propriedades conforme descrito na etapa 2.  
  
    2.  Sobre o **contas executar como** , clique em **adicionar...**  e 
    3.  Selecione a conta executar como criada recentemente.  
  
        ![RunAsProfileWizardAdd2](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>Próxima etapa  
Agora que você configurou os pacotes de gerenciamento, você está pronto para começar a monitorar o dispositivo. Para obter mais informações, consulte [monitorar o dispositivo por usando o System Center Operations Manager &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
