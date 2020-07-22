---
title: STEndPoint (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STEndPoint (geography Data Type)
- STEndPoint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STEndPoint method
ms.assetid: 8974cd07-8ec4-4126-8fc2-fdcf322ccedd
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 475b5e99cd7628992e90a2921c0bd726f8f69560
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554394"
---
# <a name="stendpoint-geography-data-type"></a>STEndPoint (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna o ponto de extremidade de uma instância de **geography**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STEndPoint ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
 Tipo do OGC (Open Geospatial Consortium): **Point**  
  
## <a name="remarks"></a>Comentários  
 STEndPoint() é o equivalente a [STPointN](../../t-sql/spatial-geography/stpointn-geography-data-type.md)`(x.STNumPoints``())`.  
  
 Esse método retornará nulo se for chamado em uma instância de **geography** vazia.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `LineString` com `STGeomFromText()` e usa `STEndPoint()` para recuperar o ponto de extremidade de `LineString`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STEndPoint().ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
