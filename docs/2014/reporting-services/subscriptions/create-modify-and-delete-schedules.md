---
title: Criar, modificar e excluir agendamentos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report-specific schedules [Reporting Services]
- shared schedules [Reporting Services]
- modifying schedules
- removing schedules
- shared schedules [Reporting Services], creating
- shared schedules [Reporting Services], modifying
- schedules [Reporting Services], deleting
- deleting schedules
- schedules [Reporting Services], creating
- schedules [Reporting Services], modifying
- shared schedules [Reporting Services], deleting
ms.assetid: 05da5f3d-9222-43a9-893b-aa10f0f690f8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 81ad874c4d7e3c417058b2403c1307893300feaa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48118776"
---
# <a name="create-modify-and-delete-schedules"></a>Create, Modify, and Delete Schedules
  Use este tópico para aprender a criar, modificar e excluir agendas.  
  
 Neste tópico:  
  
-   [Visão geral do gerenciamento de agendas compartilhadas](#bkmk_overview)  
  
-   [Criar e gerenciar agendas compartilhadas (modo SharePoint)](#bkmk_sharepoint)  
  
-   [Criar e gerenciar agendas compartilhadas (modo nativo)](#bkmk_native)  
  
##  <a name="bkmk_overview"></a> Visão geral do gerenciamento de agendas compartilhadas  
 Para gerenciar agendas compartilhadas para o modo nativo, use a página agendas no Gerenciador de relatórios ou a pasta agendas compartilhadas no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para o modo do SharePoint, use as páginas de gerenciamento para o aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Você pode exibir todas as agendas programadas definidas para o servidor de relatório, pausar e retomar agendas (apenas no Gerenciador de Relatórios) e selecionar agendas para modificação ou exclusão. A página Agendas Compartilhadas traz as seguintes informações sobre o estado de cada agenda: frequência, proprietário, data de validade e status.  
  
 Você pode saber se uma agenda compartilhada é ativamente usada:  
  
-   Inspecionando os valores nos campos de Data da Última Execução, Data da Próxima Execução e Status na página Agendas Compartilhadas. Se uma agenda não for mais executada devido à expiração, a data de validade será exibida no campo Status.  
  
-   Exibindo a página Relatórios de uma determinada agenda compartilhada. Esta página lista todos os relatórios e todos os conjuntos de dados compartilhados que usam a agenda compartilhada.  
  
-   Exibindo os arquivos de log de execução do relatório ou logs de rastreamento para determinar se os relatórios foram executados nos horários especificados pela agenda. Para obter mais informações, consulte [Fontes e arquivos de log do Reporting Services](../report-server/reporting-services-log-files-and-sources.md).  
  
##  <a name="bkmk_sharepoint"></a> Criar e gerenciar agendas compartilhadas (modo do SharePoint)  
 Uma agenda compartilhada é uma agenda com vários propósitos que fornece informações de agenda prontas para uso para qualquer quantidade de relatórios ou assinaturas. Crie uma agenda compartilhada uma vez e, depois, faça referências a ela em uma assinatura ou página de propriedade quando precisar especificar informações de agenda. Agendas compartilhadas podem ser gerenciadas, pausadas e reiniciadas a partir de um local central. Em contraste, você deve editar manualmente uma agenda personalizada a fim de impedir a execução de um relatório ou uma assinatura.  
  
 Você deve ser um administrador de site para criar, modificar ou excluir agendamentos compartilhados em um site do SharePoint.  
  
 Você pode identificar um agendamento específico pelo nome descritivo. Se um nome não for especificado, um nome padrão será criado com base nos fatos da agenda, por exemplo, o padrão de recorrência ou as datas e horas em que é executado.  
  
> [!NOTE]  
>  A criação de agendas compartilhadas exige o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
### <a name="create-shared-schedules-sharepoint"></a>Criar agendas compartilhadas (SharePoint)  
  
##### <a name="to-create-shared-schedules"></a>Para criar agendas compartilhadas  
  
1.  Clique em **Ações do Site**.  
  
2.  Clique em **Configurações de Site**.  
  
3.  Na seção Reporting Services, clique em **Gerenciar Agendas Compartilhadas**.  
  
4.  Clique em **Adicionar Agenda** para abrir a página Propriedades da Agenda.  
  
5.  Digite um nome descritivo para o agendamento. Nas páginas de aplicativo usadas para funcionar com os relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , esse nome aparecerá em listas suspensas nas páginas de definição de agenda em todo o site. Evite usar nomes longos e difíceis de ler. Obedeça a uma convenção de nomeação que coloque a informação mais descritiva no início do nome.  
  
6.  Escolha uma frequência. Dependendo da frequência escolhida, as opções de agenda exibidas na página podem ser alteradas para oferecer suporte a essa frequência (por exemplo, se você escolher **Mês**, o nome de cada mês será exibido na página).  
  
7.  Defina o agendamento. Nem todas as combinações de agendamento têm suporte em um único agendamento.  
  
8.  Defina as datas de início e fim.  
  
9. Clique em **OK**.  
  
### <a name="delete-shared-schedules-sharepoint"></a>Excluir agendas compartilhadas (SharePoint)  
 Todas as agendas, sejam compartilhadas ou específicas de relatório, devem ser excluídas manualmente. Se você excluir uma agenda compartilhada que estiver em uso, todas as referências a ela serão substituídas por agendas personalizadas não especificadas (ou seja, uma agenda personalizada sem informações de data ou hora).  
  
 Excluir um agendamento e deixá-lo expirar são ações diferentes. Uma data de expiração é usada para parar um agendamento, mas não o exclui. Como os agendamentos são usados para automatizar as operações do servidor de relatórios, eles nunca são excluídos automaticamente. Agendamentos expirados fornecem evidência para os administradores do servidor de relatórios quanto aos motivos pelos quais um processo automatizado parou subitamente. Sem a presença do agendamento expirado, um administrador de servidor de relatórios corre o risco de fazer um diagnóstico incorreto do problema ou gastar tempo desnecessariamente tentando solucionar um processo totalmente funcional.  
  
 Uma agenda personalizada que expirou permanece anexada ao relatório. Você poderá determinar se uma agenda expirou verificando sua data de término. Uma agenda compartilhada expirada permanece na lista de Agendas Compartilhadas. O campo Status indica se a agenda expirou. Você pode restabelecer o agendamento estendendo a data de fim, ou pode remover a referência ao agendamento se ele não for mais necessário.  
  
##### <a name="to-delete-a-shared-schedule"></a>Para excluir uma agenda compartilhada  
  
1.  Clique em **Ações do Site**.  
  
2.  Clique em **Configurações de Site**.  
  
3.  Na seção Reporting Services, clique em **Gerenciar Agendas Compartilhadas**.  
  
4.  Selecione a agenda e clique em **Excluir**.  
  
##  <a name="bkmk_native"></a> Criar e gerenciar agendas compartilhadas (modo nativo)  
 As agendas compartilhadas devem ser excluídas manualmente usando a página Agendas no Gerenciador de Relatórios ou a pasta Agendas Compartilhadas no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Se você excluir uma agenda compartilhada que está em uso, serão substituídas todas as referências a ela por agendas específicas do relatório.  
  
 As agendas específicas do relatório e assinatura são excluídas quando você exclui o relatório ou a assinatura ou quando você opta por uma abordagem diferente para executar o relatório ou a assinatura. Por exemplo, optar por **Sempre executar este relatório com a data mais recente** excluirá uma agenda específica do relatório criada para executar um relatório como um instantâneo de execução do relatório.  
  
 Excluir um agendamento e deixá-lo expirar são ações diferentes. Uma data de expiração é usada para parar um agendamento, mas não o exclui. Como as agendas são usadas para automatizar muitos recursos, elas nunca são excluídas automaticamente. Agendamentos expirados fornecem evidência para os administradores do servidor de relatórios quanto aos motivos pelos quais um processo automatizado parou subitamente. Sem a presença da agenda expirada, um administrador do servidor de relatório pode diagnosticar incorretamente o problema ou gastar tempo desnecessário tentando solucionar um processo totalmente funcional.  
  
 Uma agenda específica do relatório que expirou permanece anexada ao relatório. Você poderá determinar se uma agenda expirou verificando sua data de término. Uma agenda compartilhada expirado permanece na lista Agendas Compartilhadas. O campo Status indica se a agenda expirou. Você pode restabelecer o agendamento estendendo a data de fim, ou pode remover a referência ao agendamento se ele não for mais necessário.  
  
### <a name="create-delete-or-modify-a-shared-schedule-report-manager"></a>Criar, excluir ou modificar uma agenda compartilhada (Gerenciador de Relatórios)  
 A criação e modificação de uma agenda é composta pela definição de opções de frequência que determinam quando a agenda é executada.  
  
-   São criadas agendas compartilhadas como itens separados. Depois que eles são criados, você faz referência a eles ao definir uma assinatura ou alguma outra operação agendada.  
  
-   As agendas específicas do relatório são criadas quando você define uma assinatura ou define as propriedades de execução do relatório; o preenchimento das informações de agenda é parte da definição de uma assinatura ou da definição de propriedades. Para definir uma agenda específica do relatório, abra o relatório ou a assinatura que usa este.  
  
 Uma agenda compartilhada contém informações de agenda e recorrência que podem ser usadas por qualquer número de relatórios e assinaturas publicados que são executados em um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se houver muitos relatórios e assinaturas em execução ao mesmo tempo, você pode criar uma agenda compartilhada para esses trabalhos. Se desejar alternar subsequentemente o padrão de recorrência ou a data de término, faça a alteração em um lugar.  
  
 As agendas compartilhadas são mais fáceis de manter e oferecem mais flexibilidade no gerenciamento de operações agendadas. Por exemplo, você pode pausar e retomar agendas compartilhadas. Além disso, se houver muitas operações agendadas em execução ao mesmo tempo, você pode criar várias agendas compartilhadas que são executadas em horários diferentes e, em seguida, ajustar as informações de agenda até que a carga de processamento se estabilize no servidor de relatório.  
  
 Um agendamento pode ser criado ou modificado a qualquer momento. No entanto, se uma agenda começar a ser executada antes de você ter concluído as modificações, será usada a versão anterior da agenda. O agendamento revisado só entra em vigor quando você o salva.  
  
 Se estiver modificando uma agenda compartilhada, poderá fazer uma pausa nela antes de fazer as alterações. As alterações entram em vigor quando você reiniciar a agenda.  
  
##### <a name="to-create-or-modify-a-shared-schedule-report-manager"></a>Para criar ou modificar uma agenda compartilhada (Gerenciador de Relatórios)  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  No Gerenciador de Relatórios, clique em **Configurações de Site**na barra de ferramentas global.  
  
3.  Clique em **agendas**.  
  
4.  Clique em **Nova Agenda**. Para modificar uma agenda existente, clique no nome da agenda.  
  
5.  Digite um nome descritivo para a agenda.  
  
6.  Selecione **Hora**, **Dia**, **Semana**ou **Mês**. Clique em **Uma vez** para criar uma agenda que é executada somente uma vez por dia. Opções adicionais aparecem quando você especifica a base da agenda.  
  
7.  Opcionalmente, selecione uma data para iniciar a agenda. O padrão é o dia atual. Você pode adiar a hora de início de agenda escolhendo uma data posterior.  
  
8.  Opcionalmente, selecione uma data para terminar a agenda. A agenda deixa de ser executada nesta data, mas não é excluída.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##### <a name="to-delete-a-shared-schedule-report-manager"></a>Para excluir uma agenda compartilhada (Gerenciador de Relatórios)  
  
1.  No Gerenciador de Relatórios, clique em **Configurações de Site**na barra de ferramentas global.  
  
    > [!NOTE]  
    >  Se **configurações de Site** é não está disponível, você não tem permissão para acessar configurações de site.  
  
2.  Na seção **Outros** da página, clique em **Gerenciar agendamentos compartilhados**.  
  
3.  Marque a caixa de seleção próxima ao agendamento que deseja excluir e clique em **Excluir**.  
  
 Se uma agenda compartilhada usada por vários relatórios e assinaturas for excluída, o servidor de relatório criará agendas individuais para cada relatório e assinatura que usou anteriormente a agenda compartilhada. Cada nova agenda individual conterá a data, a hora e o padrão de recorrência que foram especificados na agenda compartilhada. Observe que o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não fornece o gerenciamento central de agendas individuais. Se você excluir uma agenda compartilhada, deverá manter as informações de agenda para cada item individual.  
  
 Se você não tiver certeza de que uma agenda compartilhada será usada, considere a exclusão dela no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] fornece os mesmos recursos de gerenciamento de agenda compartilhada que o Gerenciador de Relatórios, mas fornece uma página Relatórios adicional que mostra o nome de cada relatório que usa a agenda.  
  
### <a name="create-delete-or-modify-a-shared-schedule-management-studio"></a>Criar, excluir ou modificar uma agenda compartilhada (Management Studio)  
 Uma agenda compartilhada contém informações de agenda e recorrência que podem ser usadas por qualquer número de relatórios e assinaturas publicados que são executados em um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se houver muitos relatórios e assinaturas em execução ao mesmo tempo, você pode criar uma agenda compartilhada para esses trabalhos. Se desejar alternar subsequentemente o padrão de recorrência ou a data de término, faça a alteração em um lugar.  
  
 As agendas compartilhadas são mais fáceis de manter e oferecem mais flexibilidade no gerenciamento de operações agendadas. Por exemplo, você pode pausar e retomar agendas compartilhadas. Além disso, se houver muitas operações agendadas em execução ao mesmo tempo, você pode criar várias agendas compartilhadas que são executadas em horários diferentes e, em seguida, ajustar as informações de agenda até que a carga de processamento se estabilize no servidor de relatório.  
  
##### <a name="to-create-or-modify-a-shared-schedule-management-studio"></a>Para criar ou modificar uma agenda compartilhada (Management Studio)  
  
1.  Inicie o SQL Server Management Studio e conecte-se a uma instância do servidor de relatório.  
  
2.  No Pesquisador de Objetos, expanda um nó do servidor de relatório.  
  
3.  A pasta agendas compartilhadas com o botão direito e, em seguida, clique em **nova agenda**. A página Geral da caixa de diálogo **Nova Agenda Compartilhada** é exibida.  
  
     Para modificar uma agenda compartilhada existente, expanda a pasta Agendas Compartilhadas, clique com o botão direito do mouse na agenda que deseja modificar e clique em **Propriedades**.  
  
4.  Digite um nome descritivo para a agenda.  
  
5.  Opcionalmente, selecione uma data para iniciar a agenda. O padrão é o dia atual.  
  
6.  Opcionalmente, selecione uma data para terminar a agenda. A agenda deixa de ser executada nesta data, mas não é excluída.  
  
7.  Para configurar uma agenda recorrente, selecione **Hora**, **Dia**, **Semana**ou **Mês**. São exibidas opções adicionais. Use essas opções adicionais para configurar a frequência da agenda, com base em sua hora, dia, semana ou mês preferido.  
  
     Se preferir, especifique uma agenda única (não recorrente) selecionando **Uma Vez**e especificando uma **Hora de Início**.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##### <a name="to-delete-a-shared-schedule-management-studio"></a>Para excluir uma agenda compartilhada (Management Studio)  
  
1.  No Pesquisador de Objetos, expanda um nó do servidor de relatório.  
  
2.  Expanda a pasta Agendas Compartilhadas, clique com o botão direito do mouse na agenda que deseja excluir e, em seguida, clique em **Excluir**. A caixa de diálogo **Excluir Itens do Catálogo** é exibida.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Se uma agenda compartilhada usada por vários relatórios e assinaturas for excluída, o servidor de relatório criará agendas individuais para cada relatório e assinatura que usou anteriormente a agenda compartilhada. Cada nova agenda individual conterá a data, a hora e o padrão de recorrência que foram especificados na agenda compartilhada. Observe que o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não fornece o gerenciamento central de agendas individuais. Se você excluir uma agenda compartilhada, deverá manter as informações de agenda para cada item individual. Antes de excluir uma agenda compartilhada, use o [página relatórios](../tools/schedule-properties-reports-page.md) para determinar quais relatórios estão usando atualmente a agenda compartilhada.  
  
## <a name="see-also"></a>Consulte também  
 [Agendas](schedules.md)   
 [Pausar e retomar agendamentos compartilhados](pause-and-resume-shared-schedules.md)   
 [Armazenar um relatório em cache &#40;Gerenciador de Relatórios&#41;](../report-server/cache-a-report-report-manager.md)   
 [Adicionar um instantâneo ao histórico de relatórios &#40;Gerenciador de Relatórios&#41;](../report-server/add-a-snapshot-to-report-history-report-manager.md)  
  
  
