---
title: IsValidDetailed (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IsValidDetailed_TSQL
- IsValidDetailed
dev_langs:
- TSQL
helpviewer_keywords:
- IsValidDetailed geography
ms.assetid: f5f0b753-c825-43ce-987d-98655d8d8702
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 5bbe4c8cf9f6084282f37353aede357d5086ddc6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65937681"
---
# <a name="isvaliddetailed-geography-data-type"></a>IsValidDetailed (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna uma mensagem que pode ajudar a identificar problemas com um objeto espacial que não é válido. Quando o objeto não é válido, apenas o primeiro erro é retornado. Quando o objeto é válido, um valor de 24400 é retornado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.IsValidDetailed()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **nvarchar(max)**  
  
 Tipo de retorno do CLR: **string**  
  
## <a name="remarks"></a>Remarks  
 A tabela a seguir contém os valores de retorno possíveis:  
  
|Valor retornado|Descrição|  
|------------------|-----------------|  
|24400|Válido|  
|24401|Não válido, motivo desconhecido.|  
|24402|Não válido porque o ponto {0} é um ponto isolado que não é válido nesse tipo de objeto.|  
|24403|Não válido porque algum par de bordas de polígono se sobrepõe.|  
|24404|Não válido porque um anel de polígono {0} apresenta interseção consigo mesmo ou com outro anel.|  
|24405|Não válido porque um anel de polígono apresenta interseção consigo mesmo ou com outro anel.|  
|24406|Não válido porque a curva {0} se degenera em um ponto.|  
|24407|Não válido porque o anel do polígono {0} é recolhido em uma linha no ponto {1}.|  
|24408|Não válido porque o anel de polígono {0} não é fechado.|  
|24409|Não válido porque alguma parte do anel de polígono {0} está no interior de um polígono.|  
|24410|Não válido porque o anel {0} é o primeiro anel em um polígono do qual não é o anel exterior.|  
|24411|Não válido porque o anel {0} está fora do anel exterior {1} de seu polígono.|  
|24412|Não válido porque o interior de um polígono com anéis {0} e {1} não está conectado.|  
|24413|Não válido devido a duas bordas sobrepostas em curva {0}.|  
|24414|Não válido porque uma borda da curva {0} se sobrepõe a uma borda da curva {1}.|  
|24415|Não válido porque algum polígono tem uma estrutura de anel inválida.|  
|24416|Não válido porque na curva {0} a borda que inicia no ponto {1} é uma linha ou um arco degenerado com pontos de extremidade opostos.|  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir de um objeto espacial inválido ilustra como os métodos **IsValidDetailed()** se comportam.  
  
```sql  
DECLARE @p GEOGRAPHY = 'Polygon((2 2, 4 4, 4 2, 2 4, 2 2))'  
SELECT @p.IsValidDetailed()  
--Returns: 24409: Not valid because some portion of polygon ring (1) lies in the interior of a polygon.  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
