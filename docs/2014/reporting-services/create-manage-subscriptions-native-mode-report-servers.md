---
title: Criar e gerenciar assinaturas de servidores de relatório no modo Nativo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], managing
ms.assetid: 7f46cbdb-5102-4941-bca2-5e0ff9012c6b
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 44bf77f23724f51ddc75f708e5663b43e607df0e
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56023907"
---
# <a name="create-and-manage-subscriptions-for-native-mode-report-servers"></a>Crie e gerencie assinaturas de servidores de relatório no modo Nativo
  Esta seção contém tópicos sobre processamento, omissão e controle de assinaturas. O gerenciamento de assinaturas varia para assinaturas padrão e assinaturas controladas por dados. As assinaturas padrão normalmente são de propriedade e gerenciadas pelo usuário. Por outro lado, as assinaturas controladas por dados normalmente são criadas e mantidas por um administrador de servidor de relatório.  
  
 Os recursos de assinatura e entrega são habilitados por padrão (a entrega de email deve ser configurada antes de ser usada). As extensões de entrega padrão incluem a entrega de email de servidor de relatório e de compartilhamento de arquivos. A não ser que você crie ou instale extensões de entrega personalizadas, esses são os únicos métodos de distribuição disponíveis para assinaturas em um servidor de relatório no modo nativo.  
  
## <a name="permissions-for-subscribing-to-reports-on-a-native-mode-report-server"></a>Permissões para assinar relatórios em um servidor de relatório no modo nativo  
 Dependendo de como as funções forem usadas, você pode fornecer o recurso de assinatura para alguns grupos de usuários habilitando ou desabilitando tarefas de assinatura para diferentes funções. Os recursos de assinatura estão disponíveis aos usuários por meio de duas tarefas:  
  
-   A tarefa “Gerenciar assinaturas individuais” permite que os usuários criem, modifiquem e excluam assinaturas para um relatório específico. Nas funções predefinidas, essa tarefa faz parte das funções Navegador e Construtor de Relatórios. As atribuições de função que incluem essa tarefa permitem que um usuário gerencie somente as assinaturas que ele cria.  
  
-   A tarefa “Gerenciar todas as assinaturas” permite que os usuários acessem e modifiquem todas as assinaturas. Essa tarefa é obrigatória para criar assinaturas controladas por dados. Em funções predefinidas, a função Gerenciador de Conteúdo inclui essa tarefa.  
  
## <a name="disabling-subscriptions"></a>Desabilitando assinaturas  
 Para impedir que os usuários criem assinaturas, desmarque a tarefa “Gerenciar assinaturas individuais” da função. Quando essa tarefa é removida, as páginas Assinatura não estão disponíveis. No Gerenciador de Relatórios, a página Minhas Assinaturas parece estar vazia (não é possível excluí-la), mesmo que contivesse assinaturas anteriormente. A remoção de tarefas relacionadas à assinatura impede que os usuários criem e modifiquem assinaturas, mas não exclui as assinaturas existentes. As assinaturas existentes continuarão sendo executadas até serem excluídas. Para obter mais informações sobre a exclusão de assinaturas, consulte [criar, modificar e excluir assinaturas padrão &#40;Reporting Services no modo nativo&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md).  
  
 Para desabilitar o processamento de assinaturas em um servidor de relatório, você pode definir a `ScheduleEventsAndReportDeliveryEnabled` propriedade para `False` na **configuração de área de superfície do Reporting Services** faceta da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] gerenciamento baseado em políticas. Isso impedirá a execução de todas as operações agendadas. Você não pode simplesmente desabilitar o processamento de assinaturas no servidor de relatório.  
  
 Para obter instruções sobre como cancelar a assinatura que está sendo processada no servidor de relatório, consulte [gerenciar um processo em execução](subscriptions/manage-a-running-process.md).  
  
## <a name="disabling-delivery-extensions"></a>Desabilitando extensões de entrega  
 Todas as extensões de entrega instaladas em um servidor de relatório estão disponíveis para qualquer usuário que tenha permissão para criar uma assinatura em um relatório específico. As extensões de entrega a seguir estão disponíveis e são configuradas automaticamente:  
  
-   Compartilhamento de Arquivos do Windows  
  
-   Biblioteca do SharePoint (disponível somente a partir de um site do SharePoint que é integrado com um servidor de relatório no modo integrado do SharePoint)  
  
 A entrega de email deve ser configurada antes de ser usada. Se você não configurá-la, esse recurso não estará disponível. Para obter mais informações, consulte [configurar um servidor de relatório para entrega de email &#40;Configuration Manager do SSRS&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
 Se você desejar desabilitar extensões específicas, remova as entradas de extensão no arquivo RSReportServer.config. Para obter mais informações, consulte [RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md) e [configurar um servidor de relatório para entrega de email &#40;Configuration Manager do SSRS&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
 Depois de ser removida, a extensão de entrega não está mais disponível no Gerenciador de Relatórios ou em um site do SharePoint. A remoção de uma extensão de entrega pode resultar em assinaturas inativas. Exclua as assinaturas ou configure-as para usar uma extensão de entrega diferente antes de remover uma extensão.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Usar Minhas Assinaturas](subscriptions/use-my-subscriptions-native-mode-report-server.md)  
 Explica como usar a página Minhas Assinaturas para gerenciar as assinaturas que você possui.  
  
 [Pausar o processamento de relatório e assinatura](subscriptions/disable-or-pause-report-and-subscription-processing.md)  
 Descreve os vários modos de pausar o processamento de relatório, como, por exemplo, usando as atribuições de função ou desabilitando recursos de servidor de relatório.  
  
 [Controlar a distribuição de relatórios](../../2014/reporting-services/control-report-distribution.md)  
 Descreve configurações e opções de entrega que podem ser usadas para controlar a distribuição de relatórios.  
  
 [Monitorar assinaturas do Reporting Services](subscriptions/monitor-reporting-services-subscriptions.md)  
 Descreve como é possível determinar se uma assinatura foi bem-sucedida ou falhou, bem como os efeitos das alterações de relatório nas assinaturas existentes.  
  
## <a name="see-also"></a>Consulte também  
 [Criar, modificar e excluir assinaturas padrão &#40;Reporting Services no modo nativo&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
  
