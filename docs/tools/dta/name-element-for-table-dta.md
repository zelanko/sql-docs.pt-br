---
title: Nome de elemento de tabela (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Name element
ms.assetid: 422a755f-ee52-4863-b1aa-f4ef1b8fd0bb
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 525f18c180337358abd98d84b59276448729e0bc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33068353"
---
# <a name="name-element-for-table-dta"></a>Elemento de nome de tabela (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Especifica um nome de tabela para ajuste.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Schema>  
    <Table>  
        <Name>...</Name>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**string**, entre 1 e 255 caracteres.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Obrigatórios. Uma vez para cada elemento de **Table** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Table para Schema &#40;DTA&#41;](../../tools/dta/table-element-for-schema-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso, veja [Elemento Server&#40;DTA&#41;](../../tools/dta/server-element-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
