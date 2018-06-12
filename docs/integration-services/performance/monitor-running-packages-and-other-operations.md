---
title: Monitorar pacotes em execução e outras operações | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2018
ms.prod: sql
ms.prod_service: integration-services
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.isoperations.executions.f1
- sql13.ssis.ssms.isoperations.general.f1
ms.assetid: cbbcd79f-ab9b-46ec-84cb-4821c1d16b99
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e2b5a991661e3aa53de611a0cf78e04b2a6d23b5
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34772134"
---
# <a name="monitor-running-packages-and-other-operations"></a>Monitorar a execução de pacotes e outras operações
  Você pode monitorar execuções de pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , validações de projeto e outras operações usando uma ou mais das ferramentas a seguir. Algumas ferramentas, como toques de dados, estão disponíveis somente para os projetos que são implantados no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
-   Logs  
  
     Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
-   Relatórios  
  
     Para saber mais, confira [Reports for the Integration Services Server](#reports).  
  
-   exibições  
  
     Para obter mais informações, consulte [Exibições &#40;Catálogo do Integration Services&#41;](../../integration-services/system-views/views-integration-services-catalog.md).  
  
-   Contadores de desempenho  
  
     Para obter mais informações, consulte [Performance Counters](../../integration-services/performance/performance-counters.md).  
  
-   Toques de dados  

> [!NOTE]
> Este artigo descreve como monitorar a execução de pacotes do SSIS em geral e como monitorar a execução de pacotes localmente. Também é possível executar e monitorar pacotes do SSIS no Banco de Dados SQL do Azure. Para obter mais informações, consulte [Migrar cargas de trabalho do SQL Server Integration Services por lift-and-shift para a nuvem](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md).
>
> Embora também seja possível executar pacotes do SSIS no Linux, nenhuma ferramenta de monitoramento é fornecida no Linux. Para obter mais informações, consulte [Extrair, transformar e carregar dados no Linux com o SSIS](../../linux/sql-server-linux-migrate-ssis.md).

## <a name="operation-types"></a>Tipos de operação  
 São monitorados vários tipos diferentes de operações no catálogo **SSISDB** , no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Cada operação pode ter várias mensagens associadas a ela. Cada mensagem pode ser classificada em um de vários tipos diferentes. Por exemplo, uma mensagem pode ser de tipo Informações, Aviso ou Erro. Para obter a lista completa dos tipos de mensagem, consulte a documentação da exibição [catalog.operation_messages &#40;Banco de Dados do SSISDB&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md) do Transact-SQL. Para ver uma lista completa dos tipos de operação, consulte [catalog.operations &#40;Banco de Dados do SSISDB&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md).  
  
 São usados nove tipos de status diferentes para indicar o status de uma operação. Para ver uma lista completa dos tipos de status, consulte a exibição [catalog.operations &#40;Banco de Dados do SSISDB&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md).  

## <a name="active_ops"></a> Caixa de diálogo Operações Ativas
  Use a caixa de diálogo **Operações Ativas** para exibir o status de operações do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em execução no momento no servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , como implantação, validação e execução de pacotes. Esses dados são armazenados no catálogo SSISDB.  
  
 Para obter mais informações sobre modos de exibição do [!INCLUDE[tsql](../../includes/tsql-md.md)] relacionados, consulte [catalog.operations &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md), [catalog.validations &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-validations-ssisdb-database.md), e [catalog.executions &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)  
  
###  <a name="open_dialog"></a> Abrir a caixa de diálogo Operações Ativas  
  
1.  Abra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Conectar-se ao Mecanismo de Banco de Dados do Microsoft SQL Server  
  
3.  No Pesquisador de Objetos, expanda o nó **Integration Services** , clique com o botão direito do mouse em **SSISDB**e clique em **Operações Ativas**.  
  
### <a name="configure-the-options"></a>Configurar as opções  
  
 **Tipo**  
 Especifica o tipo de operação. Os seguintes são os valores possíveis para o campo **Tipo** e os valores correspondentes na coluna operations_type da exibição **catalog.operations** do Transact-SQL.  
  
|||  
|-|-|  
|Inicialização do Integration Services|1|  
|Limpeza de operações (trabalho do SQL Agent)|2|  
|Limpeza de versões do projeto (trabalho do SQL Agent)|3|  
|Implantar projeto|101|  
|Restaurar projeto|106|  
|Criar e iniciar execução de pacote|200|  
|Parar operação (parando uma validação ou execução|202|  
|Validar projeto|300|  
|Validar pacote|301|  
|Configurar catálogo|1.000|  
  
 **Parar**  
 Clique para parar uma operação em execução no momento.  

## <a name="viewing-and-stopping-packages-running-on-the-integration-services-server"></a>Exibindo e parando pacotes que são executados no servidor do Integration Services
  O banco de dados do **SSISDB** armazena o histórico da execução em tabelas internas que não são visíveis aos usuários. Porém, ele expõe as informações necessárias por meio de exibições públicas que você pode consultar. Ele também fornece procedimentos armazenados que você pode chamar para executar tarefas comuns relacionadas a pacotes.  
  
 Normalmente você gerencia objetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no servidor no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. No entanto, você também pode consultar as exibições de banco de dados e chamar os procedimentos armazenados diretamente, ou escrever código personalizado que chame a API gerenciada. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e a API gerenciada consultam as exibições e chamam os procedimentos armazenados para executar muitas de suas tarefas. Por exemplo, você pode exibir a lista de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que estão em execução atualmente no servidor e solicitar a interrupção de pacotes, se necessário.  
  
### <a name="viewing-the-list-of-running-packages"></a>Exibindo a lista de pacotes em execução  
 É possível exibir a lista de pacotes que estão sendo executados no momento no servidor na caixa de diálogo **Operações Ativas** . Para obter mais informações, consulte [Active Operations Dialog Box](#active_ops).  
  
 Para obter informações sobre os outros métodos que podem ser usados para exibir a lista de pacotes em execução, consulte os tópicos a seguir.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] acesso  
 Para exibir a lista de pacotes em execução no servidor, consulte a exibição [catalog.executions &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md) para obter pacotes que têm um status 2.  
  
 Acesso programático por meio de API gerenciada  
 Consulte o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices> e suas classes.  
  
### <a name="stopping-a-running-package"></a>Interrompendo um pacote em execução  
 Você pode solicitar um pacote em execução a ser interrompido na caixa de diálogo **Operações Ativas** . Para obter mais informações, consulte [Active Operations Dialog Box](#active_ops).  
  
 Para obter informações sobre os outros métodos que podem ser usados para interromper um pacote em execução, consulte os tópicos a seguir.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] acesso  
 Para interromper um pacote em execução no servidor, chame o procedimento armazenado, [catalog.stop_operation &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md).  
  
 Acesso programático por meio de API gerenciada  
 Consulte o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices> e suas classes.  
  
### <a name="viewing-the-history-of-packages-that-have-run"></a>Exibindo o histórico de pacotes executados  
 Para exibir o histórico de pacotes executados no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], use o relatório **Todas as Execuções** . Para obter mais informações sobre o relatório **Todas as Execuções** e outros relatórios padrão, consulte [Relatórios do servidor do Integration Services](#reports).  
  
 Para obter informações sobre os outros métodos que podem ser usados para exibir o histórico de pacotes em execução, consulte os tópicos a seguir.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] acesso  
 Para exibir informações sobre os pacotes que foram executados, consulte a exibição [catalog.executions &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md).  
  
 Acesso programático por meio de API gerenciada  
 Consulte o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices> e suas classes.  

## <a name="reports"></a> Reports for the Integration Services Server
  Na versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], os relatórios padrão estão disponíveis no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para ajudar a monitorar projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , que foram implantados no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Esses relatórios ajudam a exibir o status e o histórico do pacote e, se necessário, a identificar a causa de falhas na execução do pacote.  
  
 Na parte superior de cada página de relatório, o ícone de voltar leva você à página anteriormente exibida, o ícone de atualização atualiza as informações exibidas na página e o ícone de impressão permite imprimir a página atual.  
  
 Para obter informações sobre como implantar pacotes no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], consulte [Implantar projetos e pacotes no SSIS (Integration Services)](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
### <a name="integration-services-dashboard"></a>Painel do Integration Services  
 O relatório **Painel do Integration Services** oferece uma visão geral de todas as execuções de pacote na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para cada pacote executado no servidor, o painel permite "ampliar" para localizar detalhes específicos sobre erros de execução de pacote que possam ter ocorrido.  
  
 O relatório exibe as seções de informações a seguir.  
  
|Seção|Descrição|  
|-------------|-----------------|  
|**Informações de Execução**|Mostra o número de execuções que estão em estados diferentes (com falha, executando, teve sucesso, outros) nas últimas 24 horas.|  
|**Informações do Pacote**|Mostra o número total de pacotes que foram executados nas últimas 24 horas.|  
|**Informações de Conexão**|Mostra as conexões que foram usadas em execuções com falha nas últimas 24 horas.|  
|**Informações Detalhadas do Pacote**|Mostra os detalhes das execuções completas ocorridas nas últimas 24 horas. Por exemplo, esta seção mostra o número de execuções com falha em relação ao número total de execuções, a duração de execuções (em segundos) e a duração média de execuções nos últimos três meses.<br /><br /> Você pode exibir informações adicionais para um pacote clicando em **Visão Geral**, **Todas as Mensagens**e **Desempenho de Execução**.<br /><br /> O relatório de **Desempenho de Execução** mostra a duração da última instância de execução, bem como as horas de início e de término, e o ambiente que foi aplicado.<br /><br /> O gráfico e a tabela associada incluídos no relatório de **Desempenho de Execução** mostram a duração das últimas 10 execuções com êxito do pacote. A tabela também mostra a duração média de uma execução em um período de três meses. Os ambientes diferentes e os valores literais diferentes podem ter sido aplicados em tempo de execução dessas 10 execuções com êxito do pacote.<br /><br /> Finalmente, o relatório de **Desempenho de Execução** mostra a hora ativa e o tempo total para os componentes de fluxo de dados do pacote. O Tempo Ativo se refere ao tempo total que o componente gastou na execução em todas as fases, e o Tempo Total representa o tempo total decorrido para um componente. O relatório só exibe essas informações para componentes do pacote quando o nível de log da última execução do pacote foi definido como o desempenho ou detalhado.<br /><br /> O relatório de **Visão Geral** mostra o estado de tarefas do pacote. O relatório de **Mensagens** mostra as mensagens de evento e as mensagens de erro para o pacote e as tarefas, como relatar as horas de início e de término, e o número de linhas gravadas.<br /><br /> Você também pode clicar em **Exibir Mensagens** no relatório de **Visão Geral** para navegar até o relatório **Mensagens** . Você também pode clicar em **Exibir Visão Geral** no relatório **Mensagens** para navegar até o relatório **Visão Geral** .|  
  
 Você pode filtrar a tabela exibida em qualquer página clicando em **Filtrar** e, em seguida, selecionando os critérios na caixa de diálogo **Configurações de Filtro** . Os critérios de filtro disponíveis dependem dos dados que estão sendo exibidos. É possível alterar a ordem de classificação do relatório clicando no ícone de classificação na caixa de diálogo **Configurações de Filtro** .  
  
### <a name="all-executions-report"></a>Relatório Todas as Execuções  
 O **Relatório Todas as Execuções** exibe um resumo de todas as execuções do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que foram efetuadas no servidor. Pode haver várias execuções do pacote de exemplo. Ao contrário do relatório **Painel do Integration Services** , você pode configurar o relatório **Todas as Execuções** para mostrar as execuções iniciadas durante um intervalo de datas. As datas podem abranger vários dias, meses ou anos.  
  
 O relatório exibe as seções de informações a seguir.  
  
|Seção|Descrição|  
|-------------|-----------------|  
|Filtro|Mostra o filtro atual aplicado ao relatório, como o intervalo de horas de início.|  
|Informações de Execução|Mostra a hora de início, a hora de término e a duração para cada execução do pacote. Você pode exibir uma lista de valores de parâmetros que foram usados com uma execução de pacote, como valores que foram transmitidos a um pacote filho usando a tarefa Executar Pacote. Para exibir a lista de parâmetros, clique em Visão Geral.|  
  
 Para obter mais informações sobre como usar a tarefa Executar Pacote para disponibilizar valores para um pacote filho, consulte [Tarefa Executar Pacote](../../integration-services/control-flow/execute-package-task.md).  
  
 Para obter mais informações sobre parâmetros, consulte [Parâmetros de pacote e projeto do SSIS (Integration Services)](../../integration-services/integration-services-ssis-package-and-project-parameters.md).  
  
### <a name="all-connections"></a>Todas as Conexões  
 O relatório **Todas as Conexões** fornece as informações a seguir para conexões que falharam, para execuções que ocorreram na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 O relatório exibe as seções de informações a seguir.  
  
|Seção|Descrição|  
|-------------|-----------------|  
|Filtrar|Mostra o filtro atual aplicado ao relatório, como conexões com uma cadeia de caracteres especificada e o intervalo de **Hora da Última Falha** .<br /><br /> Você define o intervalo de **Hora da Última Falha** para exibir apenas as falhas de conexão que ocorreram durante um intervalo de datas. O intervalo pode abranger vários dias, meses ou anos.|  
|Detalhes|Mostra a cadeia de conexão, o número de execuções em que uma conexão falhou, e a data da última falha na conexão.|  
  
### <a name="all-operations-report"></a>Relatório Todas as Operações  
 O **Relatório Todas as Operações** exibe um resumo de todas as operações do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que foram executadas no servidor, inclusive implantação, validação e execução de pacotes e outras operações administrativas. Como no Painel do Integration Services, você pode aplicar um filtro à tabela para reduzir as informações exibidas.  
  
### <a name="all-validations-report"></a>Relatório Todas as Validações  
 O **Relatório Todas as Validações** exibe um resumo de todas as execuções do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que foram efetuadas no servidor. O resumo exibe informações para cada validação, como status, hora de início e hora de término. Cada entrada resumida inclui um link a mensagens geradas durante validação. Como no Painel do Integration Services, você pode aplicar um filtro à tabela para reduzir as informações exibidas.  
  
### <a name="custom-reports"></a>Relatórios personalizados  
 Você pode adicionar um relatório personalizado (arquivo .rdl) ao nó do catálogo do **SSISDB** no nó **Catálogos do Integration Services** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Antes de adicionar o relatório, confirme que você está usando uma convenção de nomenclatura de três partes para qualificar completamente os objetos que você referencia, por exemplo, uma tabela de origem. Caso contrário, o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] exibirá um erro. A convenção de nomenclatura é \<database>.\<owner>.\<object>. Um exemplo seria SSISDB.internal.executions.  
  
> [!NOTE]  
>  Quando você adicionar relatórios personalizados ao nó do **SSISDB** , no nó **Bancos de Dados** , o prefixo do SSISDB não será necessário.  
  
 Para obter instruções sobre como criar e adicionar um relatório personalizado, consulte [Adicionar um relatório personalizado ao Management Studio](http://msdn.microsoft.com/library/3cf8d726-0a90-4f80-98d0-352a2a59be0f).  

## <a name="view-reports-for-the-integration-services-server"></a>Exibir relatórios do servidor do Integration Services
  Na versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], os relatórios padrão estão disponíveis no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para ajudar a monitorar projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , que foram implantados no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  Para saber mais sobre os relatórios, consulte [Relatórios do servidor do Integration Services](#reports).  
  
### <a name="to-view-reports-for-the-integration-services-server"></a>Para exibir relatórios do servidor do Integration Services  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó **Catálogos do Integration Services** no Pesquisador de Objetos.  
  
2.  Clique com o botão direito do mouse em **SSISDB**, clique em **Relatórios**e em **Relatórios Padrão**.  
  
3.  Clique em mais um item abaixo para exibir um relatório.  
  
    -   **Painel do Integration Services**  
  
    -   **Todas as Execuções**  
  
    -   **Todas as Validações**  
  
    -   **Todas as Operações**  
  
    -   **Todas as Conexões**  

## <a name="see-also"></a>Consulte Também  
 [Execução de projetos e pacotes](../packages/deploy-integration-services-ssis-projects-and-packages.md)   
 [Relatórios para solução de problemas de execução de pacote](../troubleshooting/troubleshooting-reports-for-package-execution.md)  
