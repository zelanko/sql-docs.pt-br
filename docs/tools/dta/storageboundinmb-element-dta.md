---
title: Elemento StorageBoundInMB (DTA) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- StorageBoundInMB element
ms.assetid: a8374910-bf68-4edb-b464-53a3a705e7f4
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9be01bd27f8a3ad4a878e8b5340f2a4e0aead79e
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="storageboundinmb-element-dta"></a>Elemento StorageBoundInMB (DTA)
  Especifica o espaço de máximo em megabytes que podem ser consumidos pela recomendação de ajuste do Orientador de Otimização do Mecanismo de Banco de Dados (índice e conjunto de particionamento).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <StorageBoundInMB>...</ StorageBoundInMB >  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**unsignedInt**, comprimento ilimitado.|  
|**Valor padrão**|Nenhuma.|  
|**Ocorrência**|Opcional. Só pode ser usado uma vez para o elemento **TuningOptions** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento TuningOptions &#40; DTA &#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos filho**|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Quando múltiplos bancos de dados são ajustados, as recomendações para todos os bancos de dados são consideradas no cálculo do espaço. Por padrão, o Orientador de Otimização do Mecanismo de Banco de Dados assume o menor dos seguintes tamanhos de armazenamento:  
  
-   Três vezes o tamanho de dados brutos atuais, o que inclui o tamanho total de heaps e índices clusterizados em tabelas.  
  
-   Os espaços livres em todas as unidades de disco anexas mais o tamanho dos dados brutos.  
  
 O tamanho de armazenamento padrão não inclui índices não clusterizados e exibições indexadas.  
  
 Se o valor especificado para o elemento **StorageBoundInMB** exceder o espaço de disco atual, o Orientador de Otimização do Mecanismo de Banco de Dados retorna um erro, mas continua o ajuste. Depois que o ajuste estiver completo, você pode acrescentar espaço de disco caso decida implementar a recomendação.  
  
## <a name="example"></a>Exemplo  
  
## <a name="description"></a>Descrição  
 O seguinte exemplo de código mostra como definir um limite de 1500 megabytes como o espaço de disco de máximo que uma recomendação de ajuste pode consumir:  
  
## <a name="code"></a>Código  
  
```  
<DTAInput>  
  <Server>...</Server>  
  <Workload>...</Workload>  
  <TuningOptions>  
    <StorageBoundInMB>1500</StorageBoundInMB>  
...code removed here...  
</DTAInput>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  

