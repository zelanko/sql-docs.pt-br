---
title: Alertas de dados do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 8c234077-b670-45c0-803f-51c5a5e0866e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d5dd8bad47bdbc1faaec1dcb7e9c7e9a05bed548
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66102983"
---
# <a name="reporting-services-data-alerts"></a>Alertas de dados do Reporting Services
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] são uma solução de alerta de dados que ajuda você a manter-se informado sobre os dados de relatório interessantes ou importantes para você, na hora certa. Usando dados de alerta você não precisa mais procurar informações, elas vêm até você.  
  
 As mensagens de alerta de dados são enviadas por email. Dependendo da importância das informações, você pode optar por enviar mensagens com maior ou menor frequência e somente quando os resultados forem alterados. Você pode especificar vários destinatários de email e, assim, manter os outros informados e aprimorar a eficiência e a colaboração.  
  
||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  |  
  
##  <a name="AlertingWF"></a> Arquitetura de alertas de dados e fluxo de trabalho  
 A seguir é apresentado um resumo das áreas principais dos alertas de dados do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] :  
  
-   **Definir e salvar definições de alerta de dados** – você executa um relatório, cria regras que identificam valores de dados interessantes, define um padrão de recorrência para enviar a mensagem de alerta de dados e especifica os destinatários da mensagem de alerta.  
  
-   **Executar definições de alerta de dados** – o serviço de alerta processa as definições de alerta em um horário agendado, recupera dados de relatório e cria instâncias de alerta de dados com base nas regras da definição de alerta.  
  
-   **Entregar mensagens de alerta de dados a destinatários** – o serviço de alerta cria uma instância de alerta e envia uma mensagem de alerta aos destinatários por email.  
  
 Além disso, como proprietário do alerta de dados, você pode exibir informações sobre seus alertas de dados e excluir e editar suas definições de alerta de dados. Um alerta tem apenas um proprietário, a pessoa que o criou.  
  
 Administradores de alertas, usuários com permissão para Gerenciar Alertas do SharePoint podem gerenciar alertas de dados no nível do site. Eles podem exibir listas de alertas de cada usuário de site e excluir alertas.  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] são diferentes dos alertas do SharePoint. Você pode definir alertas do SharePoint em qualquer tipo de documento, inclusive em relatórios. Os alertas do SharePoint são enviados quando o documento é alterado. Por exemplo, você adiciona uma coluna a uma tabela em um relatório. Em comparação, os alertas de dados são enviados quando os dados mostrados em um relatório atenderam as regras nas definições do alerta. Normalmente, as regras fazem referência a dados que são exibidos em um relatório.  
  
 Ao criar alertas de dados em relatórios, você pode monitorar as alterações nos dados de relatórios e enviar mensagens de alertas de dados por email quando os dados de relatório seguem regras que definem dados de interesse para você e outros usuários e em intervalos que atendem suas necessidades comerciais. Você também pode executar dados de alertas sob demanda. Se você tiver permissão de Criar Alerta do SharePoint, poderá criar alertas em qualquer relatório no qual tenha permissões de exibição. É possível criar vários alertas em um relatório, e vários usuários podem criar os mesmos ou alertas diferentes em um relatório. Para colaborar com outros usuários, você pode especificá-los como destinatários de mensagens de alerta nas definições de alertas de dados que você cria.  
  
 O diagrama a seguir mostra o fluxo de trabalho de criação e salvamento de uma definição de alerta de dados, da criação de um trabalho do SQL Agent para começar o processamento de uma instância do alerta de dados e do envio de mensagens de alertas de dados que contêm os dados de relatório que dispararam o alerta para um ou mais destinatários por email.  
  
 ![Fluxo de trabalho dos alertas do Reporting Services](media/rs-alertingworkflow.gif "Fluxo de trabalho dos alertas do Reporting Services")  
  
