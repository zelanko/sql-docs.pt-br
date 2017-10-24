---
title: BufferWithCurves (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 08/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BufferWithCurves
- BufferWithCurves_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithCurves method (geography)
ms.assetid: abf0a11c-c99c-4faa-bf80-3ae8e04d7bfb
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 80f16777999a029e1063305a0d1b8501af7e05d7
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="bufferwithcurves-geography-data-type"></a>BufferWithCurves (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna um **geografia** instância que representa o conjunto de todos os pontos cuja distância da chamada **geografia** instância é menor que ou igual a *distância* parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>Argumentos  
 *distância*  
 É um **float** que indica a distância máxima em que os pontos que formam o buffer podem estar da instância de geography.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="exceptions"></a>Exceções  
 Os critérios a seguir lançará um **ArgumentException**.  
  
-   Nenhum parâmetro é transmitido ao método como `@g.BufferWithCurves()`  
  
-   Um parâmetro não numérico é transmitido ao método como `@g.BufferWithCurves('a')`  
  
-   **NULO** é transmitido ao método, como`@g.BufferWithCurves(NULL)`  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir mostra os resultados retornados para obter valores de distância diferentes.  
  
|Valor de distância|Dimensões do tipo|Tipo espacial retornado|  
|--------------------|---------------------|---------------------------|  
|distância < 0|Zero ou um|Vazio **GeometryCollection** instância|  
|distância \< 0|Dois ou mais|Um **CurvePolygon** ou **GeometryCollection** instância com um buffer negativo.<br /><br /> Observação: Um buffer negativo pode criar vazio **GeometryCollection**|
|distância = 0|Todas as dimensões|Cópia de invocando **geografia** instância|  
|distância > 0|Todas as dimensões|**CurvePolygon** ou **GeometryCollection** instância|  
  
> [!NOTE]  
>  Como *distância* é um **float**, um valor muito pequeno pode equivaler a zero nos cálculos.  Quando isso ocorre, em seguida, uma cópia da chamada **geografia** instância será retornada.  
  
 Se um **cadeia de caracteres** parâmetro é passado para o método, em seguida, ele será convertido em um **float** ou lançará um `ArgumentException`.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-calling-bufferwithcurves-with-a-parameter-value--0-on-one-dimensional-geography-instance"></a>A. Chamando BufferWithCurves() com um valor de parâmetro < 0 em instância de geografia unidimensional  
 O exemplo a seguir retorna uma instância `GeometryCollection` vazia:  
  
 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(-1).ToString();
``` 
  
### <a name="b-calling-bufferwithcurves-with-a-parameter-value--0-on-a-two-dimensional-geography-instance"></a>B. Chamando BufferWithCurves() com um valor de parâmetro < 0 em instância de geografia bidimensional  
 O exemplo a seguir retorna uma instância `CurvePolygon` com um buffer negativo:  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-1).ToString()
 ```  
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>C. Chamando BufferWithCurves() com um valor de parâmetro < 0 que retorna uma GeometryCollection vazia  
 O exemplo a seguir mostra o que ocorre quando o *distância* parâmetro for igual a -2:  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 Isso **selecione** instrução retorna`GEOMETRYCOLLECTION EMPTY`  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>D. Chamando BufferWithCurves() com um valor de parâmetro = 0  
 O exemplo a seguir retorna uma cópia da chamada **geografia** instância:  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>E. Chamando BufferWithCurves() com um valor de parâmetro diferente de zero que é extremamente pequeno  
 O exemplo a seguir também retorna uma cópia da chamada **geografia** instância:  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>F. Chamando BufferWithCurves() com um valor de parâmetro > 0  
 O exemplo a seguir retorna uma instância `CurvePolygon`:  

 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(2).ToString();
 ```  
### <a name="g-passing-a-valid-string-parameter"></a>G. Transmitindo um parâmetro de cadeia de caracteres válido  
 O exemplo a seguir retorna a mesma instância `CurvePolygon` como mencionado anteriormente, mas um parâmetro de cadeia de caracteres é passado ao método:  

 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves('2').ToString();
```  
  
### <a name="h-passing-an-invalid-string-parameter"></a>H. Transmitindo um parâmetro de cadeia de caracteres inválido  
 O exemplo a seguir lançará um erro:  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)'  
 SELECT @g.BufferWithCurves('a').ToString();
 ```  
  
 Observe que os dois exemplos anteriores transmitiram uma cadeia de caracteres literal ao método `BufferWithCurves()`. O primeiro exemplo funciona porque o literal de cadeia de caracteres pode ser convertido em um valor numérico. Porém, o segundo exemplo lança `ArgumentException`.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de Geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [BufferWithCurves & #40; tipo de dados geometry & #41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
  

