---
title: Reporting Services com Grupos de Disponibilidade AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: edeb5c75-fb13-467e-873a-ab3aad88ab72
author: MashaMSFT
ms.author: mathoma
manager: erikre
ms.openlocfilehash: 52e7bd927c8b3df503b335b522ca8b3444f5f5fe
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830904"
---
# <a name="reporting-services-with-always-on-availability-groups-sql-server"></a>Reporting Services com grupos de disponibilidade AlwaysOn (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico contém informações sobre como configurar o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para funcionar com o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] (AG) no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Os três cenários para usar o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] são bancos de dados para fontes de dados de relatório, bancos de dados do servidor de relatório e design de relatório. A funcionalidade com suporte e a configuração exigida é diferente para os três cenários.  
  
 O principal benefício de usar o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] com fontes de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] é aproveitar réplicas secundárias legíveis como uma fonte de dados de relatório enquanto, ao mesmo tempo, as réplicas secundárias estão fornecendo um failover para um banco de dados primário.  
  
 Para obter informações gerais sobre o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [Perguntas frequentes sobre o Always On do SQL Server 2012 (http://msdn.microsoft.com/sqlserver/gg508768)](http://msdn.microsoft.com/sqlserver/gg508768)).  
  
 **Neste tópico:**  
  
-   [Requisitos para usar o Reporting Services e os grupos de disponibilidade AlwaysOn](#bkmk_requirements)  
  
-   [Fontes de dados de relatório e grupos de disponibilidade](#bkmk_reportdatasources)  
  
-   [Design de relatório e grupos de disponibilidade](#bkmk_reportdesign)  
  
-   [Bancos de dados do servidor de relatório e grupos de disponibilidade](#bkmk_reportserverdatabases)  
  
-   -   [Diferenças entre o modo nativo do SharePoint](#bkmk_differences_in_server_mode)  
  
    -   [Preparar os bancos de dados do servidor de relatório para grupos de disponibilidade](#bkmk_prepare_databases)  
  
    -   [Etapas para concluir a recuperação de bancos de dados do servidor de relatório](#bkmk_steps_to_complete_failover)  
  
    -   [Comportamento do servidor de relatório quando ocorre um failover](#bkmk_failover_behavior)  
  
##  <a name="bkmk_requirements"></a> Requisitos para usar o Reporting Services e os grupos de disponibilidade AlwaysOn  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e o Servidor de Relatórios do Power BI usa o .Net Framework 4.0 e dá suporte às propriedades de cadeia de conexão do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] para uso com fontes de dados.  
  
 Para usar o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] com o  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 2014 e anteriores, você precisa baixar e instalar um hotfix para .NET 3.5 SP1. O hotfix adiciona suporte a Cliente SQL para os recursos do AG e suporte das propriedades da cadeia de conexão **ApplicationIntent** e **MultiSubnetFailover**. Se o Hotfix não estiver instalado em cada computador que hospeda um servidor de relatório, os usuários que tentarem visualizar relatórios verão uma mensagem de erro semelhante à seguinte, e a mensagem de erro será gravada no log de rastreamento do servidor de relatório:  
  
> **Mensagem de erro:** "Palavra-chave sem suporte 'applicationintent'"  
  
 A mensagem ocorre quando você inclui uma das propriedades do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] na cadeia de conexão do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] , mas o servidor não reconhece a propriedade. A mensagem de erro destacada será vista quando você clicar no botão 'Testar Conexão' nas interfaces de usuário do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e quando você visualizar o relatório se os erros remotos estiverem habilitados nos servidores de relatórios.  
  
 Para obter mais informações sobre o hotfix necessário, veja [o hotfix da KB 2654347A introduz suporte para os recursos AlwaysOn do SQL Server 2012 no .NET Framework 3.5 SP1](http://go.microsoft.com/fwlink/?LinkId=242896).  
  
 Para obter informações sobre outros requisitos do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], veja [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
> [!NOTE]  
>  Não há suporte para arquivos de configuração do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] como **RSreportserver.config**, como parte da funcionalidade do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Se você fizer alterações manualmente em um arquivo de configuração em um dos servidores de relatórios, precisará atualizar as réplicas manualmente.  
  
##  <a name="bkmk_reportdatasources"></a> Fontes de dados de relatório e grupos de disponibilidade  
 O comportamento de fontes de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] com base no [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] pode variar, dependendo de como o administrador configurou o ambiente do AG.  
  
 Para utilizar o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] para fontes de dados de relatório, você precisará configurar a cadeia de conexão da fonte de dados de relatório para usar o *Nome DNS do Ouvinte*do grupo de disponibilidade. As fontes de dados com suporte são as seguintes:  
  
-   Fontes de dados ODBC usando SQL Native Client.  
  
-   SQL Client, com o hotfix .Net aplicado ao servidor de relatório.  
  
 A cadeia de conexão também pode conter novas propriedades de conexão AlwaysOn que configuram as solicitações de consulta de relatório para usar a réplica secundária para relatório somente leitura. O uso de réplica secundária para solicitações de relatório reduzirá a carga em uma réplica primária de leitura/gravação. A ilustração a seguir é um exemplo de uma configuração de três réplicas de AG onde as cadeias de conexão da fonte de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] foram configuradas com ApplicationIntent=ReadOnly. Neste exemplo, as solicitações de consulta de relatório são enviadas para uma réplica secundária e não para a réplica primária.  
  
 
  
 Veja a seguir uma cadeia de conexão de exemplo, em que o [AvailabilityGroupListenerName] é o **Nome DNS do Ouvinte** que foi configurado quando as réplicas foram criadas:  
  
 `Data Source=[AvailabilityGroupListenerName];Initial Catalog = AdventureWorks2016; ApplicationIntent=ReadOnly`  
  
 O botão **Testar Conexão** em interfaces de usuário do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] validará se uma conexão puder ser estabelecida, mas não validará a configuração do AG. Por exemplo, se você incluir ApplicationIntent em uma cadeia de conexão para um servidor que não faça parte do AG, o parâmetro adicional será ignorado e o botão **Testar Conexão** somente validará uma conexão que puder ser estabelecida com o servidor especificado.  
  
 Dependendo de como seus relatórios são criados e publicados, isso determinará onde você editará a cadeia de conexão:  
  
-   **Modo nativo:** use o [!INCLUDE[ssRSWebPortal-Non-Markdown](../../../includes/ssrswebportal-non-markdown-md.md)] para fontes de dados compartilhadas e relatórios que já estão publicados em um servidor de relatório de modo nativo.  
  
-   **Modo do SharePoint:** Use as páginas de configuração do SharePoint dentro das bibliotecas de documentos para relatórios que já estão publicados em um servidor do SharePoint.  
  
-   **Design de relatórios:** [!INCLUDE[ssRBnoversion](../../../includes/ssrbnoversion.md)] ou [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] quando você está criando novos relatórios. Consulte a seção 'Design de relatórios' neste tópico ou em mais informações.  
  
 **Recursos adicionais:**  
  
-   [Gerenciar fontes de dados de relatório](../../../reporting-services/report-data/manage-report-data-sources.md)  
  
-   Para obter mais informações sobre as propriedades da cadeia de conexão disponíveis, consulte [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
-   Para obter mais informações sobre ouvintes do grupo de disponibilidade, veja [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
 **Considerações:** as réplicas Secundárias normalmente experimentarão um atraso ao receber alterações de dados da réplica primária. Os fatores a seguir podem afetar a latência da atualização entre as réplicas primárias e secundárias:  
  
-   O número de réplicas secundárias. O atraso aumenta com cada réplica secundária adicionada à configuração.  
  
-   A localização geográfica e a distância entre as réplicas primárias e secundárias. Por exemplo, o atraso será geralmente maior se as réplicas secundárias estiverem em um data center diferente do que se estivessem no mesmo prédio que a réplica primária.  
  
-   Configuração do modo de disponibilidade para cada réplica. O modo de disponibilidade determina se a réplica primária espera para confirmar transações em um banco de dados até que uma réplica secundária tenha gravado a transação em disco. Para obter mais informações, confira a seção “Modos de disponibilidade” de [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
 Ao usar uma réplica secundária somente leitura como uma fonte de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] , é importante verificar se a latência de atualização de dados atende as necessidades dos usuários de relatório.  
  
##  <a name="bkmk_reportdesign"></a> Design de relatório e grupos de disponibilidade  
 Ao criar relatórios no [!INCLUDE[ssRBnoversion](../../../includes/ssrbnoversion.md)] ou um projeto de relatório no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], um usuário poderá configurar uma cadeia de conexão da fonte de dados de relatório para conter novas propriedades de conexão fornecidas pelo [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. O suporte para as novas propriedades de conexão depende de onde o usuário visualiza o relatório.  
  
-   **Visualização local:** [!INCLUDE[ssRBnoversion](../../../includes/ssrbnoversion.md)] e o [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] usam o .NET Framework 4.0 e dão suporte às propriedades de cadeia de conexão do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .  
  
-   **Visualização de modo remoto ou de servidor:** se, depois de publicar relatórios no servidor de relatório ou usar a visualização no [!INCLUDE[ssRBnoversion](../../../includes/ssrbnoversion.md)], você vir um erro semelhante ao mostrado a seguir, isso será uma indicação de que você está visualizando relatórios no servidor de relatório e no Hotfix do .NET Framework 3.5 SP1 porque o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] não foi instalado no servidor de relatório.  
  
> **Mensagem de erro:** "Palavra-chave sem suporte 'applicationintent'"  
  
##  <a name="bkmk_reportserverdatabases"></a> Bancos de dados do servidor de relatório e grupos de disponibilidade  
 O Reporting Services e o Servidor de Relatórios do Power BI oferece suporte limitado para usar o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] com bancos de dados do servidor de relatório. Os bancos de dados do servidor de relatórios podem ser configurados no AG para fazer parte de uma réplica; porém, o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] não usará automaticamente uma réplica diferente para os bancos de dados do servidor de relatório quando um failover ocorrer. Não há suporte para o uso de MultiSubnetFailover com os bancos de dados do servidor de relatório.  
  
 Ações manuais ou scripts de automação personalizados precisam ser usados para concluir o failover e a recuperação. Até que estas ações sejam concluídas, alguns recursos do servidor de relatório poderão não funcionar corretamente depois do failover do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .  
  
> [!NOTE]  
>  Ao planejar failover e recuperação de desastres para os bancos de dados do servidor de relatório, é sempre recomendável fazer backup de uma cópia da chave de criptografia do servidor de relatório.  
  
###  <a name="bkmk_differences_in_server_mode"></a> Diferenças entre o modo nativo do SharePoint  
 Esta seção resume as diferenças entre o modo com o SharePoint e os servidores de relatórios de modo nativo interagem com o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].  
  
 Um servidor de relatório do SharePoint cria **3** bancos de dados para cada aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] criado. A conexão para bancos de dados do servidor de relatório no modo do SharePoint é configurada na Administração Central do SharePoint quando você cria o aplicativo de serviço. Os nomes padrão dos bancos de dados incluem um GUID que está associado com o aplicativo de serviço. A seguir são apresentados nomes de bancos de dados de exemplo para o servidor de relatório do modo do SharePoint:  
  
