---
title: "Solucionar problemas de relat&#243;rio do Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
  - "reporting-services-sharepoint"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a705d103-85b1-49b5-b27f-332b1040d029
caps.latest.revision: 9
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 9
---
# Solucionar problemas de relat&#243;rio do Reporting Services
Este tópico ajuda você a solucionar problemas com design de relatório [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)], visualização de um relatório, publicação de um relatório em um servidor de relatório em modo nativo ou em modo SharePoint, exibindo um relatório no servidor de relatório ou exportando um relatório para um formato de arquivo diferente.  
## Monitorar Servidores de Relatório  
Você pode usar ferramentas de sistema e de banco de dados para monitorar a atividade do servidor de relatório. Você também pode exibir arquivos de log de rastreamento do servidor de relatório ou consultar o log de execução do servidor de relatório para obter informações detalhadas sobre relatórios específicos. Se estiver usando o Monitor de Desempenho, você poderá adicionar contadores de desempenho para o serviço Web Servidor de Relatórios e o serviço do Windows para identificar afunilamentos em processamentos sob demanda ou agendados.  
Para obter mais informações, consulte [Monitoramento do Desempenho do Servidor de Relatório](../../reporting-services/report-server/monitoring-report-server-performance.md).  
  
  
## Exibir os Logs do Servidor de Relatório  
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] registra muitos eventos internos e externos em arquivos de log que gravam dados sobre relatórios específicos, informações de depuração, solicitações HTTP e respostas, e eventos do servidor de relatório. Você também pode criar logs de desempenho e selecionar contadores de desempenho que especificam quais dados devem ser coletados. O diretório padrão para arquivos de log de uma instalação padrão é `<drive>\Program Files\Microsoft SQL Server\MSRS130.MSSQLSERVER\Reporting Services\LogFiles`.   
  
Para obter mais informações, consulte [Fontes e arquivos de log do Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
Para determinar especificamente se as esperas de relatório se devem à recuperação de dados, ao processamento de relatório ou à renderização de relatório, use to Log de Execução. Para obter mais informações, consulte [ExecutionLog do Servidor de Relatório e a exibição do ExecutionLog3].   
  
## Exibir a pilha de chamadas para mensagens de erro de processamento de relatório no Servidor de Relatório  
Quando exibe um relatório publicado no Gerenciador de Relatórios, pode ver uma mensagem de erro que representa um erro de processamento ou renderização geral. Para visualizar mais informações, exiba a pilha de chamadas.   
  
Para exibir a pilha de chamadas, faça logon no servidor de relatório usando as credenciais de administrador local, clique com o botão direito do mouse na página Gerenciador de Relatórios e clique em**Exibir origem**. A pilha de chamadas fornece contexto detalhado para a mensagem de erro.  
  
## Usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull.md)] para Verificar Consultas e Credenciais  
Use essa o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull.md)] para validar consultas complexas antes de incluí-las no relatório.   
  
Para obter mais informações, consulte [Editor de consultas do Mecanismo de Banco de Dados](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md) e [Gerenciar Objetos Usando o Pesquisador de Objetos](../../ssms/object/manage-objects-by-using-object-explorer.md).  
  
## Analisar relatórios de problemas com dados de relatório em cache no cliente  
Quando um autor de relatório cria um relatório no Business Intelligence Development Studio, o cliente de criação armazena em cache os dados como um arquivo de dados .rdl, que é usado quando você visualiza um relatório. Sempre que a consulta é alterada, o cache é atualizado. Para depurar problemas de relatório, às vezes, é útil evitar a atualização dos dados do relatório, para que eles não sejam alterados quando você estiver depurando.   
  
Para controlar se o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull.md)] só pode usar dados de cache, adicione a seção a seguir ao arquivo devenv.exe.config no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio.md)]. O local do diretório padrão é: `<drive>:Program Files\Microsoft Visual Studio 10.0\Common7\IDE`.   
  
```  
<system.diagnostics>  
      <switches>  
         <add name="Microsoft.ReportDesigner.ReportPreviewStore.ForceCache" value="1" />  
      </switches>  
   </system.diagnostics>  
```  
Desde que o valor seja definido como 1, somente dados de relatório em cache são usados. Não se esqueça de remover esta seção quando terminar de depurar o relatório.  
  
## Consulte também  
[Erros e eventos (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]
