---
title: Definir uma variável de estado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 45d66152-883a-49a7-a877-2e8ab45f8f79
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4b0dcc3c1709943207834aab6ef4b39453b2d89d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62827561"
---
# <a name="define-a-state-variable"></a>Definir uma variável de estado
  Este procedimento descreve como definir uma variável de pacote onde o estado CDC é armazenado.  
  
 A variável de estado CDC é carregada, inicializada e atualizada pela tarefa Controle de CDC e é usada pelo componente de fluxo de dados de Origem CDC para determinar o intervalo de processamento atual para alterar registros. A variável de estado CDC pode ser definida em qualquer contêiner comum à tarefa de Controle de CDC e à origem CDC. Isso pode estar no nível do pacote, mas pode estar também em outros contêineres, como um contêiner de loop.  
  
 A modificação manual do valor da variável de estado CDC não é recomendável, no entanto, isso pode ser útil para entender seu conteúdo.  
  
 A tabela a seguir fornece uma descrição de alto nível dos componentes do valor da variável de estado CDC.  
  
|Componente|Descrição|  
|---------------|-----------------|  
|`<state-name>`|Este é o nome do estado CDC atual.|  
|`CS`|Isso marca o ponto inicial do intervalo de processamento atual (Início atual).|  
|`<cs-lsn>`|Este é último LSN (número de sequência de log) processado na execução CDC anterior.|  
|`CE`|Isso marca o ponto final do intervalo de processamento atual (Término atual). A presença do componente de término atual no estado CDC é uma indicação de que ou um pacote CDC está atualmente em processamento ou um pacote de CDC falhou antes de processar completamente seu intervalo de processamento CDC.|  
|`<ce-lsn>`|Este é o último LSN a ser processado na execução CDC atual. Sempre presumimos que o último número de sequência a ser processado é o máximo (0xFFF…).|  
|`IR`|Isso marca o intervalo de processamento inicial.|  
|`<ir-start>`|Este é o LSN de uma alteração imediatamente antes de a carga inicial ter sido iniciada.|  
|`<ir-end>`|Este é o LSN de uma alteração imediatamente depois de a carga inicial ter sido terminada.|  
|`TS`|Isso marca o carimbo de data/hora para a última atualização do estado CDC.|  
|**\<carimbo de data/hora>**|Essa é uma representação decimal da propriedade System.DateTime.UtcNow de 64 bits.|  
|`ER`|Isso aparece quando a última operação falhou e inclui uma descrição breve da causa do erro. Se esse componente estiver presente, ela será sempre o último.|  
|`<short-error-text>`|Essa é a descrição curta do erro.|  
  
 Os LSNs e os números de sequência são codificados como uma cadeia de caracteres hexadecimal de até 20 dígitos que representam o valor LSN do binário (10).  
  
 A tabela a seguir descreve os valores de estado CDC possíveis.  
  
|Estado|Descrição|  
|-----------|-----------------|  
|(INITIAL)|Esse é o estado inicial antes de qualquer pacote ter sido executado no grupo de CDC atual. Este também é o estado quando o estado de CDC está vazio.|  
|ILSTART (Initial Load Started)|Esse é o estado do início do pacote de carga inicial, depois da chamada da operação de `MarkInitialLoadStart` para a tarefa Controle CDC.|  
|ILEND (Initial Load Ended)|Esse é o estado do término bem-sucedido do pacote de carga inicial, depois da chamada da operação de `MarkInitialLoadEnd` para a tarefa Controle CDC.|  
|ILUPDATE (Initial Load Update)|Este é o estado nas execuções do pacote de atualização trickle feed depois da carga inicial, enquanto ainda processa o intervalo de processamento inicial. Isto ocorre depois da chamada da operação `GetProcessingRange` para a tarefa Controle CDC.<br /><br /> Se estiver usando a coluna __$reprocessing, ela será definida como 1 para indicar que o pacote pode estar reprocessando linhas já no destino.|  
|TFEND (Trickle-Feed Update Ended)|Este é o estado esperado para execuções regulares de CDC. Ele indica que a execução anterior foi concluída com êxito e que uma nova execução com um novo intervalo de processamento pode ser iniciada.|  
|TFSTART|Este é o estado em uma execução não inicial do pacote de atualização trickle feed depois que a operação `GetProcessingRange` chama a tarefa Controle CDC.<br /><br /> Isto indica que uma execução CDC regular foi iniciada, mas não foi concluída ou ainda não foi concluída completamente (`MarkProcessedRange`).|  
|TFREDO (Reprocessing Trickle-Feed Updates)|Este é o estado em um `GetProcessingRange` que ocorre depois de TFSTART. Isto indica que a execução anterior não foi concluída com êxito.<br /><br /> Se estiver usando a coluna __$reprocessing, ela será definida como 1 para indicar que o pacote pode estar reprocessando linhas já no destino.|  
|ERROR|O grupo de CDC está em um estado de ERROR.|  
  
 Os seguintes são exemplos de valores de variável de estado CDC.  
  
-   ILSTART/IR/0x0000162B158700000000//TS/2011-08-07T17:10:43.0031645/  
  
-   ILSTART/IR/0x0000162B158700000000//TS/2011-08-07T17:10:43.0031645/  
  
-   TFEND/CS/0x0000025B000001BC0003/TS/2011-07-17T12:05:58.1001145/  
  
-   TFSTART/CS/0x0000030D000000AE0003/CE/0x0000159D1E0F01000000/TS/2011-08-09T05:30:43.9344900/  
  
-   TFREDO/CS/0x0000030D000000AE0003/CE/0x0000159D1E0F01000000/TS/2011-08-09T05:30:59.5544900/  
  
### <a name="to-define-a-cdc-state-variable"></a>Para definir uma variável de estado CDC  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tem o fluxo de CDC onde você precisa definir a variável.  
  
2.  Clique na guia **Explorador de Pacotes** e adicione uma nova variável.  
  
3.  Dê a variável um nome que você possa reconhecer como sua variável de estado.  
  
4.  Atribua à variável um tipo de dados **String** .  
  
 Não dê à variável um valor como parte de sua definição. O valor deve ser definido pela tarefa Controle de CDC.  
  
 Se você estiver planejando usar a tarefa Controle de CDC com **Persistência de Estado Automática**, a variável de Estado CDC será lida a partir da tabela de estado de banco de dados especificada e será atualizada para a mesma tabela quando seu valor for alterado. Para obter mais informações sobre a tabela de Estado, consulte [CDC Control Task](../control-flow/cdc-control-task.md)e [CDC Control Task Editor](../cdc-control-task-editor.md).  
  
 Se você não estiver usando a tarefa de Controle CDC com a Persistência de Estado Automática, deverá carregar o valor da variável a partir do repositório persistente em que seu valor foi salvo da última vez que o pacote foi executado e gravá-la no repositório persistente quando o processamento do intervalo atual for concluído.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefa Controle de CDC](../control-flow/cdc-control-task.md)   
 [Editor da Tarefa Controle de CDC](../cdc-control-task-editor.md)  
  
  
