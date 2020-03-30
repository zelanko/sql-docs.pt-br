---
title: Criar, modificar e excluir agendamentos | Microsoft Docs
ms.date: 06/11/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
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
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 29b453914dce3d371ded8f401fd4af0380a115b8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67140222"
---
# <a name="create-modify-and-delete-schedules"></a>Create, Modify, and Delete Schedules
  Use este artigo para aprender a criar, modificar e excluir agendas compartilhadas do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] .  Para gerenciar agendas programadas para o modo nativo, use a página Agendas no portal da Web ou a pasta de agendas compartilhadas no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para o modo do SharePoint, use as páginas de gerenciamento para o aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .

 Use um dos seguintes métodos para determinar se uma agenda compartilhada é ativamente usada:

-   **Portal da Web:** na guia **Agendas** das **Configurações do Site**, examine os valores nos campos data da Última Execução, data da Próxima Execução e Status. Se uma agenda não for mais executada devido à expiração, a data de validade será exibida no campo Status. Para obter mais informações, veja [Web portal (SSRS Native Mode)](../../reporting-services/web-portal-ssrs-native-mode.md).

-   **SQL Server Management Studio:** exibir a página **Relatórios** de uma determinada agenda compartilhada. Esta página lista todos os relatórios e todos os conjuntos de dados compartilhados que usam a agenda compartilhada. Para saber mais, confira [Reporting Services no SQL Server Management Studio](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md).

-  **Logs:** Exibindo os arquivos de log de execução do relatório ou logs de rastreamento para determinar se os relatórios foram executados nos horários especificados pela agenda. Para obter mais informações, consulte [Fontes e arquivos de log do Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).

## <a name="when-you-delete-a-shared-schedule"></a>Quando você exclui uma agenda compartilhada
As agendas compartilhadas devem ser excluídas manualmente usando a página Agendas no portal da Web ou a pasta Agendas Compartilhadas no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Se você excluir uma agenda compartilhada que está em uso, serão substituídas todas as referências a ela por agendas específicas do relatório.

Se uma agenda compartilhada usada por vários relatórios e assinaturas for excluída, o servidor de relatório criará agendas individuais para cada relatório e assinatura que usou anteriormente a agenda compartilhada. Cada nova agenda individual conterá a data, a hora e o padrão de recorrência que foram especificados na agenda compartilhada. Observe que o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não fornece o gerenciamento central de agendas individuais. Se você excluir uma agenda compartilhada, deverá manter as informações de agenda para cada item individual.

**Observação:**  se você não tiver certeza de que uma agenda compartilhada será usada, considere a exclusão dele no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] em vez de no portal da Web. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] fornece os mesmos recursos de gerenciamento de agenda compartilhada que o Gerenciador de Relatórios, mas fornece uma página Relatórios adicional que mostra o nome de cada relatório que usa a agenda.

 Excluir um agendamento e deixá-lo expirar são ações diferentes. Uma data de expiração é usada para parar um agendamento, mas não o exclui. Como as agendas são usadas para automatizar muitos recursos, elas nunca são excluídas automaticamente. Agendamentos expirados fornecem evidência para os administradores do servidor de relatórios quanto aos motivos pelos quais um processo automatizado parou subitamente. Sem a presença da agenda expirada, um administrador do servidor de relatório pode diagnosticar incorretamente o problema ou gastar tempo desnecessário tentando solucionar um processo totalmente funcional.

 ## <a name="when-you-delete-a-report-specific-schedule"></a>Quando você exclui uma agenda específica de relatório
As agendas específicas do relatório e assinatura são excluídas quando você exclui o relatório ou a assinatura ou quando você opta por uma abordagem diferente para executar o relatório ou a assinatura. Por exemplo, optar por **Sempre executar este relatório com a data mais recente** excluirá uma agenda específica do relatório criada para executar um relatório como um instantâneo de execução do relatório.

Uma agenda específica do relatório que expirou permanece anexada ao relatório. Você poderá determinar se uma agenda expirou verificando sua data de término. Uma agenda compartilhada expirado permanece na lista Agendas Compartilhadas. O campo Status indica se a agenda expirou. Você pode restabelecer o agendamento estendendo a data de fim, ou pode remover a referência ao agendamento se ele não for mais necessário.