### <a name="reports-supported-by-data-alerts"></a>Relatórios com suporte de alertas de dados  
 Você pode criar alertas de dados em todos os tipos de relatórios profissionais que são escritos no idioma de definição de relatório (RDL) e criados no Designer de Relatórios ou no Construtor de Relatórios. Relatórios que incluem regiões de dados, como tabelas e gráficos, relatórios com sub-relatórios e relatórios complexos com vários grupos de colunas paralelos e regiões de dados aninhadas. Os únicos requisitos são o relatório incluir pelo menos uma região de dados de qualquer tipo e a fonte de dados de relatório ser configurada para usar credenciais armazenadas ou nenhuma credencial. Você não pode criar um alerta em um relatório que não tenha nenhuma região de dados.  
  
 Você não pode criar alertas de dados em relatórios criados com o [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)].  
  
 Ao instalar o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no modo nativo ou no modo do SharePoint ou ao usar a versão autônoma do Construtor de Relatórios, você pode salvar relatórios em um servidor de relatório, em seu computador ou em uma biblioteca do SharePoint. Para criar alertas de dados em relatórios, os relatórios devem ser salvos ou carregados em uma biblioteca do SharePoint. Isso significa que você não pode criar alertas em relatórios salvos em um servidor de relatório no modo nativo ou em seu computador. Além disso, você não pode criar alertas inseridos em aplicativos personalizados.  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte a uma variedade de tipos de credencial em relatórios. É possível criar alertas de dados em relatórios com fontes de dados configuradas para usar credenciais armazenadas ou nenhuma credencial. Você não pode criar alertas em relatórios configurados para usar credenciais de segurança integrada ou para solicitar credenciais. O relatório é executado como parte do processamento da definição de alerta e o processamento falha sem credenciais. Para obter mais informações, consulte o seguinte:  
  
