---
title: Contêineres do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SSIS containers
- containers [Integration Services]
- containers [Integration Services], about containers
- control flow [Integration Services], containers
- SQL Server Integration Services containers
ms.assetid: 1b725922-ec59-4a47-9d55-e079463058f3
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1d27f27154fe4faa1f028c53aafd7db40f20e938
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35333270"
---
# <a name="integration-services-containers"></a>Contêineres do Integration Services
  Contêineres são objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que fornecem estrutura a pacotes e serviços a tarefas. Eles fornecem suporte à repetição de fluxos de controle em pacotes e agrupam tarefas e contêineres em unidades de trabalho significativas. Os contêineres podem incluir outros contêineres, além de tarefas.  
  
 Os pacotes usam contêineres para os propósitos a seguir:  
  
-   Repetição de tarefas para cada elemento em uma coleção, como arquivos em uma pasta, esquemas ou objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO). Por exemplo, um pacote pode executar instruções Transact-SQL que residem em arquivos múltiplos.  
  
-   Repita as tarefas até que uma expressão especificada seja avaliada como **false**. Por exemplo, um pacote pode enviar uma mensagem diferente de email sete vezes, uma vez para cada dia da semana.  
  
-   Agrupar tarefas e contêineres que precisam ter êxito ou falhar como uma unidade. Por exemplo, um pacote pode agrupar tarefas que excluem e somam linhas em uma tabela de banco de dados, e então confirmar ou reverter todas as tarefas quando uma apresentar falha.  
  
## <a name="container-types"></a>Tipos de contêineres  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece quatro tipos de contêineres para criar pacotes. A tabela a seguir lista os tipos de contêineres.  
  
|Contêiner|Descrição|  
|---------------|-----------------|  
|[Contêiner Loop Foreach](../../integration-services/control-flow/foreach-loop-container.md)|Executa um fluxo de controle repetidamente usando um enumerador.|  
|[Contêiner Loop For](../../integration-services/control-flow/for-loop-container.md)|Executa um fluxo de controle repetidamente testando uma condição.|  
|[Contêiner Sequência](../../integration-services/control-flow/sequence-container.md)|Agrupa tarefas e contêineres em fluxos de controle que são subconjuntos do fluxo de controle de pacote.|  
|[Contêiner Host da Tarefa](../../integration-services/control-flow/task-host-container.md)|Fornece serviços a uma única tarefa.|  
  
 Pacotes e manipuladores de eventos também são tipos de contêineres. Para obter informações, consulte [Pacotes do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md) e [Manipuladores de Eventos do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-event-handlers.md).  
  
### <a name="summary-of-container-properties"></a>Resumo das propriedades dos contêineres  
 Todos os tipos de contêineres têm um conjunto de propriedades em comum. Se você criar pacotes que usam as ferramentas gráficas fornecidas pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , a janela Propriedades listará as propriedades a seguir dos contêineres Foreach Loop, Loop For e Sequence. As propriedades do contêiner host da tarefa são configuradas como parte da configuração da tarefa que o host da tarefa encapsula. Você define as propriedades Host da Tarefa quando configura a tarefa.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**DelayValidation**|Um valor booliano que indica se a validação do contêiner foi adiada até o tempo de execução. O valor padrão para essa propriedade é **False**.<br /><br /> Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.DelayValidation%2A>.|  