-   ReportingService_85c08ac3c8e64d3cb400ad06ed5da5d6  
  
-   ReportingService_85c08ac3c8e64d3cb400ad06ed5da5d6TempDB  
  
-   ReportingService_85c08ac3c8e64d3cb400ad06ed5da5d6_Alerting  
  
 Os servidores de relatórios de modo nativo usam **2** bancos de dados. A seguir são apresentados nomes de bancos de dados de exemplo para o servidor de relatório do modo nativo:  
  
-   ReportServer  
  
-   ReportServerTempDB  
  
 O modo nativo não dá suporte nem usa os bancos de dados de alertas e recursos relacionados. Configure os servidores de relatório de modo nativo no Configuration Manager do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . Para o modo do SharePoint, configure o nome do banco de dados de aplicativo de serviço para ser o nome do "ponto de acesso para cliente" que você criou como parte da configuração do SharePoint. Para obter mais informações sobre como configurar o SharePoint com o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [Configurar e gerenciar grupos de disponibilidade do SQL Server para o SharePoint Server (http://go.microsoft.com/fwlink/?LinkId=245165)](http://go.microsoft.com/fwlink/?LinkId=245165)).  
  
> [!NOTE]  
>  Os servidores de relatórios do modo do SharePoint usam um processo de sincronização entre os bancos de dados de aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e os bancos de dados de conteúdo do SharePoint. É importante manter os bancos de dados do servidor de relatório e os bancos de dados de conteúdo juntos. Configure-os nos mesmos grupos de disponibilidade para que eles realizem failover e recuperação como um conjunto. Considere o cenário a seguir.  
>   
>  -   Você restaura ou realiza failover para uma cópia do banco de dados de conteúdo que não tenha recebido as mesmas atualizações recentes que o banco de dados do servidor de relatório.  
> -   O processo de sincronização do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] detectará diferenças entre a lista de itens no banco de dados de conteúdo e os bancos de dados do servidor de relatório.  
> -   O processo de sincronização excluirá ou atualizará itens no banco de dados de conteúdo.  
  
###  <a name="bkmk_prepare_databases"></a> Preparar os bancos de dados do servidor de relatório para grupos de disponibilidade  
 Veja a seguir as etapas básicas de preparar e adicionar os bancos de dados do servidor de relatório para um [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]:  
  
-   Crie seu Grupo de disponibilidade e configure um *Nome DNS do Ouvinte*.  
  
-   **Réplica primária:** configure os bancos de dados do servidor de relatório para fazerem parte de um único grupo de disponibilidade e para criarem uma réplica primária que inclui todos os bancos de dados do servidor de relatório.  
  
-   **Réplicas secundárias:** crie uma ou mais réplicas secundárias. A abordagem comum para copiar os bancos de dados da réplica primária para a réplica secundária é restaurar os bancos de dados para cada réplica secundária usando 'RESTORE WITH NORECOVERY.' Para obter mais informações sobre como criar réplicas secundárias e verificar se a sincronização de dados está funcionando, veja [Iniciar movimentação de dados em um banco de dados secundário &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
-   **Credenciais de Servidor de relatório:** você precisa criar as credenciais de servidor de relatório apropriados nas réplicas secundárias que você criou na réplica primária. As etapas exatas dependem de que tipo de autenticação você está usando em seu ambiente do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]; conta de serviço do Windows [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], conta de usuário do Windows ou autenticação do SQL Server. Para obter mais informações, veja [Configurar uma conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
-   Atualize a conexão de banco de dados para usar o Nome DNS do Ouvinte. para os servidores de relatórios do modo de nativo, altere o **Nome do Banco de Dados do Servidor de Relatório** no gerenciador de configuração do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . Para o modo do SharePoint, altere o **Nome do servidor de banco de dados** para o aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .  
  
###  <a name="bkmk_steps_to_complete_failover"></a> Etapas para concluir a recuperação de bancos de dados do servidor de relatório  
 As etapas a seguir precisam ser concluídas depois de um failover do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] para uma réplica secundária:  
  
1.  Pare a instância do serviço SQL Agent que estava sendo usado pelo mecanismo de banco de dados primário que hospeda os bancos de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .  
  
2.  Inicie o serviço SQL Agent no computador que é a nova réplica primária.  
  
3.  Pare o serviço do servidor de relatório.  
  
     Se o servidor de relatório estiver em modo nativo, pare o servidor de relatório do servidor do Windows usando o gerenciador de configuração do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .  
  
     Se o servidor de relatório estiver configurado para o modo do SharePoint, pare o serviço compartilhado do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] na Administração Central do SharePoint.  
  
