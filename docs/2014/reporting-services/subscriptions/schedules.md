---
title: Agendamentos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- schedules [Reporting Services]
- schedules [Reporting Services], about schedules
- published reports [Reporting Services], schedules
- reports [Reporting Services], scheduling
- subscriptions [Reporting Services], scheduling
- automatic report processing
ms.assetid: ecccd16b-eba9-4e95-b55d-f15c621e003f
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e0fe323460431750a6c79e181bda9e0173a31025
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56040837"
---
# <a name="schedules"></a>Agendamentos
  O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece agendas compartilhadas e específicas de relatório para ajudar a controlar o processamento e a distribuição de relatórios. A diferença entre os dois tipos de agendas é como elas são definidas, armazenadas e administradas. A construção interna dos dois tipos de agendas é a mesma. Todas as agendas especificam um tipo de recorrência: mensal, semanal ou diária. Dentro do tipo de recorrência, você define os intervalos e as faixas para a frequência com que um evento ocorre. O tipo de padrão de recorrência e a forma como ele é especificado são os mesmos para criar uma agenda compartilhada ou uma agenda específica de relatório.  
  
 Neste tópico:  
  
-   [O que você pode fazer com agendas](#bkmk_whatyoucando)  
  
-   [Comparando agendas compartilhadas e específicas de relatório](#bkmk_compare)  
  
-   [Configurar as fontes de dados](#bkmk_configuredatasources)  
  
-   [Store credenciais e contas de processamento](#bkmk_credentials)  
  
-   [Como a agenda e entrega funciona](#bkmk_how_scheduling_works)  
  
-   [Dependências de servidor](#bkmk_serverdependencies)  
  
-   [Efeitos de parar o SQL Server Agent](#bkmk_stoppingagent)  
  
-   [Efeitos de parar o serviço do servidor de relatório](#bkmk_stoppingservice)  
  
  
##  <a name="bkmk_whatyoucando"></a> O que você pode fazer com Agendas  
 Você pode usar o Gerenciador de Relatórios em modo Nativo e as páginas de administração do site do SharePoint no modo SharePoint para criar e gerenciar suas agendas. Você pode:  
  
-   Programar a entrega de relatórios em uma assinatura padrão ou controlada por dados.  
  
-   Programar o histórico de relatórios de modo que novos instantâneos sejam adicionados ao histórico de relatórios em intervalos regulares.  
  
-   Agendar quando os dados de um instantâneo de relatório devem ser atualizados.  
  
-   Agendar quando atualizar os dados de um conjunto de dados compartilhado  
  
-   Agendar a expiração de um relatório em cache ou conjunto de dados para ocorrer em um horário predefinido de modo que possa ser atualizada subsequentemente.  
  
 Você pode criar uma agenda compartilhada se desejar usar as mesmas informações de agenda para vários relatórios ou assinaturas. Os agendamentos compartilhados são definidos separadamente e então referenciados em relatórios, conjuntos de dados compartilhados e assinaturas que precisam de informações de agendamento.  
  
 Quando você cria uma agenda, o relatório salva as informações da agenda no banco de dados do servidor de relatório ou para o modo do SharePoint, o banco de dados de aplicativo de serviço. O servidor de relatório também cria um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usado para disparar a agenda. O processamento da agenda baseia-se no horário local do servidor de relatório que contém a agenda. O formato de hora segue o padrão do sistema operacional [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Para obter detalhes em como criar e gerenciar agendas, consulte [Create, Modify, and Delete Schedules](create-modify-and-delete-schedules.md).  
  
> [!NOTE]  
>  As operações de agenda não estão disponíveis em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Recursos com suporte nas edições do SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473).  
  
##  <a name="bkmk_compare"></a> Comparando agendas compartilhadas e específicas de relatório  
 Os dois tipos de agendas retornam o mesmo resultado:  
  
-   As**agendas compartilhadas** são itens portáteis e polivalentes que contêm informações de agenda prontas para uso. Como as agendas compartilhadas são itens no nível do sistema, criar uma agenda compartilhada requer permissões no nível do sistema. Por isso, um administrador de servidor de relatório ou gerenciador de conteúdo normalmente cria as agendas compartilhadas que estão disponíveis no seu servidor de relatório. As agendas compartilhadas são armazenadas e administradas no servidor de relatório usando configurações do Gerenciador de Relatórios ou do site do SharePoint.  
  
     Em comparação com agendas específicas que você define através de relatório, conjunto de dados compartilhado ou propriedades de assinatura, as agendas compartilhadas são mais fáceis de gerenciar e manter pelos seguintes motivos:  
  
    -   As agendas compartilhadas podem ser gerenciadas a partir de um local central, tornando mais fácil comparar as propriedades da agenda e ajustar os padrões de frequência e recorrência se as operações programadas estiverem sendo executadas muito juntas ou conflitando com outros processos no servidor.  
  
    -   Permitem a rápida adaptação a mudanças no ambiente computacional. Por exemplo, suponha que você tem um conjunto de relatórios que seja executado às 4h depois que um data warehouse é atualizado. Se a operação de atualização de dados for reprogramada ou atrasada, você poderá acomodar facilmente a mudança atualizando as informações de agenda em uma única agenda compartilhada.  
  
    -   Se você usar apenas agendas compartilhadas, você saberá precisamente quando as operações programadas ocorrerão. Isso torna mais fácil antecipar e acomodar as cargas de servidor antes que ocorram problemas de desempenho. Por exemplo, se você decidir programar backups de computador em um horário específico, você poderá ajustar agendas programadas para serem executadas em diferentes horários.  
  
-   As**agendas específicas do relatório** são definidas no contexto de um relatório individual, assinatura ou operação de execução de relatório para determinar a expiração de cache ou as atualizações de instantâneo. Essas agendas são criadas embutidas quando ao definir uma assinatura ou as propriedades de execução de relatório. É possível criar uma agenda específica de relatório se uma agenda compartilhada não fornecer o padrão de frequência ou de recorrência de que você precisa. Para impedir que um relatório seja executado, você deve editar uma agenda específica de relatório manualmente. As agendas específicas de relatório podem ser criadas por usuários individuais.  
  
##  <a name="bkmk_configuredatasources"></a> Configurar as fontes de dados  
 Para agendar o processamento de dados ou assinaturas para um relatório, você deve configurar a fonte de dados do relatório para que use credenciais armazenadas ou a conta de processamento de relatório autônoma. Se você usar credenciais armazenadas, só poderá armazenar um conjunto de credenciais e elas serão usadas por todos os usuários que executarem o relatório. As credenciais podem ser uma conta de usuário do Windows ou uma conta de usuário de banco de dados.  
  
 A conta de processamento de relatório autônoma é uma conta especial configurada no servidor de relatórios, que a usa para conectar-se com computadores remotos quando uma operação agendada requer processamento ou a recuperação de um arquivo externo. Se você configurar a conta, poderá usá-la para conectar-se a fontes de dados externas que fornecem dados para um relatório.  
  
 Para especificar credenciais armazenadas ou a conta de processamento de relatório autônoma, edite as propriedades da fonte de dados do relatório. Se o relatório usar uma fonte de dados compartilhados, edite a fonte de dados compartilhados.  
  
##  <a name="bkmk_credentials"></a> Armazenar credenciais e contas de processamento  
 O modo como você trabalha com uma agenda depende das tarefas que fazem parte de sua atribuição de função. Se você estiver usando funções predefinidas, os usuários que são Gerenciadores de Conteúdo e Administradores de Sistema podem criar e gerenciar qualquer agenda. Se atribuições de função personalizadas forem utilizadas, a atribuição de função deve incluir tarefas que ofereçam suporte para as operações agendadas.  
  
|Para fazer isso|Inclua esta tarefa|Funções predefinidas do modo nativo|Grupos do modo do SharePoint|  
|----------------|-----------------------|----------------------------------|----------------------------|  
|Criar, modificar ou excluir agendas compartilhadas|Gerenciar agendas compartilhadas|Administrador do Sistema|Proprietários|  
|Selecionar agendas compartilhadas|Exibir agendas compartilhadas|Usuário do Sistema|Membros|  
|Crie, modifique ou exclua agendas específicas do relatório em uma assinatura definida pelo usuário|Administrar assinaturas individuais|Navegador, Construtor de Relatórios, Meus Relatórios, Gerenciador de Conteúdo|Visitantes, membros|  
|Crie, modifique ou exclua agendas específicas do relatório para todas as outras operações agendadas|Gerenciar o histórico de relatório, gerenciar todas as assinaturas, gerenciar relatórios|Gerenciador de Conteúdo|Proprietários|  
  
 Para obter mais informações sobre a segurança no modo Nativo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Funções predefinidas](../security/role-definitions-predefined-roles.md), [Concedendo permissões em um Servidor de Relatório no modo Nativo](../security/granting-permissions-on-a-native-mode-report-server.md) e [Tarefas e Permissões](../security/tasks-and-permissions.md). Para o modo do SharePoint, consulte [Comparar funções e tarefas no Reporting Services com grupos e permissões do SharePoint](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)  
  
##  <a name="bkmk_how_scheduling_works"></a> Como o Processador de Agendamento e Entrega funciona  
 O Processador de Agendamento e Entrega fornece as seguintes funcionalidades:  
  
-   Mantém uma fila de eventos e notificações no banco de dados do servidor de relatório. Em uma implantação em expansão, a fila é compartilhada por todos os servidores de relatório na implantação.  
  
-   Chama o Processador de Relatório para executar relatórios, assinaturas de processo ou limpar um relatório armazenado em cache. Todo o processamento de relatório que ocorre como resultado de um evento de agendamento é executado como um processo em segundo plano. O modo do SharePoint utiliza trabalhos de timer para  
  
-   Chama a extensão de entrega que é especificada em uma assinatura para que o relatório possa ser entregue.  
  
 Os outros aspectos de uma operação de agendamento e entrega são tratados por outros componentes e serviços que trabalham com o Processador de Agendamento e Entrega. Mais especificamente, o Processador de Agendamento e Entrega é executado no serviço Servidor de Relatório e usa o SQL Server Agent como um temporizador para gerar eventos programados. A descrição passo a passo a seguir explica como as operações agendadas funcionam em uma implantação do Reporting Services:  
  
1.  Uma operação agendada é definida quando um usuário cria um agendamento. O agendamento define uma data e hora que serão usadas para disparar uma assinatura para entrega de relatório, atualizar um instantâneo ou expirar um cache.  
  
2.  O servidor de relatório salva as informações de agendamento no banco de dados do servidor de relatório.  
  
3.  O servidor de relatório cria um trabalho correspondente no SQL Server Agent que inclui as informações de agendamento fornecidas. Os trabalhos são criados por um procedimento armazenado, usando a conexão aberta existente com o banco de dados do servidor de relatório.  
  
4.  O SQL Server Agent executa o trabalho na data e hora especificadas no agendamento. O trabalho cria um evento que é adicionado a uma fila mantida pelo Reporting Services.  
  
5.  O evento faz com que um processo de relatório ou de assinatura ocorra. Os eventos são processados quando são detectados na fila, e o relatório é processado ou entregue adequadamente.  
  
     Antes que os eventos sejam processados, o Processador de Agendamento e Entrega executa uma etapa de autenticação para verificar se o proprietário da assinatura tem permissão para exibir o relatório.  
  
 O Reporting Services mantém uma fila de eventos para todas as operações agendadas. Ele pesquisa a fila em intervalos regulares para verificar novos eventos. Por padrão, a fila é digitalizada em intervalos de 10 segundos. Você pode alterar o intervalo modificando as definições de configuração `PollingInterval`, `IsNotificationService` e `IsEventService` no arquivo RSReportServer.config. O modo do SharePoint também usa o RSreporserver.config para obter estas configurações e os valores se aplicam a todos os aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md).  
  
##  <a name="bkmk_serverdependencies"></a> Dependências de servidor  
 O Processador de Agendamento e Entrega requer que o serviço Servidor de Relatório e o SQL Server Agent sejam iniciados. O recurso de processamento de agendamento e entrega deve ser habilitado por meio de `ScheduleEventsAndReportDeliveryEnabled` propriedade do **configuração da área de superfície do Reporting Services** faceta no gerenciamento baseado em políticas. O SQL Server Agent e o serviço Servidor de Relatório devem ser executados para que as operações agendadas ocorram.  
  
> [!NOTE]  
>  É possível usar a faceta **Configuração da Área da Superfície do Reporting Services** para parar as operações agendadas em uma base temporária ou permanente. Embora você possa criar e implantar extensões de entrega personalizadas, em si, o Processador de Agendamento e Entrega não é extensível. Não é possível alterar a forma como ele gerencia eventos e notificações. Para obter mais informações sobre volta fora recursos, consulte a seção **Eventos e entrega agendados** de [Turn Reporting Services Features On or Off](../report-server/turn-reporting-services-features-on-or-off.md).  
  
###  <a name="bkmk_stoppingagent"></a> Efeitos de parar o SQL Server Agent  
 O processamento de relatórios agendado usa o SQL Server Agent por padrão. Se você parar o serviço, nenhuma nova solicitação de processamento será adicionada à fila, a menos que seja adicionada programaticamente através do método <xref:ReportService2010.ReportingService2010.FireEvent%2A> . Quando você reinicializa o serviço, os trabalhos que criam solicitações de processamento de relatório são reiniciados. O servidor de relatório não tenta recriar os trabalhos de processamento de relatório que possam ter ocorrido anteriormente quando o SQL Server Agent estava offline. Se você parar o SQL Server Agent por uma semana, todas as operações agendadas nessa semana serão perdidas.  
  
> [!NOTE]  
>  A funcionalidade que o SQL Server Agent fornece ao Reporting Services pode ser substituída pelo código personalizado que usa o método <xref:ReportService2010.ReportingService2010.FireEvent%2A> para adicionar eventos de agendamento à fila.  
  
###  <a name="bkmk_stoppingservice"></a> Efeitos de parar o serviço Servidor de Relatório  
 Se você parar o serviço Servidor de Relatório, o SQL Server Agent continuará a adicionar solicitações de processamento de relatório à fila. As informações de status do SQL Server Agent indicam que o trabalho teve êxito. Porém, como o serviço Servidor de Relatório foi interrompido, nenhum processamento de relatório realmente ocorre. As solicitações continuarão a acumular na fila até que o serviço Servidor de Relatório seja reiniciado. Quando o serviço Servidor de Relatório é reiniciado, todas as solicitações de processamento de relatório que estão na fila são processadas.  
  
## <a name="see-also"></a>Consulte também  
 [Criar, modificar e excluir instantâneos no histórico de relatório](../report-server/create-modify-and-delete-snapshots-in-report-history.md)   
 [Assinaturas e entrega &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [Data-Driven Subscriptions](data-driven-subscriptions.md)   
 [Armazenando relatórios em cache &#40;SSRS&#41;](../report-server/caching-reports-ssrs.md)   
 [Gerenciamento do conteúdo do Servidor de Relatório &#40;Modo Nativo do SSRS&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [Conjuntos de dados compartilhados em cache &#40;SSRS&#41;](../report-server/cache-shared-datasets-ssrs.md)  
  
  