|**Descrição**|É a descrição do contêiner. A propriedade contém uma cadeia de caracteres, mas pode estar em branco.<br /><br /> Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Description%2A>.|  
|**Disable**|Um valor booliano que indica se o contêiner é executado. O valor padrão para essa propriedade é **False**.<br /><br /> Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Disable%2A>.|  
|**DisableEventHandlers**|Um valor booliano que indica se os manipuladores de eventos estão associados à execução do contêiner. O valor padrão para essa propriedade é **False**.|  
|**FailPackageOnFailure**|Um valor booliano que especifica se o pacote irá falhar se ocorrer um erro no contêiner. O valor padrão para essa propriedade é **False**.<br /><br /> Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.FailPackageOnFailure%2A>.|  
|**FailParentOnFailure**|Um valor booliano que especifica se o contêiner pai irá falhar se ocorrer um erro no contêiner. O valor padrão para essa propriedade é **False**.<br /><br /> Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.FailParentOnFailure%2A>.|  
|**ForcedExecutionValue**|Se **ForceExecutionValue** estiver definido como **True**, o objeto que contém o valor de execução opcional para o contêiner. O valor padrão dessa propriedade é **0**.<br /><br /> Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForcedExecutionValue%2A>.|  
|**ForcedExecutionValueType**|O tipo de dados de **ForcedExecutionValue**. O valor padrão dessa propriedade é **Int32**.|  
|**ForceExecutionResult**|Um valor que especifica o resultado forçado da execução do pacote ou contêiner. Os valores são **None**, **Success**, **Failure**e **Completion**. O valor padrão para essa propriedade é **None**.<br /><br /> Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForceExecutionResult%2A>.|  
|**ForceExecutionValue**|Um valor Booliano que especifica se o valor de execução opcional do contêiner deve ser forçado a conter um valor específico. O valor padrão dessa propriedade é **False**.<br /><br /> Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForceExecutionValue%2A>.|  
|**ID**|É o GUID do contêiner que é atribuído quando o pacote é criado. Esta propriedade é somente leitura.<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ID%2A>.|  
|**IsolationLevel**|É o nível de isolamento da transação de contêiner. Os valores são **Unspecified**, **Chaos**, **ReadUncommitted**, **ReadCommitted**, **RepeatableRead**, **Serializable**e **Snapshot**. O valor padrão dessa propriedade é **Serializable**. Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.IsolationLevel%2A>.|  
|**LocaleID**|É uma localidade do Microsoft Win32. O valor padrão dessa propriedade é a localidade do sistema operacional no computador local.<br /><br /> Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LocaleID%2A>.|  
|**LoggingMode**|É um valor que especifica o comportamento de log do contêiner. Os valores são **Disabled**, **Enabled**e **UseParentSetting**. O valor padrão dessa propriedade é **UseParentSetting**. Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode>.|  
|**MaximumErrorCount**|É o número máximo de erros que podem acontecer antes de um contêiner parar de ser executado. O valor padrão desta propriedade é **1**.<br /><br /> Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.MaximumErrorCount%2A>.|  
|**Nome**|É o nome do contêiner.<br /><br /> Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Name%2A>.|  
|**TransactionOption**|É a participação transacional do contêiner. Os valores são **NotSupported**, **Supported**e **Required**. O valor padrão dessa propriedade é **Supported**. Para obter mais informações, consulte <xref:Microsoft.SqlServer.Dts.Runtime.DTSTransactionOption>.|  
  
 Para saber a respeito de todas as propriedades que estão disponíveis para os contêineres Loop Foreach, Loop For, Sequência e Host da Tarefa ao configurá-los programaticamente, consulte os seguintes tópicos da API de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] :  
  
-   T:Microsoft.SqlServer.Dts.Runtime.ForEachLoop  
  
-   T:Microsoft.SqlServer.Dts.Runtime.ForLoop  
  
-   T:Microsoft.SqlServer.Dts.Runtime.Sequence  
  
-   T:Microsoft.SqlServer.Dts.Runtime.TaskHost  
  
## <a name="objects-that-extend-container-functionality"></a>Objetos que estendem a funcionalidade do contêiner  
 Os contêineres incluem fluxos de controle que consistem em executáveis e restrições de precedência e podem usar manipuladores de eventos e variáveis. O contêiner host da tarefa é uma exceção: como o contêiner host da tarefa encapsula uma única tarefa, ele não usa restrições de precedência.  
  
### <a name="executables"></a>Executáveis  
 Os executáveis referem-se às tarefas do nível de contêiner e a qualquer contêiner dentro do contêiner. Um executável pode ser uma das tarefas e dos contêineres que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece ou uma tarefa personalizada. Para obter mais informações, consulte [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md).  
  
### <a name="precedence-constraints"></a>Restrições de precedência  
 As restrições de precedência vinculam contêineres e tarefas dentro do mesmo contêiner pai em um fluxo de controle ordenado. Para obter informações, consulte [Restrições de precedência](../../integration-services/control-flow/precedence-constraints.md).  
  
### <a name="event-handlers"></a>Manipuladores de eventos  
 Os manipuladores de eventos no nível de contêiner respondem a eventos gerados pelo contêiner ou aos objetos nele incluídos. Para obter mais informações, consulte [Manipuladores de Eventos do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-event-handlers.md).  
  
### <a name="variables"></a>Variáveis  
 As variáveis usadas em contêineres incluem as variáveis do sistema no nível de contêiner fornecidas pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e as variáveis definidas pelo usuário usadas pelo contêiner. Para obter mais informações, consulte [Variáveis do SSIS &#40;Integration Services&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="break-points"></a>Pontos de interrupção  
 Quando você define um ponto de interrupção em um contêiner e a condição de interrupção é **Interromper quando o contêiner recebe o evento OnVariableValueChanged**, defina a variável no escopo de contêiner.  
  
## <a name="see-also"></a>Consulte Também  
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  
