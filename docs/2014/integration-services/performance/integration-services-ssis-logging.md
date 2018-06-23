---
title: Log do SSIS (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 64
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e9611d78d6b94038511b29577aca5aaefb36366d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117459"
---
# <a name="integration-services-ssis-logging"></a>Log do SSIS (Integration Services)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui provedores de log que você pode usar para implementar log em pacotes, contêineres e tarefas. Com o log, você pode capturar informações de tempo de execução sobre um pacote, que o ajudem a auditar e solucionar problemas de um pacote sempre que ele for executado. Por exemplo, um log pode capturar o nome do operador que executou o pacote e a hora em que o pacote começou e foi concluído.  
  
 Você pode configurar o escopo de log que ocorre durante a execução de um pacote no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para saber mais, veja [Enable Logging for Package Execution on the SSIS Server](../enable-logging-for-package-execution-on-the-ssis-server.md).  
  
 Você também pode incluir o log ao executar um pacote por meio do utilitário de prompt de comando **dtexec** . Para obter mais informações sobre os argumentos do prompt de comando que oferecem suporte para registros, consulte [dtexec Utility](../packages/dtexec-utility.md).  
  
## <a name="configure-logging-in-sql-server-data-tools"></a>Configurar o log no SQL Server Data Tools  
 Logs são associados a pacotes e são configurados no nível de pacote. Cada tarefa ou contêiner em um pacote pode registrar informações em qualquer log de pacote. As tarefas e os contêineres em um pacote podem ser habilitados para registro mesmo se o próprio pacote não for habilitado para isso. Por exemplo, você pode habilitar o registro em uma tarefa Executar SQL sem habilitar o registro no pacote pai. Um pacote, contêiner ou tarefa pode gravar em vários logs. Você só pode habilitar o registro no pacote ou optar por habilitar o registro em qualquer tarefa ou contêiner individual que o pacote inclua.  
  
 Ao adicionar o log a um pacote, você escolhe o provedor de log e o local do log. O provedor de log especifica o formato para obter os dados de log: por exemplo, um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou arquivo de texto.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui os seguintes provedores de log:  
  
-   O provedor de log Arquivo de texto que grava entradas de log em arquivos de texto de ASCII em formato CSV (valores separados por vírgula). A extensão de nome de arquivo padrão deste provedor é .log.  
  
-   O provedor de log [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , que grava rastreamentos que você pode exibir usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler. A extensão de nome de arquivo padrão deste provedor é .trc.  
  
    > [!NOTE]  
    >  Não é possível usar o provedor de log [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] em um pacote executado no modo de 64 bits.  
  
-   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de log, que grava entradas de log a `sysssislog` tabela um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados.  
  
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
  
 Você também pode criar provedores de log personalizados. Para saber mais, veja [Creating a Custom Log Provider](../extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md).  
  
 Os provedores de log em um pacote são membros da coleção de provedores de log do pacote. Quando você cria um pacote e implementa o log usando o Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , pode ver uma lista dos membros da coleção nas pastas **Provedor de Log** da guia **Explorador de Pacotes** do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Você pode configurar um provedor de log fornecendo um nome e uma descrição para ele e especificando o gerenciador de conexões que ele usa. O provedor de log [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa um gerenciador de conexões OLE DB. Os provedores de log Arquivo de texto, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]e Arquivo XML usam gerenciadores de conexões de Arquivo. O provedor de log de Eventos do Windows não usa um gerenciador de conexões, pois grava diretamente no log de Eventos do Windows. Para obter mais informações, consulte [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md) e [File Connection Manager](../connection-manager/file-connection-manager.md).  
  
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
  
##### <a name="log-entries"></a>Entradas de log  
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
|**Diagnostic**|Grava uma entrada de log que fornece informações de diagnóstico.<br /><br /> Por exemplo, você pode registrar uma mensagem antes e depois de cada chamada para um provedor de dados externo. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../troubleshooting/troubleshooting-tools-for-package-execution.md).|  
  
 O pacote e muitas tarefas têm entradas de log personalizadas que podem ser habilitadas para registro. Por exemplo, a tarefa Enviar Email fornece a entrada de log personalizada **SendMailTaskBegin** , que registra informações quando a tarefa Enviar Email começa a ser executada, mas antes de a tarefa enviar uma mensagem de email. Para saber mais, veja [Custom Messages for Logging](../custom-messages-for-logging.md).  
  
### <a name="differentiating-package-copies"></a>Diferenciando cópias de pacotes  
 Os dados de log incluem o nome e o GUID do pacote ao qual as entradas de log pertencem. Se você criar um novo pacote copiando um pacote existente, o nome e o GUID do pacote existente também serão copiados. Como resultado, você pode ter dois pacotes com o mesmo GUID e nome, dificultando a diferenciação entre eles nos dados de log.  
  
 Para eliminar essa ambiguidade, você deve atualizar o nome e o GUID dos novos pacotes. No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você pode gerar o GUID novamente na propriedade `ID` e atualizar o valor da propriedade `Name` na janela Propriedades. Você também pode alterar o GUID e o nome programaticamente ou usando o prompt de comando **dtutil** . Para obter mais informações, consulte [Definir as propriedades do pacote](../set-package-properties.md) e [Utilitário dtutil](../dtutil-utility.md).  
  
### <a name="parent-logging-options"></a>Opções de log pai  
 Geralmente, as opções de log de tarefas e os contêineres Loop For, Loop Foreach e Sequência correspondem às opções do pacote ou de um contêiner pai. Nesse caso, você pode configurá-las para herdar as opções de log de seus contêineres pai. Por exemplo, em um contêiner Loop For que inclui uma tarefa Executar SQL, essa tarefa pode usar as opções de log que são definidas no contêiner Loop For. Para usar as opções de log pai, defina a propriedade LoggingMode do contêiner como **UseParentSetting**. É possível definir essa propriedade na janela **Propriedades** do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou através da caixa de diálogo **Configurar Logs de SSIS** no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
### <a name="logging-templates"></a>Modelos de log  
 Na caixa de diálogo **Configurar Logs de SSIS** , você também pode criar e salvar configurações de log usadas com frequência como modelos e depois usar esses modelos em vários pacotes. Isso facilita a aplicação de uma estratégia de log consistente entre vários pacotes e a modificação de definições de log nos pacotes atualizando e depois aplicando os modelos. Os modelos são armazenados em arquivos XML.  
  
 **Para configurar o registro usando a caixa de diálogo Configurar Logs de SSIS**  
  
1.  Habilite o pacote e suas tarefas para registrar. O registro pode ocorrer no nível de pacote, contêiner e tarefa. Você pode especificar logs diferentes para pacotes, contêineres e tarefas.  
  
2.  Selecione um provedor de log e adicione um log ao pacote. Os logs podem ser criados apenas no nível de pacote, e uma tarefa ou contêiner deve usar um dos logs criados para esse pacote. Cada log é associado a um dos seguintes provedores de log: arquivo de texto, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Log de Eventos do Windows ou arquivo XML. Para obter mais informações, consulte [Habilitar o log de pacote no SQL Server Data Tools](../enable-package-logging-in-sql-server-data-tools.md).  
  
3.  Selecione os eventos e as informações de esquema de log sobre cada evento que você deseja capturar no log. Para obter mais informações, consulte [Configurar o log usando um arquivo de configuração salvo](../configure-logging-by-using-a-saved-configuration-file.md).  
  
### <a name="configuration-of-log-provider"></a>Configuração do provedor de log  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Um provedor de log é criado e configurado como uma etapa na implementação do log em um pacote. Para obter mais informações, consulte [o log de serviços de integração](integration-services-ssis-logging.md).  
  
 Depois de criar um provedor de log, você pode exibir e modificar suas propriedades na janela Propriedades do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Para obter mais informações sobre como definir essas propriedades programaticamente, consulte a documentação da classe <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> .  
  
### <a name="logging-for-data-flow-tasks"></a>Registro para tarefas Fluxo de Dados  
 A tarefa Fluxo de Dados fornece muitas entradas de log personalizadas que podem ser usadas para monitorar e ajustar o desempenho. Por exemplo, você pode monitorar os componentes que podem causar vazamentos de memória ou controlar quanto tempo leva para executar um determinado componente. Para obter uma lista dessas entradas de log personalizadas e saída de exemplo de log, consulte [Data Flow Task](../control-flow/data-flow-task.md).  
  
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
  
## <a name="related-tasks"></a>Related Tasks  
 A lista a seguir contém links para tópicos que mostram como executar tarefas relacionadas ao recurso de log.  
  
-   [Caixa de diálogo Configurar Logs do SSIS](../configure-ssis-logs-dialog-box.md)  
  
-   [Habilitar o log de pacote no SQL Server Data Tools](../enable-package-logging-in-sql-server-data-tools.md)  
  
-   [Habilitar o log para a execução do pacote no servidor SSIS](../enable-logging-for-package-execution-on-the-ssis-server.md)  
  
-   [Exibir entradas de log na janela Eventos de Log](../view-log-entries-in-the-log-events-window.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Ferramenta DTLoggedExec para log completo e detalhado (Projeto CodePlex)](http://go.microsoft.com/fwlink/?LinkId=150579)  
  
## <a name="see-also"></a>Consulte também  
 [Exibir entradas de log na janela Eventos de Log](../view-log-entries-in-the-log-events-window.md)  
  
  