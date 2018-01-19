---
title: CurveToLineWithTolerance (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: CurveToLineWithTolerance method (geometry)
ms.assetid: 96871075-1998-4cd9-86b1-3fc55577aee4
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2f7429f54395b5a765c84939aac2ce7fe0a94c08
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="curvetolinewithtolerance-geometry-data-type"></a>CurveToLineWithTolerance (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna uma aproximação poligonal de uma **geometria** instância que contém segmentos de arco circular.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.CurveToLineWithTolerance ( tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumentos  
 *tolerance*  
 É um **duplo** expressão que define o erro máximo entre o segmento de arco circular original e sua aproximação linear.  
  
 *relative*  
 É um **bool** expressão que indica se deve usar um máximo relativo para o desvio. Quando o relativo é definido como falso (0), um máximo absoluto é definido para o desvio que um aproximado linear poderá ter. Quando o relativo é definido como verdadeiro (1), a tolerância é calculada como um produto do parâmetro de tolerância e do diâmetro da caixa delimitadora do objeto espacial.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
## <a name="exceptions"></a>Exceções  
 A definição da tolerância <= 0 lança uma exceção `ArgumentOutOfRange`.  
  
## <a name="remarks"></a>Remarks  
 Esse método pode especificar um valor de tolerância de erro para o resultante **LineString**.  
  
 A tabela a seguir mostra o tipo de instância retornado por `CurveToLineWithTolerance()`para vários tipos.  
  
|Invocando tipo de instância|Tipo espacial retornado|  
|----------------------------|---------------------------|  
|instância de geometry vazia|Vazio **GeometryCollection** instância|  
|**Ponto** e **MultiPoint**|**Ponto** instância|  
|**MultiPoint**|**Ponto** ou **MultiPoint** instância|  
|**CircularString**, **CompoundCurve**, ou **LineString**|**LineString** instância|  
|**MultiLineString**|**LineString** ou **MultiLineString** instância|  
|**CurvePolygon** e **polígono**|**Polígono** instância|  
|**MultiPolygon**|**Polígono** ou **MultiPolygon** instância|  
|**GeometryCollection** com uma única instância que não contém um segmento de arco circular|A instância que está contida no **GeometryCollection** determina o tipo de instância retornada.|  
|**GeometryCollection** com uma instância de segmento único arco circular unidimensional (**CircularString**, **CompoundCurve**)|**LineString** instância|  
|**GeometryCollection** com uma instância de segmento único arco circular bidimensional (**CurvePolygon**)|**Polígono** instância|  
|**GeometryCollection** com várias instâncias unidimensionais|**MultiLineString** instância|  
|**GeometryCollection** com várias instâncias bidimensionais|**MultiPolygon** instância|  
|**GeometryCollection** com várias instâncias de dimensões diferentes|**GeometryCollection** instância|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>A. Usando valores de tolerância diferentes em uma instância de CircularString  
 O exemplo a seguir mostra como a definição da tolerância afeta a `LineString`instância retornada de um `CircularString` instância:  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.01, 0).STNumPoints();
 ```  
  
### <a name="b-using-the-method-on-a-multilinestring-instance-containing-one-linestring"></a>B. Usando o método em uma instância de MultiLineString que contém uma LineString  
 O exemplo a seguir mostra o que é retornado de uma instância de `MultiLineString` que só contém uma instância de `LineString`:  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('MULTILINESTRING((1 3, 4 8, 6 9))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="c-using-the-method-on-a-multilinestring-instance-containing-multiple-linestrings"></a>C. Usando o método em uma instância de MultiLineString que contém várias LineStrings  
 O exemplo a seguir mostra o que é retornado de uma instância de `MultiLineString` que contém mais de uma instância `LineString`:  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('MULTILINESTRING((1 3, 4 8, 6 9),(4 4, 9 18))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="d-setting-relative-to-true-for-an-invoking-curvepolygon-instance"></a>D. Definindo o relativo como true para uma instância de CurvePolygon de invocação  
 O exemplo a seguir usa uma `CurvePolygon` instância para chamar `CurveToLineWithTolerance()` com *relativo* definido como true:  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.CurveToLineWithTolerance(.5,1).ToString();
 ```  
  
### <a name="e-using-the-method-on-a-geometrycollection-instance"></a>E. Usando o método em uma instância de GeometryCollection  
 O exemplo a seguir chama `CurveToLineWithTolerance()` em um `GeometryCollection` que contém uma instância de `CurvePolygon` bidimensional e uma instância de `CircularString` unidimensional. `CurveToLineWithTolerance()` converte os dois tipos de segmento de arco circular para revestir tipos de segmento e os retorna em um tipo `GeometryCollection`.  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('GEOMETRYCOLLECTION(CURVEPOLYGON( COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 0 2))), CIRCULARSTRING(4 4, 8 6, 9 5))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.1, 0).ToString();
 ```  
  
## <a name="see-also"></a>Consulte também  
 [CurveToLineWithTolerance &#40; tipo de dados geography &#41;](../../t-sql/spatial-geography/curvetolinewithtolerance-geography-data-type.md)   
 [STCurveToLine &#40; tipo de dados geometry &#41;](../../t-sql/spatial-geometry/stcurvetoline-geometry-data-type.md)  
  
  

