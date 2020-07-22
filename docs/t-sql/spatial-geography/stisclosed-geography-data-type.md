---
title: STIsClosed (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsClosed (geography Data Type)
- STIsClosed_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIsClosed method
ms.assetid: eba1643f-07c4-4500-8643-b7e90f908147
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 06190fa6cc6a0377e49f423c50369a7ceb4b51d7
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555744"
---
# <a name="stisclosed-geography-data-type"></a>STIsClosed (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retornará 1 se os pontos inicial e final da instância de **geography** fornecida forem o mesmo. Retornará 1 para tipos de coleção de **geografia**, se cada instância de **geography** contida estiver fechada. Retornará 0 se a instância não for fechada.  
  
 Esse método de tipo de dados de **geography** é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STIsClosed ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de retorno do CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentários  
 Esse método retornará 0 se alguma figura de uma instância de **geography** for um ponto ou se a instância estiver vazia.  
  
 Esse método retornará true se uma instância de **FullGlobe** for um **polígono** ou outro tipo de instância.  
  
 As instâncias de **polígono** são consideradas fechadas.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `Polygon` e usa `STIsClosed()` para testar se `Polygon` está fechada.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STIsClosed();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
