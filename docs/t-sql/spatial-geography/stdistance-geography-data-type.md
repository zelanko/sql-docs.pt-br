---
title: STDistance (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STDistance_TSQL
- STDistance (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: STDistance method
ms.assetid: 063d8722-e019-4d3d-8fcf-dbf5325823e7
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9e0a059179710f258dae051ed7c901c1eaf27e15
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="stdistance-geography-data-type"></a>STDistance (Tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna a distância mais curta entre um ponto em um **geografia** instância e um ponto em outra **geografia** instância.  
  
> [!NOTE]  
>  `STDistance()`Retorna o menor **LineString** entre dois tipos de Geografia. Trata-se de uma aproximação para a distância geodésica. O desvio de `STDistance()` em modelos terrestres comuns da distância geodésica exata não mais do que. 25%. Isso evita confusão quanto às diferenças mínimas entre o comprimento e a distância em tipos geodésicos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STDistance ( other_geography )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geography*  
 É outra **geografia** instância da qual medir a distância entre a instância na qual stdistance () é invocado. Se *other_geography* vazio for definido, stdistance () retorna nulo.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **float**  
  
 Tipo de retorno CLR: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 Stdistance () sempre retornará nulo se as IDs de referência espaciais (SRIDs) da **geografia** instâncias não coincidem.  
  
> [!NOTE]  
>  Métodos de **geografia** tipo de dados que calculam uma área ou distância retornarão resultados diferentes com base na SRID da instância usada no método.   Para obter mais informações sobre SRIDs, consulte [Spatial Reference Identifiers &#40; SRIDs &#41; ](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir localiza a distância entre dois **geografia** instâncias.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SET @h = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.STDistance(@h);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