-   [Especificar informações de credenciais e de conexão para fontes de dados de relatório](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
-   [Funções e permissões &#40;Reporting Services&#41;](security/roles-and-permissions-reporting-services.md)  
  
-   [Autenticação com o servidor de relatório](security/authentication-with-the-report-server.md)  
  
### <a name="run-reports"></a>Executar relatórios  
 A primeira etapa na criação de uma definição de alerta de dados é localizar o relatório desejado na biblioteca do SharePoint e depois executar o relatório. Não é possível criar um alerta em um relatório não contenha nenhum dado no momento.  
  
 Se o relatório for parametrizado, especifique os valores de parâmetros a serem usados quando você executar o relatório. Os valores de parâmetros serão salvos nas definições de alertas de dados que você cria em um relatório. Os valores são usados quando o relatório é executado novamente como uma etapa no processamento da definição de alertas de dados. Se você quiser alterar os valores de parâmetros necessários para executar novamente o relatório com esses valores de parâmetros e criar uma definição de alerta nessa versão do relatório.  
  
### <a name="create-data-alert-definitions"></a>Criar definições de alertas de dados  
 O recurso de alertas de dados do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] inclui o Designer de Alertas de Dados, que você usa para criar definições de alertas de dados.  
  
 Para criar uma definição de alerta de dados, você executa o relatório e abre o Designer de Alertas de Dados do Visualizador de Relatórios do SharePoint no menu **Ações** . Os feeds de dados do relatório são gerados e as primeiras 100 linhas do feed de dados são exibidas em uma tabela de visualização de dados no Designer de Alertas de Dados. Todos os feeds de dados de um relatório são armazenados em cache enquanto você está trabalhando na definição de alerta no Designer de Alertas de Dados. O cache permite alternar rapidamente entre feeds de dados. Quando você reabre uma definição de alerta no Designer de Alertas de Dados, os feeds de dados são atualizados.  
  
 Definições de alertas de dados consistem em regras e cláusulas que os dados de relatório devem satisfazer para disparar uma mensagem de alerta de dados, um agendamento que define a frequência de envio da mensagem de alerta e, opcionalmente, as datas para iniciar e parar o envio da mensagem de alerta, informações como a linha de Assunto e uma descrição a ser incluída na mensagem de alerta e os destinatários da mensagem. Depois de criar uma definição de alerta, você a salva no banco de dados de alertas do SQL Server.  
  
### <a name="save-data-alert-definitions-and-alerting-metadata"></a>Salvar definições de alertas de dados e metadados de alerta  
 Quando você instala o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no modo integrado do SharePoint, o banco de dados de alertas do SQL Server é criado automaticamente.  
  
 As definições de alertas de dados e os metadados de alerta são salvos no banco de dados de alertas. Por padrão, esse banco de dados é chamado ReportingServices\<GUID>_Alerting.  
  
 Quando você salva a definição de alerta de dados, o alerta cria um trabalho do SQL Server Agent para a definição do alerta. O trabalho inclui um agendamento de trabalho. O agendamento se baseia no padrão de recorrência que você define na definição de alerta. A execução do trabalho inicia o processamento da definição de alerta de dados.  
  
### <a name="process-data-alert-definitions"></a>Processar definições de alerta de dados  
 Quando o agendamento do trabalho do SQL Server Agent inicia o processamento da definição de alerta, o relatório é executado para atualizar os feeds de dados de relatório. O serviço de alerta lê os feeds de dados e aplica as regras que as definições de alertas de dados especificam para os valores dos dados. Se um ou mais valores de dados satisfizerem as regras, uma instância de alerta de dados é criada e uma mensagem de alerta de dados com os resultados de alertas é enviada a todos os destinatários por email. Os resultados são linhas de dados de relatório que satisfizeram todas as regras no momento de criação da a instância de alerta. Para impedir várias mensagens de alerta com os mesmos resultados, você pode especificar que as mensagens somente sejam enviadas quando os resultados forem alterados. Nesse caso, uma instância alerta é criada e salva no banco de dados de alertas, mas nenhuma mensagem de alerta é gerada. Se um erro ocorrer, a instância de alerta também será salva no banco de dados de alertas e uma mensagem de alerta com os detalhes sobre o erro é enviada aos destinatários. A seção Diagnóstico e log têm posteriormente neste tópico tem mais informações sobre como registrar em log e solucionar problemas.  
  
### <a name="send-data-alert-messages"></a>Enviar mensagens de alerta de dados  
 As mensagens de alerta de dados são enviadas por email.  
  
 A linha **De** contém um valor fornecido pela configuração de entrega de email do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . A linha **Para** lista os destinatários que você especificou ao criar o alerta no Designer de Alertas de Dados.  
  
 Além da linha de Assunto de email, que você especifica no Designer de Alertas de Dados, a mensagem de alerta de dados inclui as seguintes informações:  
  
-   O nome da pessoa que criou a definição do alerta de dados.  
  
-   Se você forneceu uma descrição na definição de alerta, ela será exibida na parte superior do texto de email.  
  
-   Os resultados de alertas, consistindo nas linhas no feed de dados de relatório que satisfazem as regras especificadas na definição de alerta.  
  
-   Um link para o relatório no qual a definição de alerta se baseia.  
  
-   As regras na definição de alerta.  
  
-   Os parâmetros e valores que você usou para executar o relatório.  
  
-   Os valores contextuais de itens de relatório que estão fora das regiões de dados de relatório.  
  
 Se não for possível criar uma instância de alerta de dados ou mensagem de alerta de dados, uma mensagem de erro será enviada para todos os destinatários. Em vez dos resultados de alertas, a mensagem inclui uma descrição de erro.  
  
 Para obter mais informações, consulte [Data Alert Messages](../../2014/reporting-services/data-alert-messages.md).  
  
##  <a name="InstallAlerting"></a> Instalar os alertas de dados  
 O recurso de alertas de dados está disponível apenas quando o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] está instalado no modo integrado do SharePoint. Quando você instala o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no modo do SharePoint, a instalação cria automaticamente o banco de dados de alertas que armazena definições de alertas de dados e metadados de alertas, e duas páginas do SharePoint para gerenciamento de alertas, e adiciona o Designer de Alertas no site do SharePoint. Não há nenhuma etapa especial para execução, ou opções para definição de alertas durante a instalação.  
  
 Se você quiser saber mais sobre como instalar o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no modo do SharePoint, inclusive o serviço compartilhado do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , que é novo no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] e no aplicativo do serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] que você deve criar e configurar antes de poder usar recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , consulte [Instalar o Reporting Services no Modo do SharePoint para SharePoint 2010](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md) na biblioteca MSDN.  
  
 Como mostra o diagrama anterior deste tópico, os alertas de dados usam trabalhos do SQL Server Agent. Para criar os trabalhos, o SQL Server Agent deve estar em execução. Talvez você tenha configurado o SQL Server Agent para iniciar automaticamente quando instalou o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Se não, você pode iniciar o SQL Server Agent manualmente. Para obter mais informações, consulte [Configurar o SQL Server Agent](../ssms/agent/configure-sql-server-agent.md) e [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
 Você pode usar a página **Provisionar Assinaturas e Alertas** na Administração Central do SharePoint para descobrir se o SQL Server Agent está sendo executado e criar e baixar scripts [!INCLUDE[tsql](../includes/tsql-md.md)] personalizados que executa para conceder permissões ao SQL Server Agent. Se possível, gere também os scripts [!INCLUDE[tsql](../includes/tsql-md.md)] usando o PowerShell. Para obter mais informações, consulte [Provisionar assinaturas e alertas para aplicativos de serviço do SSRS](install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  
##  <a name="ConfigAlert"></a> Configurar alertas de dados  
 Desde o [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] , as configurações para recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , inclusive alertas de dados, são distribuídas entre o arquivo de configuração de servidor de relatório (rsreportserver.config) e um banco de dados de configuração do SharePoint sempre que você instala o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no modo do SharePoint. Quando você cria o aplicativo de serviço como uma etapa na instalação e configuração do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], o banco de dados de configuração do SharePoint é criado automaticamente. Para obter mais informações, consulte [RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md) e [arquivos de configuração do Reporting Services](report-server/reporting-services-configuration-files.md).  
  
 As configurações para alertas de dados do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] incluem os intervalos para limpar dados e metadados de alertas e o número de repetições ao enviar mensagens de alerta de dados por email. Você pode atualizar o arquivo de configuração e o banco de dados de configuração para usarem valores diferentes para configurações de alertas de dados  
  
 Você atualiza o arquivo de configuração do servidor de relatório diretamente. Você atualiza o banco de dados de configuração do SharePoint usando cmdlets do Windows PowerShell.  
  
 A tabela a seguir lista os elementos da configuração para alertas de dados e seus valores padrão, descrições e locais.  
  
