---
title: Manipuladores de eventos do SSIS (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, events
- run-time [Integration Services]
- SQL Server Integration Services packages, events
- event handlers [Integration Services], about event handlers
- events [Integration Services]
- packages [Integration Services], events
- event handlers [Integration Services]
- SSIS packages, events
- containers [Integration Services], events
- events [Integration Services], about events
ms.assetid: 6f60cf93-35dc-431c-908d-2049c4ab66ba
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 41a6ae9c6462beecaa244694bd8679df88aefc47
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176127"
---
# <a name="integration-services-ssis-event-handlers"></a>Manipuladores de eventos do SSIS (Integration Services)
  Em tempo de execução, os executáveis (pacotes e contêineres Loop Foreach, Loop For, de Sequência e de host da tarefa) geram eventos. Por exemplo, um evento OnError será gerado quando acontecer um erro. Você pode criar manipuladores de eventos personalizados para esses eventos a fim de estender a funcionalidade do pacote e fazer com que os pacotes sejam mais fáceis de administrar em tempo de execução. Os manipuladores de eventos podem executar tarefas como:

-   Limpar o armazenamento de dados temporários quando um pacote ou tarefa termina de ser executado.

-   Recuperar informações de sistema para avaliar a disponibilidade de recursos antes da execução de um pacote.

-   Atualizar dados de uma tabela quando ocorrer falha na pesquisa em uma tabela de referências.

-   Enviar uma mensagem de email quando ocorrer erro, aviso ou falha em uma tarefa.

 Quando um evento não tem um manipulador de eventos, o evento é gerado para o próximo contêiner superior na hierarquia de contêineres de um pacote. Se esse contêiner tiver um manipulador de eventos, este entrará em execução em resposta ao evento. Se não, o evento será gerado para o próximo contêiner superior na hierarquia de contêineres.

 O diagrama a seguir mostra um pacote simples que tem um contêiner Loop For que contém uma tarefa Executar SQL.

 ![Pacote, Loop For, host de tarefas e tarefa Executar SQL](media/mw-dts-eventhandlerpkg.gif "Pacote, Loop For, host de tarefas e tarefa Executar SQL")

 Só o pacote tem um manipulador de eventos, para seu evento `OnError`. Se ocorrer um erro quando a tarefa Executar SQL for executada, o manipulador de eventos `OnError` do pacote entrará em execução. O diagrama a seguir mostra a sequência de chamadas que faz o manipulador de eventos `OnError` do pacote executar.

 ![Fluxo do manipulador de eventos](media/mw-dts-eventhandlers.gif "Fluxo do manipulador de eventos")

 Manipuladores de eventos são membros de uma coleção de manipuladores de eventos e todos os contêineres incluem esta coleção. Se você criar o pacote usando o Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , poderá ver os membros das coleções de manipuladores de eventos nas pastas **Manipuladores de Eventos** , na guia **Explorador de Pacotes** , do Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] .

 Você pode configurar o contêiner de manipulador de eventos dos seguintes modos:

-   Especifique um nome e uma descrição para o manipulador de eventos.

-   Indique se o manipulador de eventos está em execução, se o pacote falha quando o manipulador de eventos falha e o número de erros que podem ocorrer antes de o manipulador de eventos falhar.

-   Especifique um resultado de execução a retornar no lugar do resultado da execução real que o manipulador de eventos retorna durante a execução.

-   Especifique a opção de transação do manipulador de eventos.

-   Especifique o modo de registro usado pelo manipulador de eventos.

## <a name="event-handler-content"></a>Conteúdo do manipulador de eventos
 Criar um manipulador de eventos é como criar um pacote; um manipulador de eventos possui tarefas e contêineres, que são colocados em sequência em um fluxo de controle, e um manipulador de eventos também pode incluir fluxos de dados. O Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] inclui a guia **Manipuladores de Eventos** para a criação de manipuladores de eventos personalizados. Para obter mais informações, consulte [manipuladores de eventos de pacote SSIS](integration-services-ssis-event-handlers.md).

 Você também pode criar manipuladores de eventos programaticamente. Para obter mais informações, consulte [Manipulação de erros programaticamente](building-packages-programmatically/handling-events-programmatically.md).

## <a name="run-time-events"></a>Eventos de tempo de execução
 A tabela a seguir lista os manipuladores de eventos que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece e descreve os eventos de tempo de execução que acionam a execução do manipulador de eventos.

|Manipulador de eventos|Evento|
|-------------------|-----------|
|`OnError`|O manipulador de eventos para o evento `OnError`. Esse evento é gerado por um executável quando ocorre um erro.|
|**OnExecStatusChanged**|Manipulador de eventos do evento **OnExecStatusChanged** . Esse evento é gerado por um executável quando seu status de execução é alterado.|
|**OnInformation**|Manipulador de eventos do evento **OnInformation** . Esse evento é gerado durante a validação e execução de um executável para fornecer informações. Esse evento transmite apenas informações, nenhum erro ou avisos.|
|**OnPostExecute**|Manipulador de eventos do evento **OnPostExecute** . Esse evento é gerado por um executável logo depois que este termina de ser executado.|
|**OnPostValidate**|Manipulador de eventos do evento **OnPostValidate** . Esse evento é gerado por um executável quando sua validação é finalizada.|
|**OnPreExecute**|Manipulador de eventos do evento **OnPreExecute** . Esse evento é gerado por um executável imediatamente antes da sua execução.|
|**OnPreValidate**|Manipulador de eventos do evento **OnPreValidate** . Esse evento é gerado por um executável quando sua validação é iniciada.|
|**OnProgress**|Manipulador de eventos do evento **OnProgress** . Esse evento é gerado por um executável quando um progresso mensurável é feito pelo executável.|
|**OnQueryCancel**|Manipulador de eventos do evento **OnQueryCancel** . Esse evento é gerado por um executável para determinar se deve parar de ser executado.|
|**OnTaskFailed**|Manipulador de eventos do evento **OnTaskFailed** . Esse evento é gerado por uma tarefa quando ela falha.|
|**OnVariableValueChanged**|Manipulador de eventos do evento **OnVariableValueChanged** . Esse evento é gerado por um executável quando o valor de uma variável é alterado. O evento é gerado pelo executável no qual a variável está definida. Esse evento não será gerado se você definir a propriedade **RaiseChangeEvent** para a variável como `False`. Para obter mais informações, consulte [Variáveis do SSIS &#40;Integration Services&#41;](integration-services-ssis-variables.md).|
|**OnWarning**|Manipulador de eventos do evento **OnWarning** . Esse evento é gerado por um executável quando ocorre um aviso.|

## <a name="configuration-of-an-event-handler"></a>Configuração de um manipulador de eventos
 Você pode definir as propriedades na janela **Propriedades** do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ou programaticamente.

 Para obter informações sobre como definir essas propriedades no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], consulte [Definir as propriedades de uma tarefa ou de um contêiner](../../2014/integration-services/set-the-properties-of-a-task-or-container.md).

 Para obter informações sobre como definir essas propriedades programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>.

## <a name="related-tasks"></a>Related Tasks
 Para obter informações sobre como adicionar um manipulador de eventos a um pacote, consulte [Adicionar um manipulador de eventos a um pacote](../../2014/integration-services/add-an-event-handler-to-a-package.md).


