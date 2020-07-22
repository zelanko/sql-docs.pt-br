---
title: AsGml (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AsGml(geometry_Data_Type)_TSQL
- AsGml
- AsGml(geometry Data Type)
- AsGml_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsGml (geometry Data Type)
ms.assetid: f6c2e130-05f3-4ef3-921b-d78b51437d48
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 61673238e63ac43d30811d3ff983917ce916a6b5
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555711"
---
# <a name="asgml-geometry-data-type"></a>AsGml (tipo de dados geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna a representação GML (Geography Markup Language) de uma instância de **geometry**.
  
Para obter mais informações sobre Geography Markup Language, confira a seguinte especificação do Open Geospatial Consortium:[Especificação do OGC, Geography Markup Language.](https://go.microsoft.com/fwlink/?LinkId=93629)
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.AsGml ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo de retorno [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **XML**  
  
 Tipo de retorno do CLR: **SqlXml**  
  
## <a name="remarks"></a>Comentários  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `LineString` e usa `AsGML()` para retornar uma descrição GML da instância.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0)', 0)  
SELECT @g.AsGml();  
```  
  
 Esse método retorna a descrição como uma instância `LineString`.  
  
```  
<LineString xmlns="https://www.opengis.net/gml">  
<posList>0 0 0 1 1 0</posList></LineString>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

