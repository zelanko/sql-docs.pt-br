---
title: STBuffer (tipo de dados geometry) | Microsoft Docs
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
f1_keywords:
- STBuffer (geometry Data Type)
- STBuffer_TSQL
dev_langs: TSQL
helpviewer_keywords: STBuffer (geometry Data Type)
ms.assetid: ca6bf2dc-1d38-4503-b87e-f2ea033d36ba
caps.latest.revision: "29"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cb93bd550570b94b1a924a20d6243e808209adec
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="stbuffer-geometry-data-type"></a>STBuffer (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um objeto geométrico que representa a união de todos os pontos cuja distância de uma **geometria** instância é menor ou igual ao valor especificado.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STBuffer ( distance )  
```  
  
## <a name="arguments"></a>Argumentos  
 *distância*  
 É um valor do tipo **float** (**duplo** no .NET Framework) Especifica a distância da instância geometry ao redor do qual o buffer será calculado.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentários  
 `STBuffer()`calcula um buffer, como [BufferWithTolerance](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md), especificando *tolerância* = distância \* .001 e *relativo*  =   **False**.  
  
 Quando *distância* > 0, uma um **polígono** ou **MultiPolygon** instância será retornada.  
  
> [!NOTE]  
>  Como a distância é um **float**, um valor muito pequeno pode equivaler a zero nos cálculos.  Quando isso ocorre, uma cópia da chamada **geometria** instância será retornada.  Consulte [float e real &#40; Transact-SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
  
 Quando *distância* = 0 e, em seguida, uma cópia da chamada **geometria** instância será retornada.  
  
 Quando *distância* < 0, em seguida,  
  
-   vazio **GeometryCollection** instância é retornada quando as dimensões da instância são 0 ou 1.  
  
-   um buffer negativo é retornado quando as dimensões da instância são 2 ou mais.  
  
    > [!NOTE]  
    >  Um buffer negativo também pode criar um vazio **GeometryCollection** instância.  
  
 Um buffer negativo remove todos os incluídos na distância especificada do limite da geometria.  
  
 O erro entre o buffer teórico e calculado é max (tolerância, extensões * 1. e-7) onde tolerância = distância \* .001. Para obter mais informações sobre extensões, consulte [referência de método do tipo de dados geometry](http://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-calling-stbuffer-with-parametervalue--0-on-one-dimensional-geometry-instance"></a>A. Chamando STBuffer() com um parameter_value < 0 em uma instância de geometry unidimensional  
 O exemplo a seguir retorna uma instância `GeometryCollection` vazia:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
### <a name="b-calling-stbuffer-with-parametervalue--0-on-a-polygon-instance"></a>B. Chamando STBuffer() com parameter_value < 0 em uma instância de Polygon  
 O exemplo a seguir retorna uma instância `Polygon` com um buffer negativo:  
  
```
 DECLARE @g geometry = 'POLYGON((1 1, 1 5, 5 5, 5 1, 1 1))'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
### <a name="c-calling-stbuffer-with-parametervalue--0-on-a-curvepolygon-instance"></a>C. Chamando STBuffer() com parameter_value < 0 em uma instância de CurvePolygon  
 O exemplo a seguir retorna uma instância `Polygon` com um buffer negativo de uma instância `CurvePolygon`:  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
> [!NOTE]  
>  Uma instância `Polygon` é retornada, em vez de uma instância `CurvePolygon`.  Para retornar um `CurvePolygon` da instância, consulte [BufferWithCurves &#40; tipo de dados geometry &#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
### <a name="d-calling-stbuffer-with-a-negative-parameter-value-that-returns-an-empty-instance"></a>D. Chamando STBuffer() com um valor de parâmetro negativo que retorna uma instância vazia  
 O exemplo a seguir mostra o que ocorre quando o *distância* parâmetro for igual a -2 para o exemplo anterior.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.STBuffer(-2).ToString();
 ```  
  
 Isso **selecione** instrução retorna um`GEOMETRYCOLLECTION EMPTY.`  
  
### <a name="e-calling-stbuffer-with-parametervalue--0"></a>E. Chamando STBuffer() com parameter_value = 0  
 O exemplo a seguir retorna uma cópia da instância `geometry` de chamada:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(0).ToString();
 ```  
  
### <a name="f-calling-stbuffer-with-a-non-zero-parameter-value-that-is-extremely-small"></a>F. Chamando STBuffer() com um valor de parâmetro diferente de zero que é extremamente pequeno  
 O exemplo a seguir também retorna uma cópia da instância `geometry` de chamada:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.STBuffer(@distance).ToString();
 ```  
  
### <a name="g-calling-stbuffer-with-parametervalue--0"></a>G. Chamando STBuffer() com parameter_value > 0  
 O exemplo a seguir retorna uma instância `Polygon`:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(2).ToString();
 ```  
  
### <a name="h-calling-stbuffer-with-a-string-parameter-value"></a>H. Chamando STBuffer() com um valor de parâmetro de cadeia de caracteres  
 O exemplo a seguir retorna a mesma instância `Polygon` como mencionado anteriormente, mas um parâmetro de cadeia de caracteres é passado ao método:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer('2').ToString();
 ```  
  
 O exemplo a seguir lançará um erro:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer('a').ToString();
 ```  
  
> [!NOTE]  
>  Os dois exemplos anteriores passaram um literal de cadeia de caracteres a `STBuffer()`.  O primeiro exemplo funciona porque o literal de cadeia de caracteres pode ser convertido em um valor numérico. Porém, o segundo exemplo lança `ArgumentException`.  
  
### <a name="i-calling-stbuffer-on-a-multipoint-instance"></a>I. Chamando STBuffer() em instância de MultiPoint  
 O exemplo a seguir retorna duas instâncias `MultiPolygon` e uma instância `Polygon`:  
  
```
 DECLARE @g geometry = 'MULTIPOINT((1 1),(1 4))'; 
 SELECT @g.STBuffer(1).ToString(); 
 SELECT @g.STBuffer(1.5).ToString(); 
 SELECT @g.STBuffer(1.6).ToString();
 ```  
  
 Os dois primeiros **selecione** instruções retornam uma `MultiPolygon` instância porque o parâmetro *distância* é menor ou igual a 1/2 a distância entre os dois pontos (1 1) e (1 4). O terceiro **selecione** instrução retorna um `Polygon` instância porque as instâncias armazenadas em buffer dos dois pontos (1 1) e (1 4) se sobrepõem.  
  
## <a name="see-also"></a>Consulte também  
 [BufferWithTolerance &#40; tipo de dados geometry &#41;](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md)   
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

