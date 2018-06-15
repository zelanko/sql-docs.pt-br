---
title: Elemento Isolation (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b8233ce2fc5d987dac6511fee978e45b213601a2
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34030907"
---
# <a name="isolation-element-assl"></a>Elemento Isolation (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Indica o nível de isolamento para um elemento que é derivado de [DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md) tipo de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataSource>  
   ...  
   <Isolation>...</Isolation>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*ReadCommitted*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Fonte de dados](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|*ReadCommitted*|Especifica que as instruções não podem ler dados que foram modificados, mas que ainda não foram confirmados por outras transações. Isso impede leituras sujas. Outras transações podem alterar dados entre instruções individuais dentro da transação atual. Isso resulta em leituras que não podem ser repetidas ou dados fantasmas. Esse valor é o padrão para o elemento **Isolation** .|  
|*Instantâneo*|Especifica que os dados lidos por qualquer instrução em uma transação serão a versão transacionalmente consistente dos dados que existiam no início da transação. A transação pode visualizar apenas as modificações de dados que estavam confirmadas antes do início da transação. As modificações de dados efetuadas por outras transações após o início da transação atual não são visíveis às instruções em execução na transação atual. O efeito será como se as instruções em uma transação obtivessem um instantâneo dos dados confirmados conforme existiam no início da transação.|  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
