---
title: Gerenciar um processo em execução | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- report processing [Reporting Services], status information
- jobs [Reporting Services]
- viewing jobs
- canceling jobs
- user jobs [Reporting Services]
- system jobs [Reporting Services]
- report processing [Reporting Services], managing running processes
- processes [Reporting Services]
- scanning processes [Reporting Services]
- status information [Reporting Services]
- report processing [Reporting Services]
- canceling subscriptions
- report servers [Reporting Services], jobs
- data-driven subscriptions
- displaying jobs
- subscriptions [Reporting Services], running processes
ms.assetid: 473e574e-f1ff-4ef9-bda6-7028b357ac42
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6eeec8517b9b55e30eb51abc25fefed0b36b2a79
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65579011"
---
# <a name="manage-a-running-process"></a>Manage a Running Process
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] monitora o status dos trabalhos que estão em execução no servidor de relatório. Em intervalos regulares, o servidor de relatório examina os trabalhos em andamento e grava as informações de status no banco de dados do servidor de relatório ou os bancos de dados de aplicativo de serviço para o modo do SharePoint. Um trabalho está em andamento se algum dos seguintes processos estiver ocorrendo: execução de consulta em um servidor de banco de dados remoto ou local, processamento de relatórios e renderização de relatórios.  
  
 Você pode gerenciar *trabalhos de usuário* e *trabalhos de sistema*.  
  
-   Os trabalhos de usuário são iniciados por um usuário individual ou uma assinatura. Isso inclui a execução de um relatório sob demanda, a solicitação de um instantâneo de histórico de relatórios, a criação manual de um instantâneo de relatório e o processamento de uma assinatura padrão.  
  
-   Os trabalhos de sistema são iniciados pelo servidor de relatório. Os trabalhos de sistema incluem instantâneos de execução de relatório agendados, instantâneos de histórico de relatórios agendados e assinaturas controladas por dados.  
  
 O tempo de processamento do relatório e o uso de recursos variam significativamente dependendo do relatório, da complexidade da consulta, da quantidade de dados e o do formato de renderização especificado para o relatório. Os relatórios que têm consultas simples em comparação a uma fonte de dados local normalmente são concluídos em milissegundos e nunca requerem gerenciamento ou ajuste. Por outro lado, um grande relatório que é renderizado em PDF ou Excel pode exigir um tempo de processamento significativo dependendo dos recursos de hardware, das opções de entrega e da execução simultânea de outros processos. Em um servidor de relatórios, a maioria dos processos de execução demorada corresponde às operações de renderização de relatório e aos processos que estão aguardando a conclusão do processamento da consulta. Ocasionalmente, você talvez precise cancelar o processamento de um relatório se desejar deixar o computador offline ou parar um trabalho cuja execução está demorando muito para terminar.  
  
 Os processos a seguir podem ser cancelados:  
  
-   Processamento de relatórios sob demanda.  
  
-   Processamento agendado de relatórios.  
  
