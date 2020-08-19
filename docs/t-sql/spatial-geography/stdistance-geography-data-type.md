---
description: STDistance (Tipo de dados geography)
title: STDistance (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDistance_TSQL
- STDistance (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDistance method
ms.assetid: 063d8722-e019-4d3d-8fcf-dbf5325823e7
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a20279a70d2e68e1cb4b34eb36ffe7de633518a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88416992"
---
# <a name="stdistance-geography-data-type"></a>STDistance (Tipo de dados geography)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  Retorna a distância mais curta entre um ponto em uma instância de **geography** e um ponto em outra instância de **geography**.  
  
> [!NOTE]  
>  `STDistance()` retorna a **LineString** mais curta entre dois tipos de geografia. Trata-se de uma aproximação para a distância geodésica. O desvio de `STDistance()` em modelos terrestres comuns da distância geodésica exata não é maior que 0,25%. Isso evita confusão quanto às diferenças mínimas entre o comprimento e a distância em tipos geodésicos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STDistance ( other_geography )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *other_geography*  
 É outra instância de **geography** da qual medir a distância entre a instância na qual STDistance() é invocado. Se *other_geography* for um conjunto vazio, STDistance() retornará nulo.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo de retorno do CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentários  
 O resultado é expresso na unidade de medida definida pelo [Identificador de Referência Espacial &#40;SRID&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md) de dados espaciais.
STDistance() sempre retornará *nulo* se os SRIDs (IDs de referência espacial) das instâncias de **geografia** não forem correspondentes.  
  
> [!NOTE]  
>  Métodos no tipo de dados **geography** que calculam uma área ou distância retornarão resultados diferentes com base no SRID da instância usado no método. Para obter mais informações sobre SRIDs, confira [SRIDs &#40;Spatial Reference Identifiers&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir localiza a distância entre duas instâncias de **geography**.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SET @h = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.STDistance(@h);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos do OGC em instâncias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
