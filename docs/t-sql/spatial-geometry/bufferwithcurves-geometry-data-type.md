---
title: BufferWithCurves (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithCurves method (geometry)
ms.assetid: 8ffaba3f-d2dd-4e57-9f41-3ced9f14b600
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: e31b83159646ed2b5a42dc53fff700e49847791e
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39455100"
---
# <a name="bufferwithcurves-geometry-data-type"></a>BufferWithCurves (tipo de dados geometria)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Retorna uma instância de **geometry** que representa o conjunto de todos os pontos cuja distância da instância de **geometry** de chamada é menor ou igual ao parâmetro *distance*.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>Argumentos  
 *distance*  
 É um **float** que indica a distância máxima em que os pontos que formam o buffer podem estar da instância de **geometry**.  
  
## <a name="return-types"></a>Tipos de retorno  
Tipo de retorno do SQL Server: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
## <a name="exceptions"></a>Exceções  
 Os critérios a seguir gerarão uma **ArgumentException**.  
  
-   Nenhum parâmetro é passado ao método, como `@g.BufferWithCurves()`  
  
-   Um parâmetro não numérico é passado para o método, como `@g.BufferWithCurves('a')`  
  
-   **NULL** é passado ao método, como `@g.BufferWithCurves(NULL)`  
  
## <a name="remarks"></a>Remarks  
 A ilustração a seguir mostra um exemplo de uma instância de geometria retornado por este método.  
  
 ![BufferedCurve](../../t-sql/spatial-geometry/media/bufferedcurve.gif)
  
 A tabela a seguir mostra os resultados retornados para obter valores de distância diferentes.  
  
|Valor de distância|Dimensões do tipo|Tipo espacial retornado|  
|--------------------|---------------------|---------------------------|  
|distância < 0|Zero ou um|Instância de **GeometryCollection** vazia|  
|distância < 0|Dois ou mais|Uma instância de **CurvePolygon** ou **GeometryCollection** com um buffer negativo. **Observação:** um buffer negativo pode criar uma **GeometryCollection** vazia|  
|distância = 0|Todas as dimensões|Cópia da instância de **geometry** de invocação|  
|distância > 0|Todas as dimensões|Instância de **CurvePolygon** ou **GeometryCollection**|  
  
> [!NOTE]  
>  Como *distance* é um **float**, um valor muito pequeno pode ser igualado a zero nos cálculos. Quando isto ocorre, uma cópia da instância de **geometry** de chamada é retornada. Consulte [float e real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
 Um buffer negativo remove todos os pontos incluídos na distância especificada do limite da geometria. A ilustração a seguir mostra um buffer negativo como a área sombreada mais clara do círculo. A linha pontilhada é o limite do polígono original e a linha sólida é o limite do polígono resultante.  
  
 Se um parâmetro **string** for passado ao método, ele será convertido em um **float** ou gerará uma `ArgumentException`.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-calling-bufferwithcurves-with-a-parameter-value--0-on-one-dimensional-geometry-instance"></a>A. Chamando BufferWithCurves() com um valor de parâmetro < 0 em instância de geometria unidimensional  
 O exemplo a seguir retorna uma instância `GeometryCollection` vazia:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(-1).ToString(); 
 ```
  
### <a name="b-calling-bufferwithcurves-with-a-parameter-value--0-on-a-two-dimensional-geometry-instance"></a>B. Chamando BufferWithCurves() com um valor de parâmetro < 0 em instância de geometria bidimensional  
 O exemplo a seguir retorna uma instância `CurvePolygon` com um buffer negativo:  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.BufferWithCurves(-1).ToString()
 ```  
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>C. Chamando BufferWithCurves() com um valor de parâmetro < 0 que retorna uma GeometryCollection vazia  
 O seguinte exemplo mostra o que ocorre quando o parâmetro *distance* é igual a -2:  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 Esta instrução **SELECT** retorna `GEOMETRYCOLLECTION EMPTY`  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>D. Chamando BufferWithCurves() com um valor de parâmetro = 0  
 O seguinte exemplo retorna uma cópia da instância de **geometry** de chamada:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>E. Chamando BufferWithCurves() com um valor de parâmetro diferente de zero que é extremamente pequeno  
 O seguinte exemplo também retorna uma cópia da instância de **geometry** de chamada:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 DECLARE @distance float = 1e-20; 
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>F. Chamando BufferWithCurves() com um valor de parâmetro > 0  
 O exemplo a seguir retorna uma instância `CurvePolygon`:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(2).ToString();
 ```  
  
### <a name="g-passing-a-valid-string-parameter"></a>G. Transmitindo um parâmetro de cadeia de caracteres válido  
 O exemplo a seguir retorna a mesma instância `CurvePolygon` como mencionado anteriormente, mas um parâmetro de cadeia de caracteres é passado ao método:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves('2').ToString();
 ```  
  
### <a name="h-passing-an-invalid-string-parameter"></a>H. Transmitindo um parâmetro de cadeia de caracteres inválido  
 O exemplo a seguir lançará um erro:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)' 
 SELECT @g.BufferWithCurves('a').ToString();
 ```  
  
 Observe que os dois exemplos anteriores transmitiram uma cadeia de caracteres literal ao método `BufferWithCurves()`. O primeiro exemplo funciona porque o literal de cadeia de caracteres pode ser convertido em um valor numérico. Porém, o segundo exemplo lança `ArgumentException`.  
  
### <a name="i-calling-bufferwithcurves-on-multipoint-instance"></a>I. Chamando BufferWithCurves() em instância de MultiPoint  
 O exemplo a seguir retorna duas instâncias `GeometryCollection` e uma instância `CurvePolygon`:  
  
```
 DECLARE @g geometry = 'MULTIPOINT((1 1),(1 4))'; 
 SELECT @g.BufferWithCurves(1).ToString(); 
 SELECT @g.BufferWithCurves(1.5).ToString(); 
 SELECT @g.BufferWithCurves(1.6).ToString();
 ```  
  
 As duas primeiras instruções **SELECT** retornam uma instância de `GeometryCollection` porque o parâmetro *distance* é menor ou igual a 1/2 da distância entre os dois pontos, (1 1) e (1 4). A terceira instrução **SELECT** retorna uma instância de `CurvePolygon` porque as instâncias armazenadas em buffer dos dois pontos, (1 1) e (1 4), se sobrepõem.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
 
