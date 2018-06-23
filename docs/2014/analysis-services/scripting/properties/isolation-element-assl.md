---
title: Elemento Isolation (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Isolation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Isolation element
ms.assetid: 28c98c6f-668e-4547-8d25-127cc3995a7d
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cdcbf79ccd1281c9f3dbaa109b3c77214ced22bf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009003"
---
# <a name="isolation-element-assl"></a>Elemento Isolation (ASSL)
  Indica o nível de isolamento para um elemento que é derivado de [DataSource](../data-type/datasource-data-type-assl.md) tipo de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataSource>  
   ...  
   <Isolation>...</Isolation>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*ReadCommitted*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Fonte de dados](../data-type/datasource-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*ReadCommitted*|Especifica que as instruções não podem ler dados que foram modificados, mas que ainda não foram confirmados por outras transações. Isso impede leituras sujas. Outras transações podem alterar dados entre instruções individuais dentro da transação atual. Isso resulta em leituras que não podem ser repetidas ou dados fantasmas. Esse valor é o padrão para o elemento `Isolation`.|  
|*Instantâneo*|Especifica que os dados lidos por qualquer instrução em uma transação serão a versão transacionalmente consistente dos dados que existiam no início da transação. A transação pode visualizar apenas as modificações de dados que estavam confirmadas antes do início da transação. As modificações de dados efetuadas por outras transações após o início da transação atual não são visíveis às instruções em execução na transação atual. O efeito será como se as instruções em uma transação obtivessem um instantâneo dos dados confirmados conforme existiam no início da transação.|  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  