|Configuração|Valor Padrão|Descrição|Location|  
|-------------|-------------------|-----------------|--------------|  
|AlertingCleanupCycleMinutes|20|Número de minutos entre inícios do ciclo de limpeza.|Arquivo de configuração do servidor de relatório|  
|AlertingExecutionLogCleanupMinutes|10080|Número de minutos para manter entradas do log de execução.|Arquivo de configuração do servidor de relatório|  
|AlertingDataCleanupMinutes|360|Número de minutos para manter dados temporários.|Arquivo de configuração do servidor de relatório|  
|AlertingMaxDataRetentionDays|180|O número de dias para a exclusão de metadados de execução de alertas, instâncias de alertas e resultados de execução.|Arquivo de configuração do servidor de relatório|  
|MaxRetries|3|O número de vezes para repetir o processamento de alertas de dados.|Banco de dados de configuração de serviço|  
|SecondsBeforeRetry|900|O número de segundos a aguardar antes de cada repetição.|Banco de dados de configuração de serviço|  
  
 Por padrão, as configurações MaxRetries e SecondsBeforeRetry se aplicam a todos os eventos que os alertas de dados disparam. Se você quiser mais controle granular das repetições e de atrasos de repetições, poderá adicionar elementos a todo e qualquer manipulador de eventos que especificar valores de MaxRetries e SecondsBeforeRetry diferentes.  
  
### <a name="event-handlers-and-retry"></a>Manipuladores de Eventos e Repetir  
 Os manipuladores de eventos são:  
  