4.  Inicie o serviço do servidor de relatório ou serviço do SharePoint do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .  
  
5.  Verifique se os relatórios podem ser executar na nova réplica primária.  
  
###  <a name="bkmk_failover_behavior"></a> Comportamento do servidor de relatório quando ocorre um failover  
 Quando ocorre o failover de bancos de dados do servidor de relatório e você atualizou o ambiente do servidor de relatório para usar a nova réplica primária, há alguns problemas operacionais que resultam do failover e do processo de recuperação. O impacto destes problemas poderá variar, dependendo da carga do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] na hora de failover e também do período de tempo que ele leva para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] realizar failover para uma réplica secundária e para o administrador do servidor de relatório atualizar o ambiente de relatório para usar a nova réplica primária.  
  
-   A execução do processamento em segundo plano pode ocorrer mais de uma vez devido à lógica de repetição e a incapacidade de o servidor de relatório marcar trabalho agendado como concluído durante o período de failover.  
  
-   A execução do processamento em segundo plano que normalmente deveria ter sido disparado para ser executado durante o período do failover não ocorrerá porque o SQL Server Agent não poderá gravar dados no banco de dados do servidor de relatório e estes dados não serão sincronizados na nova réplica primária.  
  
-   Depois que o failover de banco de dados tiver sido concluído e depois que o serviço de servidor de relatório tiver sido reiniciado, os trabalhos do SQL Server Agent serão recriados automaticamente. Até que os trabalhos do SQL Agent tiverem sido recriados, não será processada nenhuma execução em segundo plano associada aos trabalhos do SQL Server Agent. Isto inclui assinaturas do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] , agendas e instantâneos.  
  
## <a name="see-also"></a>Consulte Também  
 [Suporte do SQL Server Native Client à alta disponibilidade e recuperação de desastre](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)   
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Introdução aos Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/getting-started-with-always-on-availability-groups-sql-server.md)   
 [Usando palavras-chave da cadeia de conexão com o SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)   
 [Suporte do SQL Server Native Client à alta disponibilidade e recuperação de desastre](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)   
 [Sobre o acesso de conexão de cliente a réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)  
  
  

