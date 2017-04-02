---
title: "Executar pacotes do SSIS (Integration Services) | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "pacotes do Integration Services, executando"
  - "pacotes do SSIS, executando"
  - "pacotes [Integration Services], executando"
  - "pacotes do SQL Server Integration Services, executando"
  - "executando pacotes [Integration Services]"
  - "executando pacotes [Integration Services]"
  - "Integration Services, (veja também pacotes do Integration Services)"
ms.assetid: c5fecc23-6f04-4fb2-9a29-01492ea41404
caps.latest.revision: 65
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 61
---
# Executar pacotes do SSIS (Integration Services)
  Para executar um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , você pode usar uma de várias ferramentas dependendo de onde esses pacotes estão armazenados. As ferramentas estão listadas na tabela abaixo.  
  
 Para armazenar um pacote no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , você usa o modelo de implantação do projeto para implantar o projeto no servidor. Para obter mais informações, consulte [Implantar projetos no Servidor do Integration Services](../../integration-services/packages/deploy-projects-to-integration-services-server.md).  
  
 Para armazenar um pacote no repositório de Pacotes SSIS, o banco de dados msdb, ou no sistema de arquivos, você usa o modelo de implantação de pacote. Para obter mais informações, consulte [Implantação de pacote herdado &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md).  
  
|Ferramenta|Pacote que estão armazenados no servidor do Integration Services|Pacotes que estão armazenados no Repositório do Pacotes do SSIS ou no banco de dados msdb|Pacotes que estão armazenados no sistema de arquivos, fora do local que faz parte do Repositório de Pacotes do SSIS|  
|----------|-----------------------------------------------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|  
|**SQL Server Data Tools**|Não|Não<br /><br /> No entanto, você pode adicionar um pacote existente a um projeto do Repositório de Pacotes do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , que inclui o banco de dados msdb. A adição de um pacote existente ao projeto dessa maneira cria uma cópia local do pacote no sistema de arquivos.|Sim|  
|**No SQL Server Management Studio, quando você está conectado a uma instância do Mecanismo de Banco de Dados que hospeda o servidor do Integration Services**<br /><br /> Para obter mais informações, consulte [Caixa de diálogo Executar Pacote](../../integration-services/packages/execute-package-dialog-box.md)|Sim|Não<br /><br /> Porém, você pode importar um pacote no servidor a partir desses locais.|Não<br /><br /> Porém, você pode importar um pacote no servidor a partir do sistema de arquivos.|
|**No SQL Server Management Studio, quando você está conectado a uma instância do Mecanismo de Banco de Dados que hospeda o servidor do Integration Services que é habilitada como Mestre de Expansão**<br /><br /> Para obter mais informações, consulte [Executar pacotes em Expansão](../../integration-services/run-packages-in-integration-services-ssis-scale-out.md)|Sim|Não|Não|
|**O SQL Server Management Studio, quando está conectado ao serviço Integration Services, que gerencia o Repositório de Pacotes SSIS**|Não|Sim|Não<br /><br /> Porém, você pode importar um pacote no Repositório de Pacotes do [!INCLUDE[ssIS](../../includes/ssis-md.md)] por meio do sistema de arquivos.|  
|**dtexec**<br /><br /> Para saber mais, veja [dtexec Utility](../../integration-services/packages/dtexec-utility.md).|Sim|Sim|Sim|  
|**dtexecui**<br /><br /> Para obter mais informações, consulte [Utilitário Executar Pacote &#40;DtExecUI&#41; Referência de interface do usuário](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md)|Não|Sim|Sim|  
|**SQL Server Agent**<br /><br /> Você usa um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para agendar um pacote.<br /><br /> Para obter mais informações, consulte [SQL Server Agent Job para Pacotes](../../integration-services/packages/sql-server-agent-jobs-for-packages.md).|Sim|Sim|Sim|  
|**Procedimento armazenado interno**<br /><br /> Para obter mais informações, consulte [catalog.start_execution &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)|Sim|Não|Não|  
|**API gerenciada com o uso de tipos e membros do ** <xref:Microsoft.SqlServer.Management.IntegrationServices> |Sim|Não|Não|  
|**API gerenciada com o uso de tipos e membros do ** <xref:Microsoft.SqlServer.Dts.Runtime> |Não atualmente|Sim|Sim|  
  
## <a name="execution-and-logging"></a>Execução e registro em log  
 Os pacotes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] podem ser habilitados para registro e você pode capturar informações em tempo de execução nos arquivos de log. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
 Você pode monitorar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que é implantado e executado no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usando relatórios de operação. Os relatórios estão disponíveis no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para saber mais, confira [Reports for the Integration Services Server](../../integration-services/performance/reports-for-the-integration-services-server.md).  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
-   [Agendar um pacote usando o SQL Server Agent](../../integration-services/packages/schedule-a-package-by-using-sql-server-agent.md)  
  
-   [Executar um pacote no SQL Server Data Tools](../../integration-services/packages/run-a-package-in-sql-server-data-tools.md)  
  
-   [Executar um pacote no servidor SSIS usando o SQL Server Management Studio](../../integration-services/packages/run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Consulte também  
 [Utilitário dtexec](../../integration-services/packages/dtexec-utility.md)   
[Iniciar o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)
  
  