## <a name="create-delete-or-modify-a-shared-schedule-web-portal"></a><a name="bkmk_native"></a> Criar, excluir ou modificar uma agenda compartilhada (portal da Web)
 A criação e modificação de uma agenda é composta pela definição de opções de frequência que determinam quando a agenda é executada.

 Um agendamento pode ser criado ou modificado a qualquer momento. No entanto, se uma agenda começar a ser executada antes de você ter concluído as modificações, será usada a versão anterior da agenda. O agendamento revisado só entra em vigor quando você o salva.

 Se estiver modificando uma agenda compartilhada, poderá fazer uma pausa nela antes de fazer as alterações. As alterações entram em vigor quando você reiniciar a agenda.

1. No portal da Web, escolha **Configurações** ![ssrs_portal_settings_gear](../../reporting-services/subscriptions/media/ssrs-portal-settings-gear.png) na barra de ferramentas.  

   >[!NOTE]  
   >Se **Configurações** não estiver disponível, você não terá permissão para acessar configurações do site.  

1. Selecione **Configurações do site** no menu suspenso.
1. Selecione a guia **Agendas** .
1. Selecione **+ Nova agenda**. (Para modificar uma agenda existente, escolha o nome da agenda).
1. Digite um nome descritivo para a agenda.
1. Selecione **Hora**, **Dia**, **Semana**ou **Mês**. Clique em **Uma vez** para criar uma agenda que é executada somente uma vez por dia. Opções adicionais aparecem quando você especifica a base da agenda.
1. Opcionalmente, selecione uma data para iniciar a agenda. O padrão é o dia atual. Você pode adiar a hora de início de agenda escolhendo uma data posterior.
1. Opcionalmente, selecione uma data para terminar a agenda. A agenda deixa de ser executada nesta data, mas não é excluída.
1. Selecione uma hora para a execução da agenda.
1. Selecione **OK**.

### <a name="to-delete-a-shared-schedule-web-portal"></a>Para excluir uma agenda compartilhada (portal da Web)

1. No portal da Web, escolha **Configurações** ![ssrs_portal_settings_gear](../../reporting-services/subscriptions/media/ssrs-portal-settings-gear.png) na barra de ferramentas.
2. Selecione **Configurações do site** no menu suspenso.
3. Selecione a guia **Agendas** .
4. Marque a caixa de seleção próxima à agenda compartilhada que deseja excluir e escolha **Excluir**.

### <a name="create-delete-or-modify-a-shared-schedule--management-studio"></a>Criar, excluir ou modificar uma agenda compartilhada (Management Studio)
 Uma agenda compartilhada contém informações de agenda e recorrência que podem ser usadas por qualquer número de relatórios e assinaturas publicados que são executados em um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se houver muitos relatórios e assinaturas em execução ao mesmo tempo, você pode criar uma agenda compartilhada para esses trabalhos. Se desejar alternar subsequentemente o padrão de recorrência ou a data de término, faça a alteração em um lugar.

 As agendas compartilhadas são mais fáceis de manter e oferecem mais flexibilidade no gerenciamento de operações agendadas. Por exemplo, você pode pausar e retomar agendas compartilhadas. Além disso, se houver muitas operações agendadas em execução ao mesmo tempo, você pode criar várias agendas compartilhadas que são executadas em horários diferentes e, em seguida, ajustar as informações de agenda até que a carga de processamento se estabilize no servidor de relatório.

#### <a name="to-create-or-modify-a-shared-schedule-management-studio"></a>Para criar ou modificar uma agenda compartilhada (Management Studio)

1.  Inicie o [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] e conecte-se a uma instância do servidor de relatório.
2.  No Pesquisador de Objetos, expanda um nó do servidor de relatório.
3.  Clique com o botão direito do mouse na pasta **Agendas Compartilhadas** e, em seguida, clique em **Nova Agenda**. A página Geral da caixa de diálogo **Nova Agenda Compartilhada** é exibida.

     Para modificar uma agenda compartilhada existente, expanda a pasta Agendas Compartilhadas, clique com o botão direito do mouse na agenda que deseja modificar e clique em **Propriedades**.

4.  Digite um nome descritivo para a agenda.
5.  Opcionalmente, selecione uma data para iniciar a agenda. O padrão é o dia atual.
6.  Opcionalmente, selecione uma data para terminar a agenda. A agenda deixa de ser executada nesta data, mas não é excluída.
7.  Para configurar uma agenda recorrente, selecione **Hora**, **Dia**, **Semana**ou **Mês**. São exibidas opções adicionais. Use essas opções adicionais para configurar a frequência da agenda, com base em sua hora, dia, semana ou mês preferido.

     Se preferir, especifique uma agenda única (não recorrente) selecionando **Uma Vez**e especificando uma **Hora de Início**.

