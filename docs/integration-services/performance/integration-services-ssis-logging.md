---
title: Log do SSIS (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.configuredtslogs.containers.f1
- sql13.dts.designer.configuredtslogs.loggingdetails.f1
- sql13.dts.designer.configuredtslogs.providersandlogs.f1
- SQL13.SSIS.SSMS.ISMANAGECUSTOMIZEDLOGGINGLEVEL.F1
helpviewer_keywords:
- containers [Integration Services], logs
- Windows Event log provider [Integration Services]
- XML File log provider [Integration Services]
- SQL Server Profiler, log provider
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- tasks [Integration Services], logs
- logs [Integration Services], log providers
- Integration Services packages, logs
- log providers [Integration Services]
- packages [Integration Services], logs
- Text File log provider
- SQL Server log provider
ms.assetid: 65e17889-371f-4951-9a7e-9932b2d0dcde
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 603f1d339745e83c3a16ec5b036a8c2f2cc4c980
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="integration-services-ssis-logging"></a>Log do SSIS (Integration Services)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui provedores de log que você pode usar para implementar log em pacotes, contêineres e tarefas. Com o log, você pode capturar informações de tempo de execução sobre um pacote, que o ajudem a auditar e solucionar problemas de um pacote sempre que ele for executado. Por exemplo, um log pode capturar o nome do operador que executou o pacote e a hora em que o pacote começou e foi concluído.  
  
 Você pode configurar o escopo de log que ocorre durante a execução de um pacote no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para saber mais, veja [Enable Logging for Package Execution on the SSIS Server](#server_logging).  
  
 Você também pode incluir o log ao executar um pacote por meio do utilitário de prompt de comando **dtexec** . Para obter mais informações sobre os argumentos do prompt de comando que oferecem suporte para registros, consulte [dtexec Utility](../../integration-services/packages/dtexec-utility.md).  
  
## <a name="configure-logging-in-sql-server-data-tools"></a>Configurar o log no SQL Server Data Tools  
 Logs são associados a pacotes e são configurados no nível de pacote. Cada tarefa ou contêiner em um pacote pode registrar informações em qualquer log de pacote. As tarefas e os contêineres em um pacote podem ser habilitados para registro mesmo se o próprio pacote não for habilitado para isso. Por exemplo, você pode habilitar o registro em uma tarefa Executar SQL sem habilitar o registro no pacote pai. Um pacote, contêiner ou tarefa pode gravar em vários logs. Você só pode habilitar o registro no pacote ou optar por habilitar o registro em qualquer tarefa ou contêiner individual que o pacote inclua.  
  
 Ao adicionar o log a um pacote, você escolhe o provedor de log e o local do log. O provedor de log especifica o formato para obter os dados de log: por exemplo, um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou arquivo de texto.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui os seguintes provedores de log:  
  
-   O provedor de log Arquivo de texto que grava entradas de log em arquivos de texto de ASCII em formato CSV (valores separados por vírgula). A extensão de nome de arquivo padrão deste provedor é .log.  
  
-   O provedor de log [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , que grava rastreamentos que você pode exibir usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler. A extensão de nome de arquivo padrão deste provedor é .trc.  
  
    > [!NOTE]  
    >  Não é possível usar o provedor de log [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] em um pacote executado no modo de 64 bits.  
  
-   O provedor de log [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que grava entradas de log na tabela **sysssislog** em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   O provedor de log de Eventos do Windows, que grava entradas no log de Aplicativo do log de Eventos do Windows no computador local.  
  
-   O provedor de log Arquivo XML, que grava arquivos de log em um arquivo XML. A extensão de nome de arquivo padrão deste provedor é .xml.  
  
 Se você adicionar um provedor de log a um pacote ou configurar o log programaticamente, poderá usar um ProgID ou ClassID para identificar o provedor de log em vez de usar os nomes que o Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] exibe na caixa de diálogo **Configurar Logs de SSIS** .  
  
 A tabela a seguir lista o ProgID e o ClassID dos provedores de log incluídos pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , e o local dos logs nos quais os provedores de log gravam.  
  
|Provedor de log|ProgID|ClassID|Local|  
|------------------|------------|-------------|--------------|  
|Arquivo de texto|DTS.LogProviderTextFile|{0A039101-ACC1-4E06-943F-279948323883}|O gerenciador de conexões de arquivos usado pelo provedor de log especifica o caminho do arquivo de texto.|  
|SQL Server Profiler|DTS.LogProviderSQLProfiler|{E93F6300-AE0C-4916-A7BF-A8D0CE12C77A}|O gerenciador de conexões de arquivos que o provedor de registro usa especifica o caminho usado pelo [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|SQL Server|DTS.LogProviderSQLServer|{94150B25-6AEB-4C0D-996D-D37D1C4FDEDA}|O gerenciador de conexões do OLE DB usado pelo provedor de registro especifica o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém a tabela sysssislog com as entradas do registro.|  
|Log de eventos do Windows|DTS.LogProviderEventLog|{071CC8EB-C343-4CFF-8D58-564B92FCA3CF}|O log do Aplicativo no recurso Visualizador de Eventos do Windows contém as informações de registro do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|Arquivo XML|DTS.LogProviderXMLFile|{440945A4-2A22-4F19-B577-EAF5FDDC5F7A}|O gerenciador de conexões de arquivos usado pelo provedor de registro especifica o caminho do arquivo XML.|  
  
 Você também pode criar provedores de log personalizados. Para saber mais, veja [Creating a Custom Log Provider](../../integration-services/extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md).  
  
 Os provedores de log em um pacote são membros da coleção de provedores de log do pacote. Quando você cria um pacote e implementa o log usando o Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , pode ver uma lista dos membros da coleção nas pastas **Provedor de Log** da guia **Explorador de Pacotes** do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Você pode configurar um provedor de log fornecendo um nome e uma descrição para ele e especificando o gerenciador de conexões que ele usa. O provedor de log [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa um gerenciador de conexões OLE DB. Os provedores de log Arquivo de texto, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]e Arquivo XML usam gerenciadores de conexões de Arquivo. O provedor de log de Eventos do Windows não usa um gerenciador de conexões, pois grava diretamente no log de Eventos do Windows. Para obter mais informações, consulte [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md) e [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md).  
  
### <a name="logging-customization"></a>Personalização do log  
 Para personalizar o registro de um evento ou mensagem personalizada, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece um esquema de informações com logs comuns a ser incluído em entradas de log. O esquema de log do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] define as informações que podem ser registradas. Você pode selecionar elementos do esquema de log para cada entrada de log.  
  
 Um pacote e seus contêineres e tarefas não precisam registrar as mesmas informações; e as tarefas dentro do mesmo pacote ou contêiner podem registrar informações diferentes. Por exemplo, um pacote pode registrar informações do operador quando for iniciado, uma tarefa pode registrar a origem da falha da tarefa e outra tarefa pode registrar informações quando ocorrerem erros. Se um pacote e seus contêineres e tarefas usarem vários logs, as mesmas informações serão gravadas em todos os logs.  
  
 Você pode selecionar um nível de registro que se adapte às suas necessidades especificando os eventos e as informações a serem registrados para cada evento. Você pode achar que alguns eventos fornecem informações mais úteis que outros. Por exemplo, você talvez queira registrar apenas os nomes de computador e operador para o evento **PreExecute** , mas todas as informações disponíveis para o evento **Error** .  
  
 Para evitar que arquivos de log usem grandes quantidades de espaço em disco ou para evitar o registro excessivo, que pode degradar o desempenho, limite o registro selecionando eventos específicos e itens de informações a serem registrados. Por exemplo, você pode configurar um log para capturar só a data e o nome do computador para cada erro.  
  
 No Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , você define as opções de log usando a caixa de diálogo **Configurar Logs de SSIS** .  
  
#### <a name="log-schema"></a>Esquema de log  
 A tabela a seguir descreve os elementos no esquema de log.  
  
|Elemento|Description|  
|-------------|-----------------|  
|Computer|O nome do computador no qual o evento de log ocorreu.|  
|Operador|A identidade do usuário que iniciou o pacote.|  
|SourceName|O nome do contêiner ou tarefa no qual o evento de log ocorreu.|  
|SourceID|O identificador exclusivo do pacote; o contêiner Loop For, Loop Foreach ou Sequência ou a tarefa na qual o evento de log ocorreu.|  
|ExecutionID|O GUID da instância de execução do pacote.<br /><br /> Observação: a execução de um pacote simples pode criar entradas de log com valores diferentes para o elemento ExecutionID. Por exemplo, quando você executa um pacote no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], a fase de validação talvez crie entradas de log com um elemento ExecutionID que corresponde ao [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. No entanto, a fase de execução talvez crie entradas de log com um elemento ExecutionID correspondente a dtshost.exe. Para obter outro exemplo, quando você executa um pacote que contém tarefas Executar Pacote, cada uma dessas tarefas executa um pacote filho. Esses pacotes filho podem criar entradas de log com um elemento ExecutionID diferente do das entradas de log criadas pelo pacote pai.|  
|MessageText|Uma mensagem associada à entrada de log.|  
|DataBytes|Uma matriz de bytes específica para a entrada de log. O significado deste campo varia de acordo com a entrada de log.|  
  
 A tabela a seguir descreve três elementos adicionais no esquema de log que não estão disponíveis na guia **Detalhes** da caixa de diálogo **Configurar Logs de SSIS** .  
  
|Elemento|Description|  
|-------------|-----------------|  
|StartTime|A hora em que o contêiner ou tarefa começa a ser executado.|  
|EndTime|A hora em que a execução do contêiner ou tarefa para.|  
|DataCode|Um valor inteiro opcional que geralmente contém um valor da enumeração <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> que indica o resultado da execução do contêiner ou da tarefa:<br /><br /> 0 - Êxito<br /><br /> 1 - Falha<br /><br /> 2 - Concluído<br /><br /> 3 - Cancelado|  
  
#### <a name="log-entries"></a>Entradas de log  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] dá suporte a entradas de log em eventos predefinidos e fornece entradas de log personalizadas para muitos objetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . A caixa de diálogo **Configurar Logs de SSIS** no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] lista esses eventos e entradas de log personalizadas.  
  
 A tabela a seguir descreve os eventos predefinidos que podem ser habilitados a gravar entradas de log quando eventos de tempo de execução ocorrem. Essas entradas de log se aplicam a executáveis, ao pacote e às tarefas e contêineres que o pacote inclui. O nome da entrada de log é igual ao nome do evento de tempo de execução que foi gerado e fez com que a entrada de log fosse gravada.  
  
|Eventos|Description|  
|------------|-----------------|  
|**OnError**|Grava uma entrada de log quando ocorre um erro.|  
|**OnExecStatusChanged**|Grava uma entrada no log quando uma tarefa (não um contêiner) é suspenso ou retomado durante a depuração.|  
|**OnInformation**|Grava uma entrada de log durante a validação e execução de um executável para relatar informações.|  
|**OnPostExecute**|Grava uma entrada de log imediatamente depois que o executável termina de ser executado.|  
|**OnPostValidate**|Grava uma entrada de log quando a validação do executável termina.|  
|**OnPreExecute**|Grava uma entrada de log imediatamente antes da execução do executável.|  
|**OnPreValidate**|Grava uma entrada de log quando a validação do executável inicia.|  
|**OnProgress**|Grava uma entrada de log quando o progresso mensurável é feito pelo executável.|  
|**OnQueryCancel**|Grava uma entrada de log em qualquer ligação no processamento de tarefa no qual é possível cancelar a execução.|  
|**OnTaskFailed**|Grava uma entrada de log quando uma tarefa falha.|  
|**OnVariableValueChanged**|Grava uma entrada de log quando o valor de uma variável é alterado.|  
|**OnWarning**|Grava uma entrada de log quando ocorre um aviso.|  
|**PipelineComponentTime**|Para cada componente de fluxo de dados, grava uma entrada de log para cada fase de validação e execução. A entrada de log especifica o tempo de processamento de cada fase.|  
|**Diagnostic**<br /><br /> **DiagnosticEx**|Grava uma entrada de log que fornece informações de diagnóstico.<br /><br /> Por exemplo, você pode registrar uma mensagem antes e depois de cada chamada para um provedor de dados externo. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).<br /><br /> Registre o evento **DiagnosticEx** em log quando quiser localizar os nomes de colunas para colunas no fluxo de dados com erros. Esse evento grava um mapa de linhagem de fluxo de dados no log. Em seguida, você pode procurar o nome da coluna nesse mapa de linhagem usando o identificador da coluna capturado por uma saída do erro. Para obter mais informações, consulte [Tratamento de erro em dados](../../integration-services/data-flow/error-handling-in-data.md).<br /><br /> Observe que o evento **DiagnosticEx** não preservar o espaço em branco em sua saída XML, a fim de reduzir o tamanho do log. Para melhorar a legibilidade, copie o log em um editor de XML, no Visual Studio, por exemplo, que ofereça suporte à formatação XML e ao realce de sintaxe.<br /><br /> Observação: se você registrar em log o evento **DiagnosticEx** com o provedor de log do SQL Server, a saída poderá ficar truncada. O campo **message** do provedor de logs do SQL Server é do tipo nvarchar(2048). Para evitar o truncamento, use um provedor de logs diferente quando registrar em log os eventos **DiagnosticEx** .|  
  
 O pacote e muitas tarefas têm entradas de log personalizadas que podem ser habilitadas para registro. Por exemplo, a tarefa Enviar Email fornece a entrada de log personalizada **SendMailTaskBegin** , que registra informações quando a tarefa Enviar Email começa a ser executada, mas antes de a tarefa enviar uma mensagem de email. Para saber mais, veja [Custom Messages for Logging](#custom_messages).  
  
### <a name="differentiating-package-copies"></a>Diferenciando cópias de pacotes  
 Os dados de log incluem o nome e o GUID do pacote ao qual as entradas de log pertencem. Se você criar um novo pacote copiando um pacote existente, o nome e o GUID do pacote existente também serão copiados. Como resultado, você pode ter dois pacotes com o mesmo GUID e nome, dificultando a diferenciação entre eles nos dados de log.  
  
 Para eliminar essa ambiguidade, você deve atualizar o nome e o GUID dos novos pacotes. No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você pode gerar o GUID novamente na propriedade **ID** e atualizar o valor da propriedade **Nome** na janela Propriedades. Você também pode alterar o GUID e o nome programaticamente ou usando o prompt de comando **dtutil** . Para obter mais informações, consulte [Definir as propriedades do pacote](../../integration-services/set-package-properties.md) e [Utilitário dtutil](../../integration-services/dtutil-utility.md).  
  
### <a name="parent-logging-options"></a>Opções de log pai  
 Geralmente, as opções de log de tarefas e os contêineres Loop For, Loop Foreach e Sequência correspondem às opções do pacote ou de um contêiner pai. Nesse caso, você pode configurá-las para herdar as opções de log de seus contêineres pai. Por exemplo, em um contêiner Loop For que inclui uma tarefa Executar SQL, essa tarefa pode usar as opções de log que são definidas no contêiner Loop For. Para usar as opções de log pai, defina a propriedade LoggingMode do contêiner como **UseParentSetting**. É possível definir essa propriedade na janela **Propriedades** do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou através da caixa de diálogo **Configurar Logs de SSIS** no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
### <a name="logging-templates"></a>Modelos de log  
 Na caixa de diálogo **Configurar Logs de SSIS** , você também pode criar e salvar configurações de log usadas com frequência como modelos e depois usar esses modelos em vários pacotes. Isso facilita a aplicação de uma estratégia de log consistente entre vários pacotes e a modificação de definições de log nos pacotes atualizando e depois aplicando os modelos. Os modelos são armazenados em arquivos XML.  
  
 **Para configurar o registro usando a caixa de diálogo Configurar Logs de SSIS**  
  
1.  Habilite o pacote e suas tarefas para registrar. O registro pode ocorrer no nível de pacote, contêiner e tarefa. Você pode especificar logs diferentes para pacotes, contêineres e tarefas.  
  
2.  Selecione um provedor de log e adicione um log ao pacote. Os logs podem ser criados apenas no nível de pacote, e uma tarefa ou contêiner deve usar um dos logs criados para esse pacote. Cada log é associado a um dos seguintes provedores de log: arquivo de texto, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Log de Eventos do Windows ou arquivo XML. Para obter mais informações, consulte [Habilitar o log de pacote no SQL Server Data Tools](#ssdt).  
  
3.  Selecione os eventos e as informações de esquema de log sobre cada evento que você deseja capturar no log. Para obter mais informações, consulte [Configurar o log usando um arquivo de configuração salvo](#saved_config).  
  
### <a name="configuration-of-log-provider"></a>Configuração do provedor de log  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Um provedor de log é criado e configurado como uma etapa na implementação do log em um pacote.  
  
 Depois de criar um provedor de log, você pode exibir e modificar suas propriedades na janela Propriedades do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Para obter mais informações sobre como definir essas propriedades programaticamente, consulte a documentação da classe <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> .  
  
### <a name="logging-for-data-flow-tasks"></a>Registro para tarefas Fluxo de Dados  
 A tarefa Fluxo de Dados fornece muitas entradas de log personalizadas que podem ser usadas para monitorar e ajustar o desempenho. Por exemplo, você pode monitorar os componentes que podem causar vazamentos de memória ou controlar quanto tempo leva para executar um determinado componente. Para obter uma lista dessas entradas de log personalizadas e saída de exemplo de log, consulte [Data Flow Task](../../integration-services/control-flow/data-flow-task.md).  
  
#### <a name="capture-the-names-of-columns-in-which-errors-occur"></a>Capturar os nomes das colunas nas quais ocorrem erros  
 Quando você configura uma saída de erro no fluxo de dados, por padrão a saída de erro fornece apenas o identificador numérico da coluna na qual o erro ocorreu. Para obter mais informações, consulte [Tratamento de erro em dados](../../integration-services/data-flow/error-handling-in-data.md).  
  
 Você pode encontrar nomes de coluna, habilitando o registro em log e selecionando o evento **DiagnosticEx** . Esse evento grava um mapa de linhagem de fluxo de dados no log. Em seguida, você pode procurar o nome da coluna de seu identificador neste mapa de linhagem. Observe que o evento **DiagnosticEx** não preservar o espaço em branco em sua saída XML, a fim de reduzir o tamanho do log. Para melhorar a legibilidade, copie o log em um editor de XML, no Visual Studio, por exemplo, que ofereça suporte à formatação XML e ao realce de sintaxe.  
  
#### <a name="use-the-pipelinecomponenttime-event"></a>Usar o evento PipelineComponentTime  
 Talvez a entrada de log personalizada mais útil seja o evento PipelineComponentTime. Essa entrada de log reporta o número de milissegundos que cada componente do fluxo de dados leva em cada uma das cinco principais etapas de processamento. A tabela a seguir descreve essas etapas de processamento. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Os desenvolvedores reconhecerão essas etapas como os principais métodos de um <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>.  
  
|Etapa|Description|  
|----------|-----------------|  
|Validar|O componente verifica se há valores de propriedade válidos e os parâmetros de configuração.|  
|PreExecute|O componente executa processamento único antes de começar a processar linhas de dados.|  
|PostExecute|O componente executa processamento único depois de processar todas as linhas de dados.|  
|ProcessInput|A transformação ou o componente de destino processa as linhas de dados de entrada recebidas de uma transformação ou origem upstream.|  
|PrimeOutput|O componente de origem ou transformação preenche os buffers de dados a serem passados para uma transformação downstream ou um componente de destino.|  
  
 Quando você habilita o evento PipelineComponentTime, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] registra em log uma mensagem relativa a cada etapa de processamento executada por cada componente. As seguintes entradas de log mostram um subconjunto das mensagens registradas em log pelo pacote de exemplo CalculatedColumns do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] :  
  
 `The component "Calculate LineItemTotalCost" (3522) spent 356 milliseconds in ProcessInput.`  
  
 `The component "Sum Quantity and LineItemTotalCost" (3619) spent 79 milliseconds in ProcessInput.`  
  
 `The component "Calculate Average Cost" (3662) spent 16 milliseconds in ProcessInput.`  
  
 `The component "Sort by ProductID" (3717) spent 125 milliseconds in ProcessInput.`  
  
 `The component "Load Data" (3773) spent 0 milliseconds in ProcessInput.`  
  
 `The component "Extract Data" (3869) spent 688 milliseconds in PrimeOutput filling buffers on output "OLE DB Source Output" (3879).`  
  
 `The component "Sum Quantity and LineItemTotalCost" (3619) spent 141 milliseconds in PrimeOutput filling buffers on output "Aggregate Output 1" (3621).`  
  
 `The component "Sort by ProductID" (3717) spent 16 milliseconds in PrimeOutput filling buffers on output "Sort Output" (3719).`  
  
 Essas entradas de log mostram que a tarefa de fluxo de dados gastou a maior parte do tempo nas seguintes etapas, mostradas aqui em ordem decrescente:  
  
-   A origem de OLE DB denominada "Extrair Dados" gastou 688 ms. carregando dados.  
  
-   A transformação Coluna Derivada denominada "Calculate LineItemTotalCost" gastou 356 ms. executando os cálculos em linhas de entrada.  
  
-   A transformação Agregação denominada "Quantidade de Soma e LineItemTotalCost" gastou no total 220 ms — 141 em PrimeOutput e 79 em ProcessInput — executando cálculos e passando os dados para a próxima transformação.  

## <a name="ssdt"></a> Habilitar o log de pacote no SQL Server Data Tools
  Este procedimento descreve como adicionar registros a um pacote, configurar os registros no nível do pacote e salvar a configuração dos registros em um arquivo XML. Você só pode adicionar os registros no nível do pacote, mas o pacote não precisa executar os registros para habilitar os registros nos contêineres incluídos no pacote.  
  
> [!IMPORTANT]  
>  Se você implantar o projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , o nível de log definido para a execução do pacote substituirá o log do pacote configurado usando o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Por padrão, os contêineres de um pacote usam a mesma configuração de registro que o seu contêiner pai. Para obter informações sobre como definir opções de log para contêineres individuais, consulte [Configurar o registro em log por meio de um arquivo de configuração salvo](#saved_config).  
  
### <a name="to-enable-logging-in-a-package"></a>Para habilitar registros em um pacote  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No menu **SSIS** , clique em **Registrar em Log**.  
  
3.  Selecione um provedor de log na lista **Tipo de provedor** e clique em **Adicionar**.  
  
4.  Na coluna **Configuração**, selecione um gerenciador de conexões ou clique em **\<New connection>** para criar um novo gerenciador de conexões do tipo apropriado para o provedor de logs. Dependendo do provedor selecionado, use um dos seguintes gerenciadores de conexões:  
  
    -   Para arquivos de texto, use um gerenciador de conexões de Arquivo. Para obter mais informações, consulte [Gerenciador de Conexões de Arquivo](../../integration-services/connection-manager/file-connection-manager.md)  
  
    -   Para o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], use um Gerenciador de conexões de arquivo.  
  
    -   Para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use um gerenciador de conexões OLE DB. Para saber mais, veja [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
    -   Para o Log de Eventos de Windows, não faça nada. [!INCLUDE[ssIS](../../includes/ssis-md.md)] cria o log automaticamente.  
  
    -   Para arquivos XML, use um gerenciador de conexões de Arquivo.  
  
5.  Repita as etapas 3 e 4 para cada log a ser usado no pacote.  
  
    > [!NOTE]  
    >  Um pacote pode utilizar mais de um log de cada tipo.  
  
6.  Opcionalmente, marque a caixa de seleção no nível de pacote, selecione os logs a serem atualizados no registro no nível do pacote e clique na guia **Detalhes** .  
  
7.  Na guia **Detalhes** , selecione **Eventos** para registrar todas as entradas de log ou desmarque **Eventos** para selecionar eventos individuais.  
  
8.  Opcionalmente, clique em **Avançado** para especificar quais informações registrar.  
  
    > [!NOTE]  
    >  Por padrão, todas informações são registradas.  
  
9. Na guia **Detalhes** , clique em **Salvar.** A caixa de diálogo **Salvar como** é exibida. Localize a pasta em que deseja salvar as configurações de registro, digite um nome de arquivo para as novas configurações de log e clique em **Salvar**.  
  
10. Clique em **OK**.  
  
11. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  

## <a name="configure_logs"></a> Caixa de diálogo Configurar Logs do SSIS
  Use a caixa de diálogo **Configurar Logs de SSIS** para definir as opções do log para um pacote.  
  
 **O que você deseja fazer?**  
  
1.  [Abrir a caixa de diálogo Configurar Logs de SSIS](#open_dialog)  
  
2.  [Configurar as opções no painel Contêineres](#container)  
  
3.  [Configurar as opções na guia Provedores e Logs](#provider)  
  
4.  [Configurar as opções na guia Detalhes](#detail)  
  
###  <a name="open_dialog"></a> Abrir a caixa de diálogo Configurar Logs de SSIS  
 **Para abrir a caixa de diálogo Configurar Logs de SSIS**  
  
-   No [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em **Log** no menu **SSIS** .  
  
###  <a name="container"></a> Configurar as opções no painel Contêineres  
 Use o painel **Contêineres** da caixa de diálogo **Configurar Logs do SSIS** para habilitar o pacote e seus contêineres para logs.  
  
#### <a name="options"></a>Opções  
 **Contêineres**  
 Marque as caixas de seleção na exibição hierárquica para ativar o pacote e seus contêineres para logs:  
  
-   Se elas não forem marcadas, o contêiner não será ativado para logs. Selecione-as para ativar os logs.  
  
-   Quando esmaecido, o contêiner usa as opções de log pai. Esta opção não está disponível para o pacote.  
  
-   Quando marcado, o contêiner define suas próprias opções de log.  
  
 Se um contêiner estiver esmaecido e você quiser definir as opções de log no contêiner, clique duas vezes em sua caixa de seleção. O primeiro clique apaga a caixa de seleção e o segundo clique a seleciona, permitindo escolher os provedores de log que serão usados e selecionar as informações que serão registradas.  
  
###  <a name="provider"></a> Configurar as opções na guia Provedores e Logs  
 Use a guia **Provedores e Logs** da caixa de diálogo **Configurar Logs do SSIS** para criar e configurar logs para a captura de eventos do tempo de execução.  
  
#### <a name="options"></a>Opções  
 **Tipo de provedor**  
 Selecione um tipo de provedor de log da lista.  
  
 **Adicionar**  
 Adicione um log do tipo especificado à coleção de provedores de log do pacote.  
  
 **Nome**  
 Habilite ou desabilite logs para contêineres ou tarefas selecionadas no painel **Contêineres** da caixa de diálogo **Configurar Logs do SSIS** usando as caixas de seleção. O campo de nome é editável. Use o nome padrão para o provedor ou digite um nome exclusivo.  
  
 **Descrição**  
 O campo de descrição é editável. Clique e modifique a descrição padrão do log.  
  
 **Configuração**  
 Selecione um gerenciador de conexões existente na lista ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões. Dependendo do tipo de provedor de log, você poderá configurar um gerenciador de conexões OLE DB ou um gerenciador de conexões Arquivo. O provedor de log do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Log de Eventos do Windows não requer conexão.  
  
 Tópicos relacionados: [Gerenciador de conexões OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md) , [Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager.md)  
  
 **Delete (excluir)**  
 Selecione um provedor de log e clique em **Excluir**.  
  
###  <a name="detail"></a> Configurar as opções na guia Detalhes  
 Use a guia **Detalhes** da caixa de diálogo **Configurar Logs do SSIS** para especificar eventos e detalhes informativos a serem habilitados para log. As informações selecionadas se aplicam a todos os provedores de logs no pacote. Por exemplo, você não pode gravar determinadas informações na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e informações diferentes em um arquivo de texto.  
  
#### <a name="options"></a>Opções  
 **Eventos**  
 Ative ou desative eventos para log.  
  
 **Descrição**  
 Exiba uma descrição do evento.  
  
 **Avançado**  
 Marque ou desmarque os eventos para log e marque ou desmarque informações que serão usadas no log de cada evento. Clique em **Básico** para ocultar todos os detalhes de log, exceto a lista de eventos. As informações a seguir estão disponíveis para log:  
  
|Valor|Description|  
|-----------|-----------------|  
|**Computer**|O nome do computador no qual o evento de log ocorreu.|  
|**Operador**|O nome de usuário da pessoa que iniciou o pacote.|  
|**SourceName**|O nome do pacote, contêiner ou tarefa no qual o evento de log ocorreu.|  
|**SourceID**|O Identificador Global Exclusivo (GUID) do pacote, contêiner ou tarefa no qual o evento de log ocorreu.|  
|**ExecutionID**|O Identificador Global Exclusivo da instância de execução do pacote.|  
|**MessageText**|Uma mensagem associada à entrada de log.|  
|**DataBytes**|Reservado para uso futuro.|  
  
 **Básico**  
 Marque ou desmarque os eventos para log. Esta opção oculta os detalhes de log, exceto a lista de eventos. Se você selecionar um evento, por padrão, todos os detalhes de log serão selecionados para esse evento. Clique em **Avançado** para mostrar todos os detalhes de log.  
  
 **Carregar**  
 Especifique um arquivo XML existente para ser usado como modelo para definir as opções de log.  
  
 **Salvar**  
 Salve os detalhes de configuração como um modelo para um arquivo XML.  

## <a name="saved_config"></a> Configurar o log usando um arquivo de configuração salvo
  Este procedimento descreve como configurar o registro em log de novos contêineres em um pacote carregando um arquivo de configuração de registro em log salvo anteriormente.  
  
 Por padrão, todos os contêineres em um pacote usam a mesma configuração de registro que o seu contêiner pai. Por exemplo, as tarefas em um Loop Foreach usam a mesma configuração de registro que o Loop Foreach.  
  
### <a name="to-configure-logging-for-a-container"></a>Para configurar o registro de um contêiner  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No menu **SSIS** , clique em **Registrar em Log**.  
  
3.  Expanda a exibição de árvore do pacote e selecione o contêiner a ser configurado.  
  
4.  Na guia **Provedores e Logs** , selecione os logs a serem usados no contêiner.  
  
    > [!NOTE]  
    >  Você só pode criar logs no nível de pacote. Para obter mais informações, consulte [Habilitar o log de pacote no SQL Server Data Tools](#ssdt).  
  
5.  Clique na guia **Detalhes** e clique em **Carregar**.  
  
6.  Localize o arquivo de configuração de registro que você deseja usar e clique em **Abrir**.  
  
7.  Opcionalmente, selecione uma entrada de log diferente para o log marcando sua caixa de seleção na coluna **Eventos** . Clique em **Avançado** para selecionar o tipo de informações a serem registradas nesta entrada.  
  
    > [!NOTE]  
    >  O novo contêiner pode incluir entradas de log adicionais que não estão disponíveis para o contêiner usado originalmente para criar a configuração de registro. Essas entradas de log adicionais devem ser selecionadas manualmente se você quiser que elas sejam registradas.  
  
8.  Para salvar a versão atualizada da configuração de registro, clique em **Salvar**.  
  
9. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  

## <a name="server_logging"></a> Enable Logging for Package Execution on the SSIS Server
  Este tópico descreve como definir ou alterar o nível de registro em log de um pacote quando você executa um pacote implantado no servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . O nível de registro em log que você define ao executar o pacote anula o registro em log do pacote configurado no momento do design no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Consulte [Habilitar o log de pacote no SQL Server Data Tools](#ssdt) para obter mais informações.  
  
 Nas **Propriedades do Servidor**do SQL Server, na propriedade **Nível de registro em log do servidor** , você pode selecionar um nível de registro em log padrão para todo o servidor. Você pode escolher entre um dos níveis de registro em log internos descritos neste tópico, ou pode escolher um nível de registro em log personalizado existente. O nível de registro em log selecionado se aplica por padrão a todos os pacotes implantados no Catálogo do SSIS. Ele também se aplica por padrão a uma etapa de trabalho do SQL Agent, que executa um pacote do SSIS.  
  
 Você também pode especificar o nível de registro em log de um pacote individual usando um dos métodos a seguir. Este tópico aborda o primeiro método.  
  
-   Configuração de uma instância de uma execução de pacote usando a caixa de diálogo Executar Pacote  
  
-   Configuração de parâmetros para uma instância de uma execução usando o [catalog.set_execution_parameter_value &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
  
-   Configuração de um trabalho do SQL Server Agent para uma execução de pacote usando a caixa de diálogo Nova Etapa de Trabalho.  
  
### <a name="set-the-logging-level-for-a-package-by-using-the-execute-package-dialog-box"></a>Definir o nível de registro em log de um pacote usando a caixa de diálogo Executar Pacote  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], navegue até o pacote no Pesquisador de Objetos.  
  
2.  Clique com o botão direito do mouse no pacote e selecione **Executar**.  
  
3.  Selecione a guia **Avançado** na caixa de diálogo **Executar Pacote** .  
  
4.  Em **Nível de log**, selecione o nível de log. Este tópico contém uma descrição dos valores disponíveis.  
  
5.  Conclua qualquer outra configuração de pacote e clique em **OK** para executar o pacote.  
  
### <a name="select-a-logging-level"></a>Selecionar um nível de registro em log.  
 Os níveis de registro em log internos a seguir estão disponíveis. Você também pode selecionar um nível de registro em log existente personalizado. Este tópico contém uma descrição dos níveis de registro em log personalizados.  
  
|Nível de log|Description|  
|-------------------|-----------------|  
|Nenhum|O log está desativado. Apenas o status da execução do pacote é registrado em log.|  
|Basic|Todos os eventos são registrados em log, menos personalizados e de diagnóstico. Este é o valor padrão.|  
|RuntimeLineage|Coleta os dados necessários para rastrear as informações de linhagem no fluxo de dados. Você pode analisar essas informações de linhagem para mapear o relacionamento de linhagem entre tarefas. ISVs e desenvolvedores podem compilar ferramentas de mapeamento de linhagem personalizadas com essas informações.|  
|Desempenho|Apenas estatísticas de desempenho e eventos OnError e OnWarning são registrados em log.<br /><br /> O relatório **Desempenho de Execução** mostra a hora ativa e o tempo total para os componentes de fluxo de dados do pacote. Estas informações estão disponíveis quando o nível de log da última execução do pacote foi definido como **desempenho** ou **detalhado**. Para saber mais, confira [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).<br /><br /> A exibição [catalog.execution_component_phases](../../integration-services/system-views/catalog-execution-component-phases.md) mostra as horas de início e de término para os componentes de fluxo de dados, para cada fase de uma execução. Esta exibição mostra essas informações para esses componentes apenas quando o nível de log da execução do pacote é definido como **Desempenho** ou **Detalhado**.|  
|Detalhado|Todos os eventos são registrados em log, inclusive eventos personalizados e de diagnóstico.<br /><br /> Eventos personalizados incluem os eventos registrados por tarefas do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para saber mais sobre eventos personalizados, confira [Custom Messages for Logging](#custom_messages).<br /><br /> Um exemplo de um evento de diagnóstico é o evento **DiagnosticEx** . Sempre que uma tarefa Executar Pacote executa um pacote filho, esse evento captura os valores de parâmetro passados para os pacotes filho.<br /><br /> O evento **DiagnosticEx** também ajuda você a obter os nomes das colunas nas quais ocorrem erros no nível da linha. Esse evento grava um mapa de linhagem de fluxo de dados no log. Em seguida, você pode procurar o nome da coluna nesse mapa de linhagem usando o identificador da coluna capturado por uma saída do erro.  Para obter mais informações, consulte [Tratamento de erro em dados](../../integration-services/data-flow/error-handling-in-data.md).<br /><br /> O valor da coluna de mensagem para **DiagnosticEx** é texto XML. Para exibir o texto da mensagem para uma execução de pacote, consulte a exibição [catalog.operation_messages &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md). Observe que o evento **DiagnosticEx** não preservar o espaço em branco em sua saída XML, a fim de reduzir o tamanho do log. Para melhorar a legibilidade, copie o log em um editor de XML, no Visual Studio, por exemplo, que ofereça suporte à formatação XML e ao realce de sintaxe.<br /><br /> A exibição [catalog.execution_data_statistics](../../integration-services/system-views/catalog-execution-data-statistics.md) mostra uma linha cada vez que um componente de fluxo de dados envia dados a um componente downstream, para determinada execução do pacote. O nível de log deve ser definido como **Detalhado** para capturar essas informações na exibição.|  
  
### <a name="create-and-manage-customized-logging-levels-by-using-the-customized-logging-level-management-dialog-box"></a>Criar e gerenciar níveis de registro em log personalizados usando a caixa de diálogo Gerenciamento de Nível de Registro em Log Personalizado  
 Você pode criar níveis de registro em log personalizados que coletam somente as estatísticas e eventos que você quiser. Opcionalmente, você também pode capturar o contexto de eventos, que inclui valores de variáveis, cadeias de conexão e propriedades do componente. Quando você executa um pacote, é possível selecionar um nível de registro em log personalizado sempre que você puder selecionar um nível de registro em log interno.  
  
> [!TIP]  
>  Para capturar os valores das variáveis do pacote, a propriedade **IncludeInDebugDump** das variáveis deve ser definida como **True**.  
  
1.  Para criar e gerenciar níveis de registro em log personalizados, no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse no banco de dados SSISDB e selecione **Nível de Registro em Log Personalizado** para abrir a caixa de diálogo **Gerenciamento de Nível de Registro em Log Personalizado** . A lista **Níveis de Registro em Log Personalizados** contém todos os níveis de registro em log personalizados existentes.  
  
2.  Para **criar** um novo nível de registro em log personalizado, clique em **Criar**e forneça um nome e uma descrição. Nas guias **Estatísticas** e **Eventos** , selecione as estatísticas e eventos que você deseja coletar. Na guia **Eventos** , selecione opcionalmente **Incluir Contexto** para eventos individuais. Em seguida, clique em **Salvar**.  
  
3.  Para **atualizar** um nível de registro em log personalizado, selecione-o na lista, reconfigure-o e clique em **Salvar**.  
  
4.  Para **excluir** um nível de registro em log personalizado, selecione-o na lista e clique em **Excluir**.  
  
 **Permissões para níveis de registro em log personalizados.**  
  
-   Todos os usuários do banco de dados SSISDB podem ver os níveis de registro em log personalizados e selecionar um nível de registro em log personalizado ao executar pacotes.  
  
-   Somente os usuários na função ssis_admin ou sysadmin podem criar, atualizar ou excluir níveis de registro em log personalizados.  

## <a name="custom_messages"></a> Custom Messages for Logging
O SQL Server Integration Services fornece um conjunto avançado de eventos personalizados para gravação de entradas de log para pacotes e diversas tarefas. Você pode usar essas entradas para salvar informações detalhadas sobre progresso de execução, resultados e problemas registrando eventos predefinidos ou mensagens definidas pelo usuário para análise posterior. Por exemplo, você pode registrar quando uma inserção em massa é iniciada ou finalizada para identificar problemas de desempenho na execução do pacote.  
  
 As entradas de log personalizadas são um conjunto de entradas diferente do conjunto de eventos de log padrão, disponível para pacotes e todos os contêineres e tarefas. As entradas de log personalizadas são elaboradas para capturar informações úteis sobre uma tarefa específica em um pacote. Por exemplo, uma das entradas de log personalizadas da tarefa Executar SQL registra a instrução SQL executada pela tarefa no log.  
  
 Todas as entradas de log incluem informações de data e hora, inclusive as entradas de log que são gravadas automaticamente quando um pacote é iniciado ou finalizado. Diversos tipos de eventos de log gravam várias entradas no log. Isso acontece normalmente quando o evento tem fases diferentes. Por exemplo, o evento de log **ExecuteSQLExecutingQuery** grava três entradas: uma entrada depois que a tarefa adquire uma conexão com o banco de dados, outra depois que a tarefa começa a preparar a instrução SQL e uma depois que a execução da instrução SQL foi concluída.  
  
 Os objetos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a seguir têm entradas de log personalizadas:  
  
 [Pacote](#Package)  
  
 [Tarefa Inserção em Massa](#BulkInsert)  
  
 [Tarefa de Fluxo de Dados](#DataFlow)  
  
 [Tarefa Executar DTS 2000](#ExecuteDTS200)  
  
 [Tarefa Executar Processo](#ExecuteProcess)  
  
 [Tarefa Executar SQL](#ExecuteSQL)  
  
 [Tarefa Sistema de Arquivos](#FileSystem)  
  
 [Tarefa FTP](#FTP)  
  
 [Tarefa Fila de Mensagens](#MessageQueue)  
  
 [Tarefa Script](#Script)  
  
 [Tarefa Enviar Email](#SendMail)  
  
 [Tarefa Transferir Banco de Dados](#TransferDatabase)  
  
 [Tarefa Transferir Mensagens de Erro](#TransferErrorMessages)  
  
 [Tarefa Transferir Trabalhos](#TransferJobs)  
  
 [Tarefa Transferir Logons](#TransferLogins)  
  
 [Tarefa Transferir Procedimentos Armazenados Mestres](#TransferMasterStoredProcedures)  
  
 [Tarefa Transferir Objetos do SQL Server](#TransferSQLServerObjects)  
  
 [Tarefa Serviços Web](#WebServices)  
  
 [Tarefa Leitor de Dados do WMI](#WMIDataReader)  
  
 [Tarefa Detector de Eventos do WMI](#WMIEventWatcher)  
  
 [XML Task](#XML)  
  
### <a name="log-entries"></a>Entradas de log  
  
####  <a name="Package"></a> Pacote  
 A tabela a seguir relaciona as entradas de log personalizadas para pacotes.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**PackageStart**|Indica que o pacote começou a ser executado. Esta entrada de log é gravada no log automaticamente. Não é possível excluí-la.|  
|**PackageEnd**|Indica que o pacote foi concluído. Esta entrada de log é gravada no log automaticamente. Não é possível excluí-la.|  
|**Diagnostic**|Fornece informações sobre a configuração do sistema que afeta a execução de pacotes como os executáveis numéricos que podem ser executados simultaneamente.<br /><br /> A entrada de log **Diagnóstico** também inclui entradas anteriores e posteriores a chamadas para provedores de dados externos.|  
  
####  <a name="BulkInsert"></a> Tarefa Inserção em Massa  
 A seguinte tabela relaciona as entradas de log personalizadas para a tarefa inserção em massa .  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**DTSBulkInsertTaskBegin**|Indica que a inserção em massa iniciou.|  
|**DTSBulkInsertTaskEnd**|Indica que a inserção em massa foi concluída.|  
|**DTSBulkInsertTaskInfos**|Fornece informações descritivas sobre a tarefa.|  
  
####  <a name="DataFlow"></a> Tarefa de Fluxo de Dados  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa de Fluxo de Dados.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**BufferSizeTuning**|Indica que a tarefa de Fluxo de Dados alterou o tamanho do buffer. A entrada de log descreve os motivos da mudança de tamanho e relaciona o novo tamanho do buffer temporário.|  
|**OnPipelinePostEndOfRowset**|Indica que um componente recebeu o sinal de final do conjunto de linhas, definido pela última chamada do método **ProcessInput** . Uma entrada é gravada para cada componente no fluxo de dados que processa a entrada. A entrada contém o nome do componente.|  
|**OnPipelinePostPrimeOutput**|Indica que o componente completou sua última chamada para o método **PrimeOutput** . Dependendo do fluxo de dados, várias entradas de log podem ser gravadas. Se o componente for uma fonte, isto significará que o componente tem linhas de processamento concluídas.|  
|**OnPipelinePreEndOfRowset**|Indica que um componente está prestes a receber o sinal de final do conjunto de linhas, definido pela última chamada do método **ProcessInput** . Uma entrada é gravada para cada componente no fluxo de dados que processa a entrada. A entrada contém o nome do componente.|  
|**OnPipelinePrePrimeOutput**|Indica que o componente está prestes a receber sua chamada do método **PrimeOutput** . Dependendo do fluxo de dados, várias entradas de log podem ser gravadas.|  
|**OnPipelineRowsSent**|Informa o número de linhas fornecido a uma entrada de componente por uma chamada para o método **ProcessInput** . A entrada de log inclui o nome do componente.|  
|**PipelineBufferLeak**|Fornece informações sobre qualquer componente que manteve buffers ativos depois que o gerenciador de buffers for desativado. Isso significa que os recursos de buffers não foram liberados e pode haver vazamentos de memória. A entrada de log fornece o nome do componente e a ID do buffer.|  
|**PipelineExecutionPlan**|Informa o plano de execução do fluxo de dados. Fornece informações sobre como os buffers serão enviados a componentes. Essas informações, em combinação com a entrada de PipelineExecutionTrees, descrevem o que está acontecendo na tarefa.|  
|**PipelineExecutionTrees**|Informa as árvores de execução sobre o layout do fluxo de dados. O agendador do mecanismo de fluxo de dados usa as árvores para compilar o plano de execução do fluxo de dados.|  
|**PipelineInitialization**|Fornece informações de inicialização sobre a tarefa. Essas informações incluem os diretórios para armazenamento temporário de dados de BLOB, o tamanho do buffer padrão e o número de linhas em um buffer. Dependendo da configuração da tarefa de Fluxo de Dados, várias entradas de log podem ser gravadas.|  
  
####  <a name="ExecuteDTS200"></a> Tarefa Executar DTS 2000  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Executar DTS 2000.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**ExecuteDTS80PackageTaskBegin**|Indica que a tarefa começou a ser executada em um pacote DTS 2000.|  
|**ExecuteDTS80PackageTaskEnd**|Indica que a tarefa foi concluída.<br /><br /> Observação: o pacote DTS 2000 pode continuar a ser executado após a conclusão da tarefa.|  
|**ExecuteDTS80PackageTaskTaskInfo**|Fornece informações descritivas sobre a tarefa.|  
|**ExecuteDTS80PackageTaskTaskResult**|Informa o resultado de execução do pacote DTS 2000 executado pela tarefa.|  
  
####  <a name="ExecuteProcess"></a> Tarefa Executar Processo  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Executar Processo.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**ExecuteProcessExecutingProcess**|Fornece informações sobre o processo do executável que a tarefa está configurada para executar.<br /><br /> São gravadas duas entradas de log. Uma contém informações sobre o nome e o local do executável que a tarefa executa e o outro registra a saída do executável.|  
|**ExecuteProcessVariableRouting**|Fornece informações sobre quais variáveis são encaminhadas para a entrada e as saídas do executável. As entradas de log são gravadas em stdin (a entrada), stdout (a saída) e stderr (a saída do erro).|  
  
####  <a name="ExecuteSQL"></a> Tarefa Executar SQL  
 A tabela a seguir descreve a entrada de log personalizada da tarefa Executar SQL.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**ExecuteSQLExecutingQuery**|Fornece informações sobre as fases de execução da instrução SQL. As entradas de log são gravadas quando a tarefa adquire conexão com o banco de dados, quando a tarefa começa a preparar a instrução SQL e depois que a execução da instrução SQL é concluída. A entrada de log da fase de preparação inclui a instrução SQL usada pela tarefa.|  
  
####  <a name="FileSystem"></a> Tarefa Sistema de Arquivos  
 A tabela a seguir descreve a entrada de log personalizada da tarefa Sistema de Arquivos.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**FileSystemOperation**|Informa a operação executada pela tarefa. A entrada de log é gravada quando a operação de sistema de arquivos é iniciada e inclui informações sobre a origem e o destino.|  
  
####  <a name="FTP"></a> Tarefa FTP  
 A tabela a seguir relaciona as entradas de log personalizadas da tarefa FTP.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**FTPConnectingToServer**|Indica que a tarefa iniciou uma conexão com o servidor FTP.|  
|**FTPOperation**|Informa o início e o tipo de operação de FTP que a tarefa executa.|  
  
####  <a name="MessageQueue"></a> Tarefa Fila de Mensagens  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Fila de Mensagens.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**MSMQAfterOpen**|Indica que a tarefa finalizou a abertura da fila de mensagens.|  
|**MSMQBeforeOpen**|Indica que a tarefa começou a abrir a fila de mensagens.|  
|**MSMQBeginReceive**|Indica que a tarefa começou a receber uma mensagem.|  
|**MSMQBeginSend**|Indica que a tarefa começou a enviar uma mensagem.|  
|**MSMQEndReceive**|Indica que a tarefa terminou de receber uma mensagem.|  
|**MSMQEndSend**|Indica que a tarefa terminou de enviar uma mensagem|  
|**MSMQTaskInfo**|Fornece informações descritivas sobre a tarefa.|  
|**MSMQTaskTimeOut**|Indica que o tempo limite da tarefa foi esgotado.|  
  
####  <a name="Script"></a> Tarefa Script  
 A tabela a seguir descreve a entrada de log personalizada da tarefa Script.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**ScriptTaskLogEntry**|Informa os resultados da implementação do registro em log no script. Uma entrada de log é gravada para cada chamada ao método **Log** do objeto **Dts** . A entrada é gravada quando o código é executado. Para obter mais informações, consulte [Registro em log na Tarefa Script](../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md).|  
  
####  <a name="SendMail"></a> Tarefa Enviar Email  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Enviar Email.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**SendMailTaskBegin**|Indica que a tarefa começou a enviar uma mensagem de email.|  
|**SendMailTaskEnd**|Indica que a tarefa terminou de enviar uma mensagem de email.|  
|**SendMailTaskInfo**|Fornece informações descritivas sobre a tarefa.|  
  
####  <a name="TransferDatabase"></a> Tarefa Transferir Banco de Dados  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Transferir Banco de Dados.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**SourceDB**|Especifica o banco de dados que a tarefa copiou.|  
|**SourceSQLServer**|Especifica o computador a partir do qual o banco de dados foi copiado.|  
  
####  <a name="TransferErrorMessages"></a> Tarefa Transferir Mensagens de Erro  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Transferir Mensagens de Erro.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**TransferErrorMessagesTaskFinishedTransferringObjects**|Indica que a tarefa terminou de transferir mensagens de erro.|  
|**TransferErrorMessagesTaskStartTransferringObjects**|Indica que a tarefa começou a transferir as mensagens de erro.|  
  
####  <a name="TransferJobs"></a> Tarefa Transferir Trabalhos  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Transferir Trabalhos.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**TransferJobsTaskFinishedTransferringObjects**|Indica que a tarefa terminou a transferência dos trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|**TransferJobsTaskStartTransferringObjects**|Indica que a tarefa começou a transferência dos trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
  
####  <a name="TransferLogins"></a> Tarefa Transferir Logons  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Transferir Logons.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**TransferLoginsTaskFinishedTransferringObjects**|Indica que a tarefa terminou a transferência dos logons.|  
|**TransferLoginsTaskStartTransferringObjects**|Indica que a tarefa começou a transferência dos logons.|  
  
####  <a name="TransferMasterStoredProcedures"></a> Tarefa Transferir Procedimentos Armazenados Mestres  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Transferir Procedimentos Armazenados Mestres.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**TransferStoredProceduresTaskFinishedTransferringObjects**|Indica que a tarefa terminou de transferir procedimentos armazenados definidos pelo usuário armazenados no banco de dados **mestre** .|  
|**TransferStoredProceduresTaskStartTransferringObjects**|Indica que a tarefa começou a transferir procedimentos armazenados definidos pelo usuário armazenados no banco de dados **mestre** .|  
  
####  <a name="TransferSQLServerObjects"></a> Tarefa Transferir Objetos do SQL Server  
 A tabela a seguir relaciona as entradas de log personalizadas da tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**TransferSqlServerObjectsTaskFinishedTransferringObjects**|Indica que a tarefa terminou a transferência dos objetos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**TransferSqlServerObjectsTaskStartTransferringObjects**|Indica que a tarefa começou a transferência dos objetos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
  
####  <a name="WebServices"></a> Tarefa Serviços Web  
 A tabela a seguir relaciona as entradas de log personalizadas que podem ser habilitadas para a tarefa Serviços Web.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**WSTaskBegin**|A tarefa começou a acessar um serviço Web.|  
|**WSTaskEnd**|A tarefa completou um método de serviço Web.|  
|**WSTaskInfo**|Informações descritivas sobre a tarefa.|  
  
####  <a name="WMIDataReader"></a> Tarefa Leitor de Dados do WMI  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Leitor de Dados do WMI.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**WMIDataReaderGettingWMIData**|Indica que a tarefa começou a ser ler os dados do WMI.|  
|**WMIDataReaderOperation**|Informa a consulta WQL executada pela tarefa.|  
  
####  <a name="WMIEventWatcher"></a> Tarefa Detector de Eventos do WMI  
 A tabela a seguir relaciona as entradas de registro personalizadas da tarefa Detector de Eventos do WMI.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**WMIEventWatcherEventOccurred**|Mostra que o evento ocorrido era o que a tarefa estava monitorando.|  
|**WMIEventWatcherTimedout**|Indica que o tempo limite da tarefa foi esgotado.|  
|**WMIEventWatcherWatchingForWMIEvents**|Indica que a tarefa começou a executar a consulta WQL. A entrada inclui a consulta.|  
  
####  <a name="XML"></a> XML Task  
 A tabela a seguir descreve a entrada de log personalizada da tarefa XML.  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**XMLOperation**|Fornece informações sobre a operação executada pela tarefa|  

## <a name="related-tasks"></a>Related Tasks  
 A lista a seguir contém links para tópicos que mostram como executar tarefas relacionadas ao recurso de log.  
  
-   [Eventos registrados em log por um pacote do Integration Services](../../integration-services/performance/events-logged-by-an-integration-services-package.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Ferramenta DTLoggedExec para log completo e detalhado (Projeto CodePlex)](http://go.microsoft.com/fwlink/?LinkId=150579)  
