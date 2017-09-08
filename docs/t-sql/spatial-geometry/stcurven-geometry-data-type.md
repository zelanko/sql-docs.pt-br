---
title: STCurveN (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveN method (geometry)
ms.assetid: 64adf1a1-3a41-41fb-b7d1-44390c3e4ea9
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dd5b459bfa271d98844d30455e4e1a9e03d0e2cd
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stcurven-geometry-data-type"></a>STCurveN (Tipo de Dados de geometria)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna a curva especificada de um **geometria** instância que é um **LineString**, **CircularString**, **CompoundCurve**, ou  **MultiLineString**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STCurveN ( curve_index )  
```  
  
## <a name="arguments"></a>Argumentos  
 *curve_index*  
 É um **int** expressão entre 1 e o número de curvas no **geometria** instância.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
## <a name="exceptions"></a>Exceções  
 Se *curve_index* < 1, em seguida, um `ArgumentOutOfRangeException` é gerada.  
  
## <a name="remarks"></a>Comentários  
 **NULO** é retornado quando ocorrer qualquer uma das seguintes opções:  
  
-   o **geometria** instância é declarada, mas não criar uma instância  
  
-   o **geometria** instância está vazia  
  
-   *curve_index* excede o número de curvas no **geometria** instância  
  
-   o **geometria** instância é um **ponto**, **MultiPoint**, **polígono**, **CurvePolygon**, ou  **MultiPolygon**  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-stcurven-on-a-circularstring-instance"></a>A. Usando STCurveN() em uma instância de CircularString  
 O exemplo a seguir retorna a segunda curva em uma instância de `CircularString`:  
  
 `DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';`  
  
 `SELECT @g.STCurveN(2).ToString();`  
  
 O exemplo anterior neste tópico retorna:  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve-instance-with-one-circularstring-instance"></a>B. Usando STCurveN() em uma instância de CompoundCurve com uma instância de CircularString  
 O exemplo a seguir retorna a segunda curva em uma instância de `CompoundCurve`:  
  
 `DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0))';`  
  
 `SELECT @g.STCurveN(2).ToString();`  
  
 O exemplo anterior neste tópico retorna:  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-instance-with-three-circularstring-instances"></a>C. Usando STCurveN() em uma instância de CompoundCurve com três instâncias de CircularString  
 O exemplo seguinte usa uma instância de `CompoundCurve` que combina três instâncias de `CircularString` separadas na mesma sequência de curva como o exemplo anterior:  
  
 `DECLARE @g geometry = 'COMPOUNDCURVE (CIRCULARSTRING (0 0, 1 2.1082, 3 6.3246), CIRCULARSTRING(3 6.3246, 0 7, -3 6.3246), CIRCULARSTRING(-3 6.3246, -1 2.1082, 0 0))';`  
  
 `SELECT @g.STCurveN(2).ToString();`  
  
 O exemplo anterior neste tópico retorna:  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
 Note que os resultados são os mesmos para os três exemplos anteriores. Qualquer que seja o formato WKT (Well-known Text) usado para inserir a mesma sequência de curva, os resultados retornados por `STCurveN()` serão os mesmos quando uma instância de `CompoundCurve` for usada.  
  
### <a name="d-validating-the-parameter-before-calling-stcurven"></a>D. Validando o parâmetro antes de chamar STCurveN()  
 O exemplo a seguir mostra como verificar se `@n` é válido antes de chamar o `STCurveN()`método:  
  
 `DECLARE @g geometry;`  
  
 `DECLARE @n int;`  
  
 `SET @n = 3;`  
  
 `SET @g = geometry::Parse('CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');`  
  
 `IF @n >= 1 AND @n <= @g.STNumCurves()`  
  
 `BEGIN`  
  
 `SELECT @g.STCurveN(@n).ToString();`  
  
 `END`  
  
## <a name="see-also"></a>Consulte também  
 [STNumCurves &#40; tipo de dados geometry &#41;](../../t-sql/spatial-geometry/stnumcurves-geometry-data-type.md)   
 [Métodos do OGC em instâncias de geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


