---
title: STMLineFromText (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STMLineFromText (geometry Data Type)
- STMLineFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STMLineFromText (geometry Data Type)
ms.assetid: 39fe8559-c4c2-4d61-8508-86eb0a103807
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 9b8e09118b13c016bbd8abedbfb009c76d9661e9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762340"
---
# <a name="stmlinefromtext-geometry-data-type"></a>STMLineFromText (tipo de dados geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna uma instância de **geometry** de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) aumentada com valores Z (elevação) e M (medida) presentes na instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
STMLineFromText ( 'multilinestring_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *multilinestring_tagged_text*  
 É a representação WKT da instância de **geometryMultiLineString** que você deseja retornar. *multilinestring_tagged_text* é uma expressão **nvarchar(max)** .  
  
 *SRID*  
 É uma expressão **int** que representa a SRID (ID de referência espacial) da instância de **geometryMultiLineString** que você deseja retornar.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
 Tipo do OGC: **MultiLineString**  
  
## <a name="remarks"></a>Comentários  
 Esse método gerará uma **FormatException** se a entrada não for bem formatada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STMLineFromText()` para criar uma instância `geometry`.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STMLineFromText('MULTILINESTRING ((100 100, 200 200), (3 4, 7 8, 10 10))', 0);  
```  
  
 `SELECT @g.ToString();`  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos geometry estáticos OGC](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

