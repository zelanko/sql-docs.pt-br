---
title: AsGml (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4a4ca0fcd5b8b7b4ffdb39d3201f7060efe18a74
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="asgml-geometry-data-type"></a>AsGml (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna a representação GML Geography Markup Language () de um **geometria** instância.
  
Para obter mais informações sobre Geography Markup Language, consulte a seguinte especificação aberta da Consortium geoespaciais:[OGC Specifications, Geography Markup Language.](http://go.microsoft.com/fwlink/?LinkId=93629)
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.AsGml ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **xml**  
  
 Tipo de retorno CLR: **SqlXml**  
  
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
<LineString xmlns="http://www.opengis.net/gml">  
<posList>0 0 0 1 1 0</posList></LineString>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de geometria](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  


