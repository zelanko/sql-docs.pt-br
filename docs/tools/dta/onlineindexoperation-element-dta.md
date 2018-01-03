---
title: Elemento OnlineIndexOperation (DTA) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: OnlineIndexOperation element
ms.assetid: 7c5614cd-09aa-4a59-9591-347aa7d36473
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dd8acd696b9aa2ddfe200adba618d848657df5f7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="onlineindexoperation-element-dta"></a>Elemento OnlineIndexOperation (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Especifica se os índices, exibições indexadas ou partições que o orientador de otimização do mecanismo de banco de dados recomenda podem ser criadas online.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <OnlineIndexOperation>...</OnlineIndexOperation>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**string**, nenhum tamanho máximo.|  
|**Valores permitidos**|**OFF**<br /> Nenhuma estrutura de design físico recomendada pode ser criada online.<br /><br /> **ON**<br /> Todas as estruturas de design físico recomendadas podem ser criadas online.<br /><br /> **MIXED**<br /> O Orientador de Otimização do Mecanismo de Banco de Dados tenta recomendar estruturas de design físico que podem ser criadas online quando possível.<br /><br /> Use um desses valores com esse elemento. Se os índices são criados online, a palavra-chave **ONLINE = ON** será acrescentada à definição de seus objetos.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Opcional. Se usado, só pode ser utilizado uma vez para o elemento **TuningOptions** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivos de entrada XML simples &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
