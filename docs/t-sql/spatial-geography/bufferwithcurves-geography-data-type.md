---
title: BufferWithCurves (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 08/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BufferWithCurves
- BufferWithCurves_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithCurves method (geography)
ms.assetid: abf0a11c-c99c-4faa-bf80-3ae8e04d7bfb
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 81222e73df527d5d51a592dd2cabe62384b5f936
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65937323"
---
# <a name="bufferwithcurves-geography-data-type"></a>BufferWithCurves (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna uma instância de **geography** que representa o conjunto de todos os pontos cuja distância da instância de **geography** de chamada é menor ou igual ao parâmetro *distance*.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>Argumentos  
 *distance*  
 É um **float** que indica a distância máxima em que os pontos que formam o buffer podem estar da instância de geografia.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="exceptions"></a>Exceções  
 Os critérios a seguir gerarão uma **ArgumentException**.  
  
-   Nenhum parâmetro é transmitido ao método como `@g.BufferWithCurves()`  
  
-   Um parâmetro não numérico é transmitido ao método como `@g.BufferWithCurves('a')`  
  
-   **NULL** é passado ao método, como `@g.BufferWithCurves(NULL)`  
  
## <a name="remarks"></a>Remarks  
 A tabela a seguir mostra os resultados retornados para obter valores de distância diferentes.  
  
|Valor de distância|Dimensões do tipo|Tipo espacial retornado|  
|--------------------|---------------------|---------------------------|  
|distância < 0|Zero ou um|Instância de **GeometryCollection** vazia|  
|distância \< 0|Dois ou mais|Uma instância de **CurvePolygon** ou **GeometryCollection** com um buffer negativo.<br /><br /> Observação: Um buffer negativo pode criar uma **GeometryCollection** vazia|
|distância = 0|Todas as dimensões|Cópia da instância de **geography** de invocação|  
|distância > 0|Todas as dimensões|Instância de **CurvePolygon** ou **GeometryCollection**|  
  
> [!NOTE]  
>  Como *distance* é um **float**, um valor muito pequeno pode ser igualado a zero nos cálculos.  Quando isto ocorre, uma cópia da instância de **geography** de chamada é retornada.  
  
 Se um parâmetro **string** for passado ao método, ele será convertido em um **float** ou gerará uma `ArgumentException`.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-calling-bufferwithcurves-with-a-parameter-value--0-on-one-dimensional-geography-instance"></a>A. Como chamar BufferWithCurves() com um valor de parâmetro < 0 em instância de geografia unidimensional  
 O exemplo a seguir retorna uma instância `GeometryCollection` vazia:  
  
 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(-1).ToString();
``` 
  
### <a name="b-calling-bufferwithcurves-with-a-parameter-value--0-on-a-two-dimensional-geography-instance"></a>B. Como chamar BufferWithCurves() com um valor de parâmetro < 0 em uma instância de geografia bidimensional  
 O exemplo a seguir retorna uma instância `CurvePolygon` com um buffer negativo:  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-1).ToString()
 ```  
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>C. Como chamar BufferWithCurves() com um valor de parâmetro < 0 que retorna uma GeometryCollection vazia  
 O seguinte exemplo mostra o que ocorre quando o parâmetro *distance* é igual a -2:  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 Esta instrução **SELECT** retorna `GEOMETRYCOLLECTION EMPTY`  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>D. Chamando BufferWithCurves() com um valor de parâmetro = 0  
 O seguinte exemplo retorna uma cópia da instância de **geography** de chamada:  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>E. Chamando BufferWithCurves() com um valor de parâmetro diferente de zero que é extremamente pequeno  
 O seguinte exemplo também retorna uma cópia da instância de **geography** de chamada:  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>F. Como chamar BufferWithCurves() com um valor de parâmetro > 0  
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
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias de geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [BufferWithCurves &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
  
