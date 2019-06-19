---
title: LAT (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Lat
- Lat_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Lat method
ms.assetid: 051d66bc-04de-4c58-861c-760dc5b859b5
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 03e9aa242fd76579f17090c17257a865ebb927ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65937666"
---
# <a name="lat-geography-data-type"></a>Lat (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  A propriedade de latitude da instância de **geography**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
.Lat  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo CLR: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 No modelo OpenGIS, Lat só é definida nas instâncias de **geografia** compostas por um único ponto. Essa propriedade retornará NULL se instâncias de **geography** contiverem mais de um ponto. Essa propriedade é exata e somente leitura.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo cria um ponto e retorna a latitude do ponto.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Lat;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