|Manipulador de Eventos|Descrição|  
|-------------------|-----------------|  
|FireAlert|Clique em **Executar**  no Gerenciador de Alertas de Dados para iniciar o processamento imediato de uma definição de alerta.|  
|FireSchedule|O SQL Server Agent inicia o agendamento de trabalho para uma definição de alerta.|  
|CreateSchedule|Você cria uma definição de alerta de dados e um agendamento de trabalho do SQL Server Agent é criado com base no intervalo de frequência especificado na definição de alerta.|  
|UpdateSchedule|Você atualiza o intervalo de frequência da definição de alerta de dados e o agendamento de trabalho do SQL Server Agent é atualizado.|  
|DeleteSchedule|Você exclui a definição de alerta de dados e seu trabalho do SQL Server Agent é excluído.|  
|GenerateAlert|O tempo de execução de alerta processa o feed de dados de relatório, aplica as regras especificadas na definição de alerta de dados, determina se deve ser criada uma instância de alerta de dados e, se necessário, cria uma instância do alerta de dados.|  
|DeliverAlert|O tempo de execução cria a mensagem de alerta de dados e a envia para todos os destinatários por email.|  
  
 A tabela a seguir resume os manipuladores de eventos e quando a repetição será acionada:  
  
|Categoria do erro|<|\<|Tipo de evento||>|>|>|  
|--------------------|--------|--------|----------------|-|--------|--------|--------|  
||**FireAlert**|**FireSchedule**|**CreateSchedule**|**UpdateSchedule**|**DeleteSchedule**|**GenerateAlert**|**DeliverAlert**|  
|Memória insuficiente|X|X|X|X|X|X|X|  
|Anulação de thread|X|X|X|X|X|X|X|  
|O SQL Agent não está em execução|X||X|X|X|||  
|Transitório. Na maioria dos casos, devido a problemas de conexões, tempos limite e bloqueios.|X|X|X|X|X|X|X|  
|IOException|||||||X|  
|WebException|||||||X|  
|SocketException|||||||X|  
|SMTPException **(\*)**|||||||X|  
  
 **(\*)** Erros de SMTP que dispararão uma repetição:  
  
-   SmtpStatusCode.ServiceNotAvailable  
  
-   SmtpStatusCode.MailboxBusy  
  
-   SmtpStatusCode.MailboxUnavailable  
  
###  <a name="bkmk_disablealerts"></a> Desabilitar alertas de dados  
 Para desabilitar o recurso de alerta de dados, atualize a seção Serviço do arquivo de configuração. O código a seguir mostra a seção Serviço do arquivo de configuração.  
  
 `<Service>`  
  
 `<IsSchedulingService>True</IsSchedulingService>`  
  
 `<IsNotificationService>True</IsNotificationService>`  
  
 `<IsEventService>True</IsEventService>`  
  
 `<IsAlertingService>True</IsAlertingService>`  
  
 `...`  
  
 `</Service>`  
  
 Para desabilitar o alerta, altere True para False em `<IsAlertingService>True</IsAlertingService>`.  
  
##  <a name="Permissions"></a> Permissões para alertas de dados  
 Para poder criar alertas de dados em relatórios, você deve ter permissão para executar o relatório e para criar alertas no site do SharePoint. Para obter mais informações sobre permissões de relatório, consulte o seguinte.  
  
