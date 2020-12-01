---
description: STLength (tipo de dados geography)
title: STLength (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STLength (geography Data Type)
- STLength_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLength method
ms.assetid: 774560ab-4a4a-4058-b043-1e67cf6fb9eb
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 5fe53017aa78bd4025a251611fd6f50c67d4401a
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88445151"
---
# <a name="stlength-geography-data-type"></a>STLength (tipo de dados geography)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  Retorna o comprimento total dos elementos em uma instância de **geography** ou nas instâncias de **geografia** em uma **GeometryCollection**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STLength ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo de retorno do CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentários  
 Se uma instância de **geography** for fechada, seu comprimento será calculado como o comprimento total em torno da instância. O comprimento de qualquer polígono é seu perímetro, e o comprimento de um ponto é 0. O comprimento de uma **GeometryCollection** é encontrado calculando a soma dos comprimentos de todas as instâncias de **geografia** contidas dentro da coleção.  
  
 STLength () funciona em LineStrings válidos e inválidos. Em geral, um LineString é inválido devido aos segmentos sobrepostos, que podem ser causados por anomalias como rastreamentos de GPS imprecisos. STLength () não remove segmentos sobrepostos ou inválidos. Ele inclui segmentos sobrepostos e inválidos no valor de comprimento que ele retorna. O método MakeValid () pode remover segmentos sobrepostos de um LineString.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `LineString` e usa `STLength()` para encontrar o comprimento da instância.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STLength();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos do OGC em instâncias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
