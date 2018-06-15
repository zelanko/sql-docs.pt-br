---
title: CurveToLineWithTolerance (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e5445cce83bfc6328606b4a2fa0f55ffe37587f1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33061783"
---
# <a name="curvetolinewithtolerance-geography-data-type"></a>CurveToLineWithTolerance (tipo de dados de geografia)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna uma aproximação poligonal de uma instância de **geography** que contém segmentos de arco circulares.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.CurveToLineWithTolerance( tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumentos  
 *tolerance*  
 É uma expressão **double** que define o erro máximo entre o segmento de arco circular original e sua aproximação linear.  
  
 *relative*  
 É uma expressão**booliana** que indica se um máximo relativo para o desvio deverá ser usado. Quando o relativo é definido como falso (0), um máximo absoluto é definido para o desvio que um aproximado linear poderá ter.  Quando o relativo é definido como verdadeiro (1), a tolerância é calculada como um produto do parâmetro de tolerância e do diâmetro da caixa delimitadora do objeto espacial.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="exceptions"></a>Exceções  
 A definição de tolerância <= 0 gera uma exceção **ArgumentOutOfRange**.  
  
## <a name="remarks"></a>Remarks  
 Esse método permite uma quantidade de tolerância de erro a ser especificada para a **LineString** resultante.  
  
 O método **CurveToLineWithTolerance** retornará uma instância de **LineString** para uma instância de **CircularString** ou de **CompoundCurve** e uma instância de  **Polígono** para uma instância de **CurvePolygon**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>A. Usando valores de tolerância diferentes em uma instância de CircularString  
 O seguinte exemplo mostra como a definição da tolerância afeta a instância de `LineString` retornada de uma instância de `CircularString`:  
  
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
 O exemplo a seguir usa uma instância de `CurvePolygon` para chamar `CurveToLineWithTolerance()` com *relativo* definido como true:  
  
 ```
 DECLARE @g geography = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658), (-122.348 47.658, -122.358 47.658, -122.358 47.653)))';  
 SELECT @g.CurveToLineWithTolerance(.5,1).ToString();
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
