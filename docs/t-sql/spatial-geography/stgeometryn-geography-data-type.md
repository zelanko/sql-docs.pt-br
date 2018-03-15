---
title: STGeometryN (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STGeometryN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryN method
ms.assetid: 53755f69-cd50-475b-b3b8-a1a9157cf03a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e92224c6ea0aae9ad389353a705f3c1c3c9aa21c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="stgeometryn-geography-data-type"></a>STGeometryN (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna um elemento **geography** especificado em uma **GeometryCollection** ou um de seus subtipos. Quando STGeometryN() é usado em um subtipo de uma **GeometryCollection**, como **MultiPoint** ou **MultiLineString**, esse método retorna a instância de **geography** se é chamado com N=1.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STGeometryN ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 Uma expressão **int** entre 1 e o número de instâncias de **geography** na **GeometryCollection**.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Esse método retornará nulo se o parâmetro for maior que o resultado de [STNumGeometries()](../../t-sql/spatial-geography/stnumgeometries-geography-data-type.md) e gerará uma **ArgumentOutOfRangeException** se o parâmetro *expression* for menor que 1.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `MultiPoint``geography` e usa `STGeometryN()` para localizar a segunda instância de `geography` da **GeometryCollection**.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STGeometryN(2).ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
