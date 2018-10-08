---
title: Elemento StorageBoundInMB (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- StorageBoundInMB element
ms.assetid: a8374910-bf68-4edb-b464-53a3a705e7f4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3f869c8e2aa06be9f1ba7605d89576b62bdc0ed5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47710734"
---
# <a name="storageboundinmb-element-dta"></a>Elemento StorageBoundInMB (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Opcional. Só pode ser usado uma vez para o elemento **TuningOptions** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos filho**|None|  
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
