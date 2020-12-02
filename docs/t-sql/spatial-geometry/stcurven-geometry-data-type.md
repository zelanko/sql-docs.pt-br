---
description: STCurveN (Tipo de Dados de geometria)
title: STCurveN (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveN method (geometry)
ms.assetid: 64adf1a1-3a41-41fb-b7d1-44390c3e4ea9
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: e182b7c5670bd86e0d684d1d8caaea563a2ff456
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88467373"
---
# <a name="stcurven-geometry-data-type"></a>STCurveN (Tipo de Dados de geometria)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

Retorna a curva especificada de uma instância de **geometry** que é uma **LineString**, uma **CircularString**, uma **CompoundCurve** ou uma **MultiLineString**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STCurveN ( curve_index )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *curve_index*  
 É uma expressão **int** entre 1 e o número de curvas na instância de **geometry**.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
## <a name="exceptions"></a>Exceções  
 Se *curve_index* < 1, uma `ArgumentOutOfRangeException` será gerada.  
  
## <a name="remarks"></a>Comentários  
 **NULL** é retornado quando ocorre uma das seguintes opções:  
  
-   a instância de **geometry** é declarada, mas não é criada uma instância dela  
  
-   a instância de **geometry** está vazia  
  
-   *curve_index* excede o número de curvas na instância de **geometry**  
  
-   a instância de **geometry** é um **Point**, um **MultiPoint**, um **Pplygon**, um **CurvePolygon** ou um **MultiPolygon**  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-stcurven-on-a-circularstring-instance"></a>a. Usando STCurveN() em uma instância de CircularString  
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
  
  

