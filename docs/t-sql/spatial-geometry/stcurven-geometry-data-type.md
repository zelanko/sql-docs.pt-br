---
title: STCurveN (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
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
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveN method (geometry)
ms.assetid: 64adf1a1-3a41-41fb-b7d1-44390c3e4ea9
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 496934186af543eb5a7263245c90ce7309112d10
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="stcurven-geometry-data-type"></a>STCurveN (Tipo de Dados de geometria)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna a curva especificada de uma instância de **geometry** que é uma **LineString**, uma **CircularString**, uma **CompoundCurve** ou uma **MultiLineString**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STCurveN ( curve_index )  
```  
  
## <a name="arguments"></a>Argumentos  
 *curve_index*  
 É uma expressão **int** entre 1 e o número de curvas na instância de **geometry**.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
## <a name="exceptions"></a>Exceções  
 Se *curve_index* < 1, uma `ArgumentOutOfRangeException` será gerada.  
  
## <a name="remarks"></a>Remarks  
 **NULL** é retornado quando ocorre uma das seguintes opções:  
  
-   a instância de **geometry** é declarada, mas não é criada uma instância dela  
  
-   a instância de **geometry** está vazia  
  
-   *curve_index* excede o número de curvas na instância de **geometry**  
  
-   a instância de **geometry** é um **Point**, um **MultiPoint**, um **Pplygon**, um **CurvePolygon** ou um **MultiPolygon**  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-stcurven-on-a-circularstring-instance"></a>A. Usando STCurveN() em uma instância de CircularString  
 O exemplo a seguir retorna a segunda curva em uma instância de `CircularString`:  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 O exemplo anterior neste tópico retorna:  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve-instance-with-one-circularstring-instance"></a>B. Usando STCurveN() em uma instância de CompoundCurve com uma instância de CircularString  
 O exemplo a seguir retorna a segunda curva em uma instância de `CompoundCurve`:  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 O exemplo anterior neste tópico retorna:  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-instance-with-three-circularstring-instances"></a>C. Usando STCurveN() em uma instância de CompoundCurve com três instâncias de CircularString  
 O exemplo seguinte usa uma instância de `CompoundCurve` que combina três instâncias de `CircularString` separadas na mesma sequência de curva como o exemplo anterior:  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE (CIRCULARSTRING (0 0, 1 2.1082, 3 6.3246), CIRCULARSTRING(3 6.3246, 0 7, -3 6.3246), CIRCULARSTRING(-3 6.3246, -1 2.1082, 0 0))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 O exemplo anterior neste tópico retorna:  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
 Note que os resultados são os mesmos para os três exemplos anteriores. Qualquer que seja o formato WKT (Well-known Text) usado para inserir a mesma sequência de curva, os resultados retornados por `STCurveN()` serão os mesmos quando uma instância de `CompoundCurve` for usada.  
  
### <a name="d-validating-the-parameter-before-calling-stcurven"></a>D. Validando o parâmetro antes de chamar STCurveN()  
 O exemplo a seguir mostra como verificar se `@n` é válido antes de chamar o método `STCurveN()`:  
  
```
 DECLARE @g geometry;  
 DECLARE @n int;  
 SET @n = 3;  
 SET @g = geometry::Parse('CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');  
 IF @n >= 1 AND @n <= @g.STNumCurves()  
 BEGIN  
 SELECT @g.STCurveN(@n).ToString();  
 END
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [STNumCurves &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stnumcurves-geometry-data-type.md)   
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

