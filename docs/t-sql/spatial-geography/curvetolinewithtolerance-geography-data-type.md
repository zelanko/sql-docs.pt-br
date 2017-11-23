---
title: CurveToLineWithTolerance (tipo de dados geography) | Microsoft Docs
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
- CurveToLineWithTolerance_TSQL
- CurveToLineWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- CurveToLineWithTolerance method (geography)
ms.assetid: 74369c76-2cf6-42ae-b9cc-e7a051db2767
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 712ba7cb9705769ae805503a47880d5f349351d1
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="curvetolinewithtolerance-geography-data-type"></a>CurveToLineWithTolerance (tipo de dados de geografia)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna uma aproximação poligonal de uma **geografia** instância que contém segmentos de arco circular.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.CurveToLineWithTolerance( tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumentos  
 *tolerância*  
 É um **duplo** expressão que define o erro máximo entre o segmento de arco circular original e sua aproximação linear.  
  
 *relativo*  
 É um **bool** indicando se deve usar um máximo relativo para o desvio de expressão. Quando o relativo é definido como falso (0), um máximo absoluto é definido para o desvio que um aproximado linear poderá ter.  Quando o relativo é definido como verdadeiro (1), a tolerância é calculada como um produto do parâmetro de tolerância e do diâmetro da caixa delimitadora do objeto espacial.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="exceptions"></a>Exceções  
 Definição da tolerância < = 0 lança um **ArgumentOutOfRange** exceção.  
  
## <a name="remarks"></a>Comentários  
 Esse método permite uma quantidade de tolerância de erro deve ser especificado para o resultante **LineString**.  
  
 **CurveToLineWithTolerance** método retornará um **LineString** instância para uma **CircularString** ou **CompoundCurve** instância e **Polígono** instância para uma **CurvePolygon** instância.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>A. Usando valores de tolerância diferentes em uma instância de CircularString  
 O exemplo a seguir mostra como a definição da tolerância afeta a `LineString`instância retornada de um `CircularString` instância:  
  
 ```
 DECLARE @g geography;  
 SET @g = geography::Parse('CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.01, 0).STNumPoints();
```  
  
### <a name="b-using-the-method-on-a-multilinestring-instance-containing-one-linestring"></a>B. Usando o método em uma instância de MultiLineString que contém uma LineString  
 O exemplo a seguir mostra o que é retornado de uma instância de `MultiLineString` que só contém uma instância de `LineString`:  
  
 ```
 DECLARE @g geography;  
 SET @g = geography::Parse('MULTILINESTRING((-122.358 47.653, -122.348 47.649))');  
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="c-using-the-method-on-a-multilinestring-instance-containing-multiple-linestrings"></a>C. Usando o método em uma instância de MultiLineString que contém várias LineStrings  
 O exemplo a seguir mostra o que é retornado de uma instância de `MultiLineString` que contém mais de uma instância `LineString`:  
  
 ```
 DECLARE @g geography;  
 SET @g = geography::Parse('MULTILINESTRING((-122.358 47.653, -122.348 47.649),(-123.358 47.653, -123.348 47.649))');  
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="d-setting-relative-to-true-for-an-invoking-curvepolygon-instance"></a>D. Definindo o relativo como true para uma instância de CurvePolygon de invocação  
 O exemplo a seguir usa uma `CurvePolygon` instância para chamar `CurveToLineWithTolerance()` com *relativo* definido como true:  
  
 ```
 DECLARE @g geography = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658), (-122.348 47.658, -122.358 47.658, -122.358 47.653)))';  
 SELECT @g.CurveToLineWithTolerance(.5,1).ToString();
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de Geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  

