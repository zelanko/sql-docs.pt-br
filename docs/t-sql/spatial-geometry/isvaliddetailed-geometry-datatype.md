---
title: "IsValidDetailed (DataType Geométrico) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- IsValidDetailed geometry
ms.assetid: 5a31e88a-ad7b-4ef7-b773-e2571f1cb3aa
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ecc088ca8a68406e9146ed1b74ff72c441cb235a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="isvaliddetailed-geometry-datatype"></a>IsValidDetailed (DataType geométrico)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna uma mensagem que pode ajudar a identificar problemas com um objeto espacial que não é válido. Quando o objeto não é válido, apenas o primeiro erro é retornado. Quando o objeto é válido, um valor de 24400 é retornado.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.IsValidDetailed()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **nvarchar (max)**  
  
 Tipo de retorno CLR: **cadeia de caracteres**  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir contém os valores de retorno possíveis:  
  
|Valor de retorno|Description|  
|------------------|-----------------|  
|24400|Válido|  
|24401|Não válido, motivo desconhecido.|  
|24402|Não válido porque o ponto {0} é um ponto isolado que não é válido nesse tipo de objeto.|  
|24403|Não válido porque algum par de bordas de polígono se sobrepõe.|  
|24404|Não válido porque o anel de polígono {0} apresenta interseção consigo mesmo ou com outro anel.|  
|24405|Não válido porque um anel de polígono apresenta interseção consigo mesmo ou com outro anel.|  
|24406|Não válido porque a curva {0} se degenera em um ponto.|  
|24407|Não é válido porque {0} do anel de polígono se recolhe em uma linha no ponto de \\{1 \\}.|  
|24408|Não válido porque o anel de polígono {0} não é fechado.|  
|24409|Não válido porque alguma parte do anel de polígono {0} está no interior de um polígono.|  
|24410|Não válido porque o anel {0} é o primeiro anel em um polígono do qual não é o anel exterior.|  
|24411|Não é válido porque o anel {0} está fora do \\{1 \\} do anel exterior de seu polígono.|  
|24412|Não é válido porque o interior de um polígono com anéis {0} e \\{1 \\} não está conectado.|  
|24413|Não válido devido a duas bordas sobrepostas em curva {0}.|  
|24414|Não é válido porque uma borda da curva {0} sobrepõe uma borda da curva \\{1 \\}.|  
|24415|Não válido porque algum polígono tem uma estrutura de anel inválida.|  
|24416|Não é válido porque na curva {0} a borda que começa no ponto \\{1 \\} é uma linha ou um arco degenerado com pontos de extremidade opostos.|  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir de um objeto espacial inválido ilustra como o **isvaliddetailed ()** métodos se comporta.  
  
```tsql  
DECLARE @p GEOMETRY = 'Polygon((2 2, 4 4, 4 2, 2 4, 2 2))'  
SELECT @p.IsValidDetailed()  
--Returns: 24404: Not valid because polygon ring (1) intersects itself or some other ring.  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de geometria](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  


