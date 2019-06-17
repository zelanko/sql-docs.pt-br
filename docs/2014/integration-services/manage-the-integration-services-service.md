---
title: Gerenciar o serviço do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services service, configuring
- services [Integration Services], configuring
ms.assetid: 45554117-a0df-4830-b41c-5ebb33b764a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fc3b1eb4e73b3d77b49cc9f485e0a6fc456a8875
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057786"
---
# <a name="manage-the-integration-services-service"></a>Gerenciar o serviço Integration Services
    
> [!IMPORTANT]  
>  Esse tópico discute o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , um serviço do Windows para o gerenciamento de pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] dá suporte ao serviço para compatibilidade de versões anteriores com versões anteriores do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. A partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], você pode gerenciar objetos como pacotes no servidor do Integration Services.  
  
 Quando você instala o componente [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] também é instalado. Por padrão, o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é iniciado e o tipo de inicialização do serviço é definido como automático. Porém, você também precisa instalar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para usar o serviço para gerenciar pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em execução e armazenados.  
  
> [!NOTE]  
>  Você não pode se conectar a uma instância da [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] partir os [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] versão do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. Ou seja, na caixa de diálogo **Conectar ao Servidor** , você não pode informar o nome de um servidor no qual esteja sendo executada apenas a versão do [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] do serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Entretanto, você pode editar o arquivo de configuração do serviço e, desse modo, gerenciar os pacotes armazenados em uma instância do [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] a partir da versão do [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. Para obter mais informações, consulte [Configurando o Serviço Integration Services &#40;Serviço SSIS#41;](service/integration-services-service-ssis-service.md).  
  
 Você pode instalar apenas uma única instância do serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em um computador. O serviço não é específico de uma determinada instância do [!INCLUDE[ssDE](../includes/ssde-md.md)]. Você se conecta ao serviço usando o nome do computador no qual ele está sendo executado.  
  
 Você pode gerenciar o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] usando um dos seguintes snap-ins do MMC (Console de Gerenciamento Microsoft): SQL Server Configuration Manager ou Services. Antes que você possa gerenciar pacotes em [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], é preciso se certificar que o serviço foi iniciado.  
  
 Por padrão, o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é configurado para gerenciar pacotes no banco de dados msdb de uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] que é instalada ao mesmo tempo em que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Se uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] não for instalada ao mesmo tempo, o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] será configurado para gerenciar pacotes no banco de dados msdb de uma instância local padrão do [!INCLUDE[ssDE](../includes/ssde-md.md)]. Para gerenciar pacotes que estão armazenados em uma instância nomeada ou remota do [!INCLUDE[ssDE](../includes/ssde-md.md)], ou em várias instâncias do [!INCLUDE[ssDE](../includes/ssde-md.md)], é preciso modificar o arquivo de configuração para o serviço. Para obter mais informações, consulte [Configurando o Serviço Integration Services &#40;Serviço SSIS#41;](service/integration-services-service-ssis-service.md).  
  
 Por padrão, o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] está configurado para interromper a execução de pacotes quando o serviço estiver parado. Entretanto, o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] não espera que os pacotes parem e alguns pacotes podem continuar executando após o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ser interrompido.  
  
 Se o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] for interrompido, você poderá continuar executando pacotes com o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], o Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)], o Utilitário de Execução de Pacotes e o utilitário de prompt de comando **dtexec** (dtexec.exe). Porém, você não pode monitorar os pacotes em execução.  
  
 Por padrão, o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] executa no contexto da conta de SERVIÇO DE REDE.  
  
 O serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] grava no log de evento do Windows. Você pode exibir eventos de serviço em [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Você também pode exibir eventos de serviço usando Visualizador de Eventos do Windows.  
  
### <a name="to-set-properties-of-integration-services-service-using-the-services-snap-in"></a>Para definir as propriedades do serviço do Integration Services usando o snap-in Serviços  
  
-   [Definir as propriedades do serviço do Integration Services](../../2014/integration-services/set-the-properties-of-the-integration-services-service.md)  
  
### <a name="to-view-service-events-for-integration-services-service"></a>Para exibir eventos para o serviço do Integration Services  
  
-   [Exibir eventos para o serviço do Integration Services](../../2014/integration-services/view-events-for-the-integration-services-service.md)  
  
## <a name="see-also"></a>Consulte também  
 [Serviço Integration Services &#40;Serviço SSIS&#41;](service/integration-services-service-ssis-service.md)   
 [Configurando o Serviço Integration Services &#40;Serviço SSIS#41;](configuring-the-integration-services-service-ssis-service.md)   
 [Assistente de Importação e Exportação do SQL Server](import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)   
 [Utilitário dtexec](packages/dtexec-utility.md)   
 [Execução de projetos e pacotes](packages/run-integration-services-ssis-packages.md)  
  
  