-   [Gerando feeds de dados de relatórios &#40;Construtor de Relatórios e SSRS&#41;](report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)  
  
-   [Definir permissões para itens do Servidor de Relatório em um site do SharePoint &#40;Reporting Services no modo integrado do SharePoint&#41;](security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] oferecem suporte a dois níveis de permissão: operador de informações e administrador de alerta. A tabela a seguir lista as permissões e as tarefas do SharePoint relacionadas.  
  
|Tipo de usuário|Permissão do SharePoint|Descrição da tarefa|  
|---------------|---------------------------|----------------------|  
|Operador de informações|Exibir Itens<br /><br /> Criar Alertas|Exibir os itens como relatórios e criar alertas de dados nos relatórios. Editar e excluir alertas.|  
|Administrador de alerta|Gerenciar Alertas|Exiba uma lista de todos os alertas de dados salvos no site do SharePoint e exclua alertas.|  
  
##  <a name="DiagnosticsLogging"></a> Diagnóstico e log  
 Os alertas de dados fornecem várias maneiras para ajudar os operadores de informações e administradores a manter o controle de alertas e a compreender porque houve falha de alertas e para ajudar os administradores a usar os logs de execução para saber quais mensagens de alerta foram enviadas para quem, o número de instâncias de alertas e assim por diante.  
  
### <a name="data-alert-manager"></a>Gerenciador de Alertas de Dados  
 O Gerenciador de Alertas de Dados lista definições de alertas e informações de erro que ajudam os operadores de informações e os administradores de alertas a compreenderem porque ocorreu uma falha. Algumas razões comuns de falha incluem:  
  
-   O feed de dados do relatório foi alterado e as colunas que eram usadas nas regras da definição de alertas de dados não estão mais incluídas no feed de dados.  
  
-   A permissão para exibir o relatório foi revocada.  
  
-   O tipo de dados da fonte de dados subjacente foi alterado e a definição de alerta não é mais válida.  
  
### <a name="logs"></a>Logs  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] fornece vários logs que podem ajudá-lo a saber mais sobre os relatórios que são executados durante o processamento de definições de alertas de dados, as instâncias de alertas de dados que são criadas e assim sucessivamente. Três logs são particularmente úteis: o log de execução de alerta, o log de execução do servidor de relatório e o log de rastreamento do servidor de relatório.  
  
 Para obter informações sobre outros logs do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , consulte [Fontes e arquivos de log do Reporting Services](report-server/reporting-services-log-files-and-sources.md).  
  
#### <a name="alerting-execution-log"></a>Log de execução de alerta  
 O serviço de tempo de execução de alerta grava entradas na tabela ExecutionLogView do banco de dados de alertas. Você pode consultar a tabela ou executar os procedimentos armazenados a seguir para obter informações de diagnóstico mais sofisticadas sobre os alertas de dados salvos no banco de dados de alertas.  
  
-   ReadAlertData  
  
-   ReadAlertHistory  
  
-   ReadAlertInstances  
  
-   ReadEventHistory  
  
-   ReadFeedPollHistory  
  
-   ReadFeedPools  
  
-   ReadPollData  
  
-   ReadSentAlerts  
  
 Você pode usar o SQL Agent para executar o procedimento armazenado em uma agenda. Para obter mais informações, consulte [SQL Server Agent](../ssms/agent/sql-server-agent.md).  
  
#### <a name="report-server-execution-log"></a>Log de execução de servidor de relatório  
 Relatórios são executados para gerar os feeds de dados nos quais as definições de alertas de dados se baseiam. O log de execução do servidor de relatório no banco de dados do servidor de relatório captura informações cada vez que o relatório é executado. Você pode consultar a exibição de ExecutionLog2 no banco de dados para obter informações detalhadas. Para obter mais informações, consulte [Log de execução do servidor de relatório e exibição do ExecutionLog3](report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
#### <a name="report-server-trace-log"></a>Log de rastreamento do Servidor de Relatório  
 O log de rastreamento do servidor de relatório contém informações detalhadas sobre as operações do serviço Servidor de Relatório, incluindo as operações executadas pelo serviço Web Servidor de Relatório, pelo Gerenciador de Relatórios e pelo processamento em segundo plano. As informações do log de rastreamento podem ser úteis se você estiver depurando um aplicativo que inclui um servidor de relatório ou investigando um problema específico que foi gravado no log de evento ou de execução. Para obter mais informações, consulte [Report Server Service Trace Log](report-server/report-server-service-trace-log.md).  
  
##  <a name="PerformanceCounters"></a> Contadores de desempenho  
 Os alertas de dados fornecem seus próprios contadores de desempenho. Todos menos um contador de desempenho estão relacionados a um evento que faz parte do serviço de tempo de execução de alerta. O contador de desempenho relacionado à fila de evento informa o comprimento da fila de todos os eventos ativos.  
  
|Evento ou fila de eventos|Contador de desempenho|  
|--------------------------|-------------------------|  
|ALERTINGQUEUESIZE|Alerta: comprimento da fila de evento|  
|FireAlert|Alerta: eventos processados - FireAlert|  
|FireSchedule|Alerta: eventos processados - FireSchedule|  
|CreateSchedule|Alerta: eventos processados - CreateSchedule|  
|UpdateSchedule|Alerta: eventos processados - UpdateSchedule|  
|DeleteSchedule|Alerta: eventos processados - DeleteSchedule|  
|GenerateAlert|Alerta: eventos processados - GenerateAlert|  
|DeliverAlert|Alerta: eventos processados - DeliverAlert|  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] fornece contadores de desempenho para outros recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [contadores de desempenho para os objetos de desempenho de reportserversharepoint: Service e ReportServer: Service](report-server/performance-counters-reportserver-service-performance-objects.md), [contadores de desempenho para o MSRS 2014 Web Service e o Windows do MSRS 2014 Objetos de desempenho do serviço &#40;modo nativo&#41;](report-server/performance-counters-msrs-2011-web-service-performance-objects.md), e [contadores de desempenho para o modo do SharePoint do MSRS 2014 Web Service e objetos de desempenho do MSRS 2014 Windows Service SharePoint modo &#40;SharePoint Modo de&#41;](report-server/performance-counters-msrs-2011-sharepoint-mode-performance-objects.md).  
  
##  <a name="SupportForSSL"></a> Suporte para SSL  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] pode usar o serviço HTTP SSL (protocolo SSL) para estabelecer conexões criptografadas com um servidor de relatório ou site do SharePoint.  
  
 O serviço de tempo de execução de alerta e a interface do usuário de alertas de dados oferecem suporte para SSL e funcionam de modo semelhante quer você use SSL ou HTTP; no entanto, há algumas diferenças sutis. Quando a definição de alerta de dados é criada usando uma conexão SSL, a URL associada à biblioteca do SharePoint da mensagem de alerta de dados também usa SSL. Você pode identificar a conexão SSL porque ela usa HTTPS, em vez de HTTP em sua URL. De modo semelhante, se a definição de alerta de dados foi criada usando uma conexão HTTP, o link para o site do SharePoint usa HTTP. Se a definição de alerta foi criada usando SSL ou HTTP, a experiência para usuários e administradores de alertas será idêntica ao uso do Designer de Alerta de Dados ou do Gerenciador de Alertas de Dados. Se o protocolo (HTTP ou SSL) for alterado entre a hora em que a definição de alerta foi criada e atualizada e salva novamente, o protocolo original será mantido e usado em URLs de link.  
  
 Se você criar um alerta de dados em um site do SharePoint que está configurado para usar o SSL e, em seguida, remover o requisito de SSL, o alerta continuará funcionando no site. Se o site for excluído, o site de zona padrão será usado.  
  
##  <a name="UserInterface"></a> Interface do usuário de alerta de dados  
 Os alertas de dados fornecem páginas do SharePoint para o gerenciamento de alertas e um designer para criação e edição de definições de alertas de dados.  
  
-   **Designer de Alertas de Dados** no qual você cria ou edita definições de alertas de dados. Para obter mais informações, consulte [Designer de Alertas de Dados](../../2014/reporting-services/data-alert-designer.md), [Criar um Alerta de Dados no Designer de Alertas de Dados](create-a-data-alert-in-data-alert-designer.md) e [Editar um alerta de dados no Designer de Alertas](edit-a-data-alert-in-alert-designer.md).  
  
-   **Gerenciador de Alertas de Dados** no qual você exibe listas de alertas de dados, exclui alertas e abre alertas para edição. O Gerenciador de Alertas de Dados é fornecido em duas versões: uma para os usuários gerenciarem os alertas que criam e uma para os administradores gerenciarem os alertas que pertencem aos usuários do site.  
  
     Para obter mais informações sobre como gerenciar alertas de dados que você criou, consulte [Gerenciador de Alertas de Dados para Usuários do SharePoint](../../2014/reporting-services/data-alert-manager-for-sharepoint-users.md) e [Gerenciar meus alertas de dados no Gerenciador de Alertas de Dados](manage-my-data-alerts-in-data-alert-manager.md).  
  
     Para obter mais informações sobre como gerenciar todos os alertas de dados em um site, consulte [Gerenciador de Alertas de dados para administradores de alertas](../../2014/reporting-services/data-alert-manager-for-alerting-administrators.md) e [Gerenciar todos os alertas de dados em um site do SharePoint no Gerenciador de Alertas de Dados](manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager.md).  
  
-   **Provisione assinaturas e alertas de dados** nos quais você descobre se os Reporting Services podem usar o SQL Server Agent para alertas de dados e scripts de download que permitem acesso ao SQL Server Agent. Para obter mais informações, consulte [Provisionar assinaturas e alertas para aplicativos de serviço do SSRS](install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  
##  <a name="Globalization"></a> Globalização de alertas de dados  
 Certos scripts, como Árabe e Hebraico, são escritos da direita para a esquerda. Os dados de alertas oferecem suporte para scripts da direita para a esquerda, bem como da esquerda para a direita. Os dados de alerta detectam a cultura e alteram a aparência e o comportamento da interface do usuário e o layout de mensagens de alertas de dados de acordo. A cultura é derivada da configuração regional do sistema operacional no computador do usuário. A cultura é salva cada vez que você atualiza e salva novamente a definição de alerta de dados.  
  
 A cultura pode afetar se os dados atendem às regras na definição de alerta. Comparações de cadeias de caracteres geralmente são afetadas pelas regras específicas de cultura.  
  
 A determinação se os dados de relatório satisfazem a definição de alerta pode ser afetada pela cultura na definição de alerta. Isso ocorre mais comumente em cadeias de caracteres. Por exemplo, em uma definição de alerta com a cultura alemã, uma regra que compara a letra "o" em inglês e a letra "ö" em alemão não seria satisfeita. Na mesma definição de alerta que usa a cultura inglesa, a regra seria satisfeita.  
  
 A formatação de dados também se baseia na cultura da definição de alerta. Por exemplo, se a cultura usar um período como o símbolo decimal, o valor será exibido como 45.67; enquanto uma cultura que usa uma vírgula como o símbolo decimal, exibe 45,67.  
  
 Dependendo da interface do usuário de alerta de dados que você usar, o suporte para itens da direita para a esquerda variará. O Designer de Alerta de Dados oferece suporte para o script da direita para a esquerda em caixas de texto, mas o layout do designer não é da direita para a esquerda. Seu layout é da esquerda para a direita, assim como outras ferramentas. Se uma definição de alerta for criada com orientação da direita para a esquerda, e depois editada em um ambiente da esquerda para a direita, a orientação de texto da direita para a esquerda será preservada quando você salvar a definição de alerta. O Gerenciador de Alertas de Dados se comporta da mesma forma que uma página do SharePoint. Seu layout é da direita para esquerda, assim como outras páginas do SharePoint. Mensagens de alertas de dados se baseiam em definições de alerta da direita para a esquerda, exibem texto de mensagem da direita para a esquerda e o layout de mensagem é da esquerda para a direita.  
  
##  <a name="HowTo"></a> Tarefas relacionadas  
  
-   [Salvar um relatório em uma biblioteca do SharePoint &#40;Construtor de Relatórios&#41;](report-builder/save-a-report-to-a-sharepoint-library-report-builder.md)  
  
-   [Criar um Alerta de Dados no Designer de Alertas de Dados](create-a-data-alert-in-data-alert-designer.md)  
  
-   [Editar um alerta de dados no Designer de Alertas](edit-a-data-alert-in-alert-designer.md)  
  
-   [Gerenciar Meus alertas de dados no Gerenciador de alertas de dados](manage-my-data-alerts-in-data-alert-manager.md)  
  
-   [Gerenciar todos os alertas de dados em um site do SharePoint no Gerenciador de Alertas de Dados](manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager.md)  
  
-   [Conceder permissões a usuários e administradores de alerta](grant-permissions-to-users-and-alerting-administrators.md)  
  
## <a name="see-also"></a>Consulte também  
 [Designer de Alertas de Dados](../../2014/reporting-services/data-alert-designer.md)   
 [Gerenciador de Alertas de dados para administradores de alertas](../../2014/reporting-services/data-alert-manager-for-alerting-administrators.md)   
 [Gerenciador de Alertas de Dados para Usuários do SharePoint](../../2014/reporting-services/data-alert-manager-for-sharepoint-users.md)  
  
  