8.  Selecione **OK**.

##### <a name="to-delete-a-shared-schedule-management-studio"></a>Para excluir uma agenda compartilhada (Management Studio)

1.  No Pesquisador de Objetos, expanda um nó do servidor de relatório.
2.  Para verificar se a agenda compartilhada não está sendo usada atualmente por relatórios, expanda a pasta Agendas Compartilhadas, clique com o botão direito do mouse na agenda e em **Propriedades**.
3. clique na guia **Relatórios** para exibir a lista de relatórios que usam atualmente o agendamento.
clique em **Cancelar**
4.  Expanda a pasta Agendas Compartilhadas, clique com o botão direito do mouse na agenda que deseja excluir e, em seguida, clique em **Excluir**. A caixa de diálogo **Excluir Itens do Catálogo** é exibida.
5.  Selecione **OK**.

 Se uma agenda compartilhada usada por vários relatórios e assinaturas for excluída, o servidor de relatório criará agendas individuais para cada relatório e assinatura que usou anteriormente a agenda compartilhada. Cada nova agenda individual conterá a data, a hora e o padrão de recorrência que foram especificados na agenda compartilhada.

##  <a name="create-and-manage-shared-schedules-sharepoint-mode"></a><a name="bkmk_sharepoint"></a>Criar e gerenciar agendas compartilhadas (modo do SharePoint)
 Você deve ser um administrador de site para criar, modificar ou excluir agendamentos compartilhados em um site do SharePoint.

 Você pode identificar um agendamento específico pelo nome descritivo. Se um nome não for especificado, um nome padrão será criado com base nos fatos da agenda, por exemplo, o padrão de recorrência ou as datas e horas em que é executado.

> [!NOTE]
> A criação de agendas compartilhadas exige o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.

### <a name="create-shared-schedules-sharepoint-mode"></a>Criar agendas compartilhadas (Modo do SharePoint)
1.  Clique em **Ações do Site**.
2.  Clique em **Configurações de Site**.
3.  Na seção Reporting Services, clique em **Gerenciar Agendas Compartilhadas**.
4.  Clique em **Adicionar Agenda** para abrir a página Propriedades da Agenda.
5.  Digite um nome descritivo para o agendamento. Nas páginas de aplicativo usadas para funcionar com os relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , esse nome aparecerá em listas suspensas nas páginas de definição de agenda em todo o site. Evite usar nomes longos e difíceis de ler. Obedeça a uma convenção de nomeação que coloque a informação mais descritiva no início do nome.
6.  Escolha uma frequência. Dependendo da frequência escolhida, as opções de agenda exibidas na página podem ser alteradas para oferecer suporte a essa frequência (por exemplo, se você escolher **Mês**, o nome de cada mês será exibido na página).
7.  Defina o agendamento. Nem todas as combinações de agendamento têm suporte em um único agendamento.
8.  Defina as datas de início e fim.
9. Clique em **OK**.

### <a name="delete-shared-schedules-sharepoint-mode"></a>Excluir agendas compartilhadas (Modo do SharePoint)
 Todas as agendas, sejam compartilhadas ou específicas de relatório, devem ser excluídas manualmente. Se você excluir uma agenda compartilhada que estiver em uso, todas as referências a ela serão substituídas por agendas personalizadas não especificadas (ou seja, uma agenda personalizada sem informações de data ou hora).

1.  Clique em **Ações do Site**.
2.  Clique em **Configurações de Site**.
3.  Na seção Reporting Services, clique em **Gerenciar Agendas Compartilhadas**.
4.  Selecione a agenda e clique em **Excluir**.


## <a name="see-also"></a>Confira também
 [Agendas](../../reporting-services/subscriptions/schedules.md)  
 [Pausar e retomar agendas compartilhadas](../../reporting-services/subscriptions/pause-and-resume-shared-schedules.md)  
 [Relatórios em cache (SSRS)](../../reporting-services/report-server/caching-reports-ssrs.md)  
 [Criar, modificar e excluir instantâneos no histórico de relatórios](../report-server/create-modify-and-delete-snapshots-in-report-history.md)

