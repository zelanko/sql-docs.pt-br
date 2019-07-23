---
title: Executar pacotes do SSIS (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.ispackageexecute.f1
- sql13.ssis.ssms.executepackage.f1
helpviewer_keywords:
- Integration Services packages, running
- SSIS packages, running
- packages [Integration Services], running
- SQL Server Integration Services packages, running
- executing packages [Integration Services]
- running packages [Integration Services]
- Integration Services, (See also Integration Services packages)
ms.assetid: c5fecc23-6f04-4fb2-9a29-01492ea41404
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 5046708ffd705ca937b89a7780e47cd62cdc3f97
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913699"
---
# <a name="run-integration-services-ssis-packages"></a>Executar pacotes do SSIS (Integration Services)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Para executar um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você pode usar uma de várias ferramentas dependendo de onde esses pacotes estão armazenados. As ferramentas estão listadas na tabela abaixo.  

> [!NOTE]
> Este artigo descreve como executar pacotes do SSIS em geral e como executar pacotes localmente. Também é possível executar pacotes do SSIS nas seguintes plataformas:
> - **A nuvem do Microsoft Azure**. Para obter mais informações, consulte [Migrar cargas de trabalho do SQL Server Integration Services por lift-and-shift para a nuvem](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md) e [Run an SSIS package in Azure](../lift-shift/ssis-azure-run-packages.md) (Executar um pacote do SSIS no Azure).
> - **Linux**. Para obter mais informações, consulte [Extrair, transformar e carregar dados no Linux com o SSIS](../../linux/sql-server-linux-migrate-ssis.md).
  
 Para armazenar um pacote no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , você usa o modelo de implantação do projeto para implantar o projeto no servidor. Para obter informações, consulte [Implantar projetos e pacotes do SSIS (Integration Services)](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 Para armazenar um pacote no repositório de Pacotes SSIS, o banco de dados msdb, ou no sistema de arquivos, você usa o modelo de implantação de pacote. Para obter mais informações, consulte [Implantação de pacote herdado &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md).  
  
|Ferramenta|Pacote que estão armazenados no servidor do Integration Services|Pacotes que estão armazenados no Repositório do Pacotes do SSIS ou no banco de dados msdb|Pacotes que estão armazenados no sistema de arquivos, fora do local que faz parte do Repositório de Pacotes do SSIS|  
|----------|-----------------------------------------------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|  
|**SQL Server Data Tools**|Não|Não<br /><br /> No entanto, você pode adicionar um pacote existente a um projeto do Repositório de Pacotes do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , que inclui o banco de dados msdb. A adição de um pacote existente ao projeto dessa maneira cria uma cópia local do pacote no sistema de arquivos.|Sim|  
|**No SQL Server Management Studio, quando você está conectado a uma instância do Mecanismo de Banco de Dados que hospeda o servidor do Integration Services**<br /><br /> Para obter mais informações, consulte [Caixa de diálogo Executar Pacote](#execute_package_dialog)|Sim|Não<br /><br /> Porém, você pode importar um pacote no servidor a partir desses locais.|Não<br /><br /> Porém, você pode importar um pacote no servidor a partir do sistema de arquivos.|
|**No SQL Server Management Studio, quando você está conectado a uma instância do Mecanismo de Banco de Dados que hospeda o servidor do Integration Services que é habilitada como Mestre de Expansão**<br /><br /> Para obter mais informações, consulte [Executar pacotes em Expansão](../../integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md)|Sim|Não|Não|
|**O SQL Server Management Studio, quando está conectado ao serviço Integration Services, que gerencia o Repositório de Pacotes SSIS**|Não|Sim|Não<br /><br /> Porém, você pode importar um pacote no Repositório de Pacotes do [!INCLUDE[ssIS](../../includes/ssis-md.md)] por meio do sistema de arquivos.|  
|**dtexec**<br /><br /> Para saber mais, veja [dtexec Utility](../../integration-services/packages/dtexec-utility.md).|Sim|Sim|Sim|  
|**dtexecui**<br /><br /> Para obter mais informações, consulte [Utilitário Executar Pacote &#40;DtExecUI&#41; Referência de interface do usuário](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md)|Não|Sim|Sim|  
|**SQL Server Agent**<br /><br /> Você usa um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para agendar um pacote.<br /><br /> Para obter mais informações, consulte [SQL Server Agent Job para Pacotes](../../integration-services/packages/sql-server-agent-jobs-for-packages.md).|Sim|Sim|Sim|  
|**Procedimento armazenado interno**<br /><br /> Para obter mais informações, consulte [catalog.start_execution &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)|Sim|Não|Não|  
|**API gerenciada, usando tipos e membros no namespace** <xref:Microsoft.SqlServer.Management.IntegrationServices>|Sim|Não|Não|  
|**API gerenciada, usando tipos e membros no namespace** <xref:Microsoft.SqlServer.Dts.Runtime>|Não atualmente|Sim|Sim|  

## <a name="execution-and-logging"></a>Execução e registro em log  
 Os pacotes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] podem ser habilitados para registro e você pode capturar informações em tempo de execução nos arquivos de log. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
 Você pode monitorar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que é implantado e executado no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usando relatórios de operação. Os relatórios estão disponíveis no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para saber mais, confira [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  
  
## <a name="run-a-package-in-sql-server-data-tools"></a>Executar um pacote no SQL Server Data Tools
  Normalmente, os pacotes são executados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante o desenvolvimento, a depuração e o teste dos pacotes. Quando você executa um pacote no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , o pacote é sempre executado imediatamente.  
  
 Enquanto um pacote estiver sendo executado, o Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] exibe o andamento da execução do pacote na guia **Progresso** . Você pode exibir a hora de início e do fim do pacote e suas tarefas e contêineres, além de informações sobre quaisquer tarefas ou contêineres no pacote em que houve falha. Depois que o pacote concluir a execução, as informações em tempo de execução continuarão disponíveis na guia **Resultados da Execução** . Para obter mais informações, consulte a seção "Relatório de progresso", no tópico [Depuração do fluxo de controle](../../integration-services/troubleshooting/debugging-control-flow.md).  
  
 **Implantação de tempo de design**. Quando um pacote é executado no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], ele é criado e, em seguida, implantado em uma pasta. Antes de executar o pacote, você pode especificar a pasta na qual ele será implantado. Por padrão, se você não especificar uma pasta, a pasta **bin** será usada. Este tipo de implantação é chamado de implantação de tempo de design.  
  
### <a name="to-run-a-package-in-sql-server-data-tools"></a>Para executar um pacote nas Ferramentas de Dados do SQL Server  
  
1.  No Gerenciador de Soluções, se sua solução contiver vários projetos, clique com o botão direito do mouse no projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote e clique em **Definir como Objeto de Inicialização** para definir o projeto de inicialização.  
  
2.  No Gerenciador de Soluções, se o projeto contiver vários pacotes, clique com o botão direito do mouse em um pacote e clique em **Definir como Objeto de Inicialização** para definir o pacote de inicialização.  
  
3.  Para executar um pacote, use um dos seguintes procedimentos:  
  
    -   Abra o pacote que você deseja executar e clique em **Iniciar Depuração** na barra de menus ou pressione F5. Após a execução do pacote, pressione Shift+F5 para retornar ao modo de design.  
  
    -   No Gerenciador de Soluções, clique com o botão direito do mouse no pacote e, em seguida, clique em **Executar Pacote**.  
  
### <a name="to-specify-a-different-folder-for-design-time-deployment"></a>Para especificar uma pasta diferente para implantação em tempo de design  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse na pasta de projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote que você deseja executar e clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Página de Propriedades do \<project name>** , clique em **Compilar**.  
  
3.  Atualize o valor na propriedade OutputPath para especificar a pasta que você deseja usar para a implantação em tempo de design e clique em **OK**.  


## <a name="run-a-package-on-the-ssis-server-using-sql-server-management-studio"></a>Executar um pacote no servidor SSIS usando o SQL Server Management Studio
  Depois de implantar o projeto no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , você pode executar o pacote no servidor.  
  
 Você pode usar relatórios de operações para exibir informações sobre pacotes que foram executados, ou que estão em execução no momento, no servidor. Para saber mais, confira [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  
  
### <a name="to-run-a-package-on-the-server-using-sql-server-management-studio"></a>Para executar um pacote no servidor usando o SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e conecte-se com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém o catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  No Explorador de Objetos, expanda o nó **Catálogo do Integration Services** , expanda o nó **SSISDB** e navegue até o pacote contido no projeto que você implantou.  
  
3.  Clique com o botão direito do mouse no nome do pacote e selecione **Executar**.  
  
4.  Configure a execução de pacote usando as configurações nas guias **Parâmetros**, **Gerenciadores de Conexões**e **Avançado** na caixa de diálogo **Executar Pacote** .  
  
5.  Clique em **OK** para executar o pacote.  
  
     -ou-  
  
     Use procedimentos armazenados para executar o pacote. Clique em **Script** para gerar a instrução Transact-SQL que cria uma instância da execução e inicia uma instância da execução. A instrução inclu uma chamada para os procedimentos armazenados catalog.create_execution, catalog.set_execution_parameter_value e catalog.start_execution. Para obter mais informações sobre esses procedimentos armazenados, consulte [catalog.create_execution &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), [catalog.set_execution_parameter_value &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) e [catalog.start_execution &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md).  

## <a name="execute_package_dialog"></a> Caixa de diálogo Executar Pacote
  Use a caixa de diálogo **Executar Pacote** para executar um pacote armazenado no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pode conter parâmetros com valores armazenados em variáveis de ambiente. Antes de executar esse tipo de pacote, você deve especificar qual ambiente será usado para fornecer os valores de variável de ambiente. Um projeto pode conter vários ambientes, mas só um ambiente pode ser usado para associar valores de variável de ambiente no momento da execução. Se nenhuma variável de ambiente for usada no pacote, nenhum ambiente será necessário.  
  
 O que você deseja fazer?  
  
-   [Abrir a caixa de diálogo Executar Pacote](#open_dialog)  
  
-   [Definir as opções na página Geral](#general)  
  
-   [Definir as opções na guia Parâmetros](#parameters)  
  
-   [Definir as opções na guia de Gerenciadores de Conexões](#connection)  
  
-   [Definir as opções na guia Avançado](#advanced)  
  
-   [Criando scripts para as opções na caixa de diálogo Executar Pacote](#script)  
  
###  <a name="open_dialog"></a> Abrir a caixa de diálogo Executar Pacote  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Você está se conectando à instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o banco de dados SSISDB.  
  
2.  Em Pesquisador de Objetos, expanda a árvore para exibir o nó **Catálogos do Integration Services** .  
  
3.  Expanda o nó **SSISDB** .  
  
4.  Expanda a pasta que contém o pacote que você deseja executar.  
  
5.  Clique com o botão direito do mouse no pacote e clique em **Executar**.  
  
###  <a name="general"></a> Definir as opções na página Geral  
 Selecione **Ambiente** para especificar o ambiente aplicado com o pacote executado.  
  
###  <a name="parameters"></a> Definir as opções na guia Parâmetros  
 Use a guia **Parâmetros** para modificar os valores de parâmetros usados quando o pacote for executado.  
  
###  <a name="connection"></a> Definir as opções na guia de Gerenciadores de Conexões  
 Use a guia Gerenciadores de Conexões para definir as propriedades dos gerenciadores de conexões do pacote.  
  
###  <a name="advanced"></a> Definir as opções na guia Avançado  
 Use a guia Avançado para gerenciar propriedades e outras configurações de pacote.  
  
 **Adicionar**, **Editar**, **Remover**  
 Clique para adicionar, editar ou remover uma propriedade.  
  
 **Nível de log**  
 Selecione o nível de log para a execução do pacote. Para obter mais informações, consulte [catalog.set_execution_parameter_value &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md).  
  
 **Despejar quando ocorrerem erros**  
 Especifique se um arquivo de despejo será criado quando ocorrerem erros durante a execução do pacote. Para obter mais informações, consulte [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
 **Tempo de execução de 32 bits**  
 Especifique se o pacote será executado em um sistema de 32 bits.  
  
###  <a name="script"></a> Criando scripts para as opções na caixa de diálogo Executar Pacote  
 Enquanto estiver na caixa de diálogo **Executar Pacote** , você também poderá usar o botão **Script** na barra de ferramentas para gravar o código [!INCLUDE[tsql](../../includes/tsql-md.md)] . O script gerado chama os procedimentos armazenados [catalog.start_execution &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) com as mesmas opções selecionadas na caixa de diálogo **Executar Pacote**. O script aparece em uma nova janela de script no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  

## <a name="see-also"></a>Consulte Também  
 [Utilitário dtexec](../../integration-services/packages/dtexec-utility.md)   
[Iniciar o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)
  
  