-   Assinaturas padrão de propriedade de usuários individuais.  
  
 O cancelamento de um trabalho só cancela os processos que estão em execução no servidor de relatório. Como o servidor de relatório não gerencia o processamento de dados que ocorre em outros computadores, cancele manualmente os processamentos de consulta que, consequentemente, ficam órfãos em outros sistemas. Especifique valores de tempo limite de consulta para desligar automaticamente consultas que estão demorando muito a serem executadas. Para obter mais informações, consulte [Definindo valores de tempo limite para processamento de relatórios e conjuntos de dados compartilhados &#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md). Para obter mais informações sobre como pausar temporariamente um relatório, consulte [Desabilitar ou pausar o processamento de relatório e de assinatura](../../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md).  
  
> [!NOTE]  
>  Em circunstâncias raras, você talvez precise reinicializar o servidor para cancelar um processo. No modo do SharePoint, talvez seja necessário reiniciar o pool de aplicativos hospedando o aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [Iniciar e parar o serviço Servidor de Relatório](../../reporting-services/report-server/start-and-stop-the-report-server-service.md).  
  
 Neste tópico:  
  
-   [Exibir e cancelar trabalhos (modo nativo)](#bkmk_native)  
  
-   [Exibir e cancelar trabalhos (modo do SharePoint)](#bkmk_sharepoint)  
  
-   [Gerenciando trabalhos programaticamente](#bkmk_programmatically)  
  
##  <a name="view-and-cancel-jobs-native-mode"></a><a name="bkmk_native"></a> Exibir e cancelar trabalhos (modo nativo)  
 Você pode usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para ver ou cancelar um trabalho que está em execução no servidor de relatório. Atualize a página para recuperar uma lista dos trabalhos que estão em execução no momento ou para obter o status atualizado do trabalho do banco de dados do servidor de relatório. Ao se conectar a um servidor de relatório no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], você pode abrir uma pasta Trabalhos para exibir uma lista dos relatórios que estão sendo processados atualmente no computador do servidor de relatório. As informações de status de cada trabalho são exibidas na página Propriedades do Trabalho. Você pode exibir as informações de status de todos os trabalhos abrindo a caixa de diálogo Cancelar Trabalhos do Servidor de Relatório.  
  
 Você pode usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para ver ou cancelar um trabalho que está em execução no servidor de relatório. Atualize a página para recuperar uma lista dos trabalhos que estão em execução no momento ou para obter o status atualizado do trabalho do banco de dados do servidor de relatório. Ao se conectar a um servidor de relatório no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], você pode abrir uma pasta Trabalhos para exibir uma lista dos relatórios que estão sendo processados atualmente no computador do servidor de relatório. As informações de status de cada trabalho são exibidas na página Propriedades do Trabalho. Você pode exibir as informações de status de todos os trabalhos abrindo a caixa de diálogo Cancelar Trabalhos do Servidor de Relatório.  
  
 Não é possível usar o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para listar ou cancelar a geração de modelos, o processamento de modelos ou assinaturas controladas por dados. O Reporting Services não permite cancelar a geração ou o processamento de modelos. Porém, você pode cancelar assinaturas controladas por dados usando as instruções fornecidas neste tópico.  
  
### <a name="how-to-cancel-report-processing-or-subscription"></a>Como cancelar assinaturas ou o processamento de relatórios  
  
1.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], conecte-se ao servidor de relatório. Para obter instruções, consulte [Conectar-se a um Servidor de Relatório no Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md).  
  
2.  Abra a pasta **Trabalhos** .  
  
3.  Clique com o botão direito do mouse no relatório e clique em **Cancelar Trabalhos**.  
  
### <a name="how-to-cancel-a-data-driven-subscription"></a>Como cancelar uma assinatura controlada por dados  
  
1.  Abra o arquivo RSReportServer.config em um editor de texto.  
  
2.  Localize **IsNotificationService**.  
  
3.  Defina-o como **False**.  
  
4.  Salve o arquivo.  
  
5.  No Gerenciador de Relatórios, exclua a assinatura controlada por dados da guia Assinaturas do relatório ou em **Minhas Assinaturas**.  
  
6.  Depois de excluir a assinatura, no arquivo RSReportServer.config, localize **IsNotificationService** e defina como **True**.  
  
7.  Salve o arquivo.  
  
### <a name="configuring-frequency-settings-for-retrieving-job-status"></a>Definindo configurações de frequência para recuperar o status do trabalho  
 Um trabalho em execução é armazenado no banco de dados temporário do servidor de relatório. Você pode modificar as configurações do arquivo RSReportServer.config para controlar a frequência em que o servidor de relatório examina trabalhos em andamento e o intervalo após o qual o status de um trabalho em execução muda de “novo” para “em execução”. A configuração **RunningRequestsDbCycle** especifica com que frequência o servidor de relatório examina processos em execução. Por padrão, as informações de status são registradas a cada 60 segundos. A configuração **RunningRequestsAge** especifica o intervalo em que um trabalho passa de “novo” para “em execução”.  
  
##  <a name="view-and-cancel-jobs-sharepoint-mode"></a><a name="bkmk_sharepoint"></a> Exibir e cancelar trabalhos (modo do SharePoint)  
 O gerenciamento de trabalhos em uma implantação no modo do SharePoint é realizado por meio da Administração Central do SharePoint, para cada aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
#### <a name="to-manage-jobs-in-sharepoint-mode"></a>Para gerenciar trabalhos no modo do SharePoint  
  
1.  Na Administração Central do SharePoint, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Localize e clique no nome do seu aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para abrir a página de gerenciamento de aplicativos.  
  
3.  Clique em **Gerenciar Trabalhos**.  
  
4.  Clique na **ID do Trabalho** para ver os detalhes do trabalho.  
  
5.  Ou clique na caixa do seu trabalho e clique em **Excluir** para cancelar o trabalho. Excluir o trabalho não exclui a assinatura.  
  
##  <a name="managing-jobs-programmatically"></a><a name="bkmk_programmatically"></a> Gerenciando trabalhos programaticamente  
 Você pode gerenciar trabalhos programaticamente ou usando um script. Para obter mais informações, consulte <xref:ReportService2010.ReportingService2010.ListJobs%2A>e <xref:ReportService2010.ReportingService2010.CancelJob%2A>.  
  
## <a name="see-also"></a>Consulte Também  
 [Cancelar Trabalhos do Servidor de Relatório &#40;Management Studio&#41;](../../reporting-services/tools/cancel-report-server-jobs-management-studio.md)   
 [Propriedades do trabalho &#40;Management Studio&#41;](../../reporting-services/tools/job-properties-management-studio.md)   
 [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Monitorar o desempenho do servidor de relatório](../../reporting-services/report-server/monitoring-report-server-performance.md)  
  
  
