---
title: Configurar o SCOM para monitorar o Analytics Platform System | Microsoft Docs
description: Siga estas etapas para configurar os pacotes de gerenciamento do System Center Operations Manager (SCOM) para o sistema de plataforma de análise. Os pacotes de gerenciamento necessários para monitorar o Analytics Platform System do SCOM.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4c2e8a42d488c18e705c9d7d8c1d53c9ff7c9cb8
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539396"
---
# <a name="configure-system-center-operations-manager-scom-to-monitor-analytics-platform-system"></a>Configurar o System Center Operations Manager (SCOM) para monitorar o Analytics Platform System
Siga estas etapas para configurar os pacotes de gerenciamento do System Center Operations Manager (SCOM) para o sistema de plataforma de análise. Os pacotes de gerenciamento necessários para monitorar o Analytics Platform System do SCOM.  
  
## <a name="BeforeBegin"></a>Antes de começar  
**Pré-requisitos**  
  
System Center Operations Manager 2007 R2 deve ser instalado e em execução.  
  
Os pacotes de gerenciamento devem ser instalados e configurados. Consulte [instalar os pacotes de gerenciamento do SCOM &#40;Analytics Platform System&#41; ](install-the-scom-management-packs.md) e [importar o pacote de gerenciamento do SCOM para PDW &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md).  
  
## <a name="ConfigureRunAsProfile"></a>Configurar o perfil executar como no System Center  
Para configurar o System Center, você precisa executar as etapas a seguir:  
  
-   Criar conta executar como para o **APS Inspetor** usuário de domínio e mapeie-o para o **conta da Microsoft APS Inspetor.**  
  
-   Criar conta executar como para o **monitoring_user** usuário APS e mapeie-o para o **conta de ação do Microsoft APS**.  
  
Aqui estão as instruções detalhadas sobre como realizar as tarefas:  
  
1.  Criar o **APS Inspetor** conta executar como com **Windows** conta o tipo para o **APS Inspetor** usuário de domínio.  
  
    1.  Navegue até o **administração** painel, clique com botão direito em **configuração Executar como** -> **contas** e selecione **criar conta executar como...**  
  
        ![ConfigureScomCreateRunAsAccount](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  O **Assistente executar como conta** caixa de diálogo será aberta. Sobre o **Introdução** , clique em **próximo**.  
  
    3.  No **propriedades gerais** página, selecione **Windows** de **o tipo de conta executar como** e especifique "Inspetor de APS" como o **nome de exibição**.  
  
        ![CreateRunAsAccountWizardGeneralProperties](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  Sobre o **credenciais** página, ![CreateRunAsAccountWizardCredentials](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  No **segurança de distribuição** página, selecione **menos seguro** e clique no **criar** botão para concluir.  
  
        ![CreateRunAsAccountWizardDistributionSecurity](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  Se você decidir usar o **mais seguro** opção, você precisa especificar manualmente os computadores aos quais as credenciais serão distribuídas. Para fazer isso, depois de criar a conta executar como, clique nele e selecione **propriedades**.  
  
        2.  Navegue até o **distribuição** guia e **adicionar** desejado de computadores.  
  
            ![RunAsAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  Definir o **conta da Microsoft APS Inspetor** perfil para usar **APS Inspetor** conta executar como.  
  
    1.  Navegue até **administração** -> **configuração de executar como** -> **perfis**.  
  
        ![AdministrationRunAsConfigurationProfiles](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  Clique com o botão direito em **conta da Microsoft APS Inspetor** na lista e selecione **propriedades**.  
  
        ![MicrosoftApsWatcherAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  O **Assistente executar como perfil** caixa de diálogo será aberta. Ignorar o **Introdução** página clicando em **próximo**.  
  
    4.  Sobre o **propriedades gerais** , clique em **próximo**.  
  
    5.  Sobre o **contas executar como** , clique no **adicionar...** botão e selecione criado anteriormente **APS Inspetor** conta executar como.  
  
        ![RunAsProfileWizardAdd](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  Clique em **salvar** para concluir a atribuição do perfil.  
  
3.  Aguarde a conclusão da descoberta de dispositivos de APS.  
  
    1.  Navegue até o **monitoramento** painel e abrir o **SQL Server Appliance** -> **Microsoft Analytics Platform System**  ->   **Dispositivos** exibição de estado.  
  
        ![SqlServerApplianceMicrosoftApsAppliances](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  Aguarde até que o dispositivo aparece na lista. O nome do dispositivo deve ser igual àquele especificado no registro. Após a conclusão da descoberta, você deve ver todos os dispositivos listados, mas não monitorados. Para habilitar o monitoramento, siga as próximas etapas.  
  
    > [!NOTE]  
    > As próximas etapas podem ser concluídas em paralelo, enquanto estão aguardando a descoberta inicial do dispositivo concluir.  
  
4.  Crie outra nova conta executar como para consultar APS de recuperação de dados de integridade.  
  
    1.  Começar a criar uma nova conta executar como, conforme descrito na etapa 1.  
  
    2.  Sobre o **propriedades gerais** página, selecione **autenticação básica** tipo de conta.  
  
        ![CreateRunAsAccountWizardGeneralProperties2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  Sobre o **credenciais** página, forneça credenciais válidas para acessar o estado de integridade APS DMVs.  
  
        ![CreateRunAsAccountWizardCredentials2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  Configurar o **conta de ação do Microsoft APS** perfil para usar a conta executar como criada recentemente para a instância APS.  
  
    1.  Navegue até o **conta de ação do Microsoft APS** propriedades conforme descrito na etapa 2.  
  
    2.  Sobre o **contas executar como** , clique em **adicionar...** e 
    3.  Selecione a conta executar como criada recentemente.  
  
        ![RunAsProfileWizardAdd2](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>Próxima etapa  
Agora que você configurou os pacotes de gerenciamento, você está pronto para iniciar o monitoramento do dispositivo. Para obter mais informações, consulte [monitorar o dispositivo por usando o System Center Operations Manager &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
