---
title: Elemento OnlineIndexOperation (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- OnlineIndexOperation element
ms.assetid: 7c5614cd-09aa-4a59-9591-347aa7d36473
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9bb877ae48153d4fabae13170eb5f072218012d6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62657211"
---
# <a name="onlineindexoperation-element-dta"></a>Elemento OnlineIndexOperation (DTA)
  Especifica se os índices, as exibições indexadas ou as partições que o Database Engine Tuning Advisor recomenda podem ser criados online.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <OnlineIndexOperation>...</OnlineIndexOperation>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|DESCRIÇÃO|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|`string`, nenhum tamanho máximo.|  
|**Valores permitidos**|**OFF**<br /> Nenhuma estrutura de design físico recomendada pode ser criada online.<br /><br /> **ON**<br /> Todas as estruturas de design físico recomendadas podem ser criadas online.<br /><br /> **MIXED**<br /> O Orientador de Otimização do Mecanismo de Banco de Dados tenta recomendar estruturas de design físico que podem ser criadas online quando possível.<br /><br /> Use um desses valores com esse elemento. Se os índices são criados online, a palavra-chave **ONLINE = ON** será acrescentada à definição de seus objetos.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Opcional. Se usado, só pode ser utilizado uma vez para o elemento `TuningOptions`.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento TuningOptions &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivos de entrada XML simples &#40;DTA&#41;](simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
