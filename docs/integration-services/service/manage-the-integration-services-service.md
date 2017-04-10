---
title: "Gerenciar o servi&#231;o Integration Services | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Serviço do Integration Services, configurando"
  - "serviços [Integration Services], configurando"
ms.assetid: 45554117-a0df-4830-b41c-5ebb33b764a5
caps.latest.revision: 63
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 63
---
# Gerenciar o servi&#231;o Integration Services
    
> **IMPORTANTE:** Esse tópico discute o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , um serviço do Windows para o gerenciamento de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] dá suporte ao serviço para compatibilidade de versões anteriores com versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], você pode gerenciar objetos como pacotes no servidor do Integration Services.  
  
 Quando você instala o componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] também é instalado. Por padrão, o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é iniciado e o tipo de inicialização do serviço é definido como automático. Porém, você também precisa instalar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para usar o serviço para gerenciar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em execução e armazenados.  
  
> **OBSERVAÇÃO:** para se conectar diretamente a uma instância do Serviço Integration Services herdado, você precisa usar a versão do SSMS (SQL Server Management Studio) alinhada com a versão do SQL Server na qual o Serviço Integration Services está em execução. Por exemplo, para se conectar ao Serviço Integration Services herdados executados em uma instância do SQL Server 2016, você precisa usar a versão do SSMS liberada para o SQL Server 2016. [Baixe o SSMS (SQL Server Management Studio)](https://msdn.microsoft.com/library/mt238290.aspx).
>
>   Na caixa de diálogo **Conectar ao Servidor** do SSMS, não é possível inserir o nome de um servidor no qual uma versão anterior do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] esteja em execução. No entanto, para gerenciar pacotes armazenados em um servidor remoto, não é necessário se conectar à instância do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nesse servidor remoto. Em vez disso, edite o arquivo de configuração do serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de forma que o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] exiba os pacotes armazenados no servidor remoto. Para obter mais informações, consulte [Configurando o serviço Integration Services &#40; Serviço SSIS&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md).  
  
 Você pode instalar apenas uma única instância do serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um computador. O serviço não é específico de uma determinada instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Você se conecta ao serviço usando o nome do computador no qual ele está sendo executado.  
  
 Você pode gerenciar o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usando um dos seguintes snap-ins do MMC (Console de Gerenciamento Microsoft): SQL Server Configuration Manager ou Serviços. Antes que você possa gerenciar pacotes em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], é preciso se certificar que o serviço foi iniciado.  
  
 Por padrão, o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é configurado para gerenciar pacotes no banco de dados msdb de uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que é instalada ao mesmo tempo em que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Se uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] não for instalada ao mesmo tempo, o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] será configurado para gerenciar pacotes no banco de dados msdb de uma instância local padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Para gerenciar pacotes que estão armazenados em uma instância nomeada ou remota do [!INCLUDE[ssDE](../../includes/ssde-md.md)], ou em várias instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)], é preciso modificar o arquivo de configuração para o serviço. Para obter mais informações, consulte [Configurando o serviço Integration Services &#40; Serviço SSIS&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md).  
  
 Por padrão, o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] está configurado para interromper a execução de pacotes quando o serviço estiver parado. Entretanto, o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não espera que os pacotes parem e alguns pacotes podem continuar executando após o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ser interrompido.  
  
 Se o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] for interrompido, você poderá continuar executando pacotes com o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)], o Utilitário de Execução de Pacotes e o utilitário de prompt de comando **dtexec** (dtexec.exe). Porém, você não pode monitorar os pacotes em execução.  
  
 Por padrão, o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] executa no contexto da conta de SERVIÇO DE REDE.  
  
 O serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] grava no log de evento do Windows. Você pode exibir eventos de serviço em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você também pode exibir eventos de serviço usando Visualizador de Eventos do Windows.  
  
### Para definir as propriedades do serviço do Integration Services usando o snap-in Serviços  
  
-   [Definir as propriedades do serviço do Integration Services](../../integration-services/service/set-the-properties-of-the-integration-services-service.md)  
  
### Para exibir eventos para o serviço do Integration Services  
  
-   [Exibir eventos para o serviço do Integration Services](../../integration-services/service/view-events-for-the-integration-services-service.md)  
  
## Consulte também  
 [Serviço Integration Services &#40;Serviço SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md)   
 [Configurando o Serviço Integration Services &#40;Serviço SSIS#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md)   
 [Assistente de Importação e Exportação do SQL Server](../Topic/SQL%20Server%20Import%20and%20Export%20Wizard.md)   
 [Utilitário dtexec](../../integration-services/packages/dtexec-utility.md)   
 [Execução de projetos e pacotes](https://msdn.microsoft.com/library/ms141708(v=sql.130).aspx)  
  
  