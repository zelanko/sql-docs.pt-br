---
title: STCurveN (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STCurveN
- STCurveN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveN method (geography)
ms.assetid: 99ef7100-2c4b-4f07-8d66-b343da94b023
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d33b8e6752ac8aca3bc6846a4558af4830373081
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stcurven-geography-data-type"></a>STCurveN (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna a curva especificada de um **geografia** instância que é um **LineString**, **CircularString**, ou **CompoundCurve**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STCurveN( n )  
```  
  
## <a name="arguments"></a>Argumentos  
 *n*  
 É um **int** expressão entre 1 e o número de curvas no **geografia** instância.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="exceptions"></a>Exceções  
 Se n < 1, em seguida, uma **ArgumentOutOfRangeException** é gerada.  
  
## <a name="remarks"></a>Comentários  
 **NULO** é retornado quando ocorre o seguinte critério.  
  
-   O **geografia** instância é declarada, mas não é instanciada  
  
-   O **geografia** instância está vazia  
  
-   n excede o número de curvas no **geografia** instância (consulte [STNumCurves &#40; tipo de dados geography &#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md)  
  
-   A dimensão para a **geografia** instância não é igual a (consulte [STDimension &#40; tipo de dados geography &#41;](../../t-sql/spatial-geography/stdimension-geography-data-type.md)  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-stcurven-on-a-circularstring"></a>A. Usando stcurven () em um CircularString  
 O exemplo a seguir retorna a segunda curva em uma **CircularString** instância:  
  
 `DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';`  
  
 `SELECT @g.STCurveN(2).ToString();`  
  
 Os resultados do exemplo.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve"></a>B. Usando STCurveN() em uma instância de CompoundCurve  
 O exemplo a seguir retorna a segunda curva em uma **CompoundCurve** instância:  
  
 `DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';`  
  
 `SELECT @g.STCurveN(2).ToString();`  
  
 Os resultados do exemplo.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-containing-three-circularstrings"></a>C. Usando STCurveN() em um CompoundCurve que contém três CircularStrings  
 O exemplo a seguir usa uma **CompoundCurve** instância que combina três separado **CircularString** instâncias na mesma sequência de curva como no exemplo anterior:  
  
 `DECLARE @g geography = 'COMPOUNDCURVE (CIRCULARSTRING (-122.358 47.653, -122.348 47.649, -122.348 47.658), CIRCULARSTRING(-122.348 47.658, -122.358 47.658, -122.358 47.653))';`  
  
 `SELECT @g.STCurveN(2).ToString();`  
  
 Os resultados do exemplo.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
 `STCurveN()` retorna os mesmos resultados independentemente do formato de texto Conhecido (WKT) usado.  
  
### <a name="d-testing-for-validity-before-calling-stcurve"></a>D. Testando a validade antes de chamar STCurve()  
 O exemplo a seguir mostra como certificar-se de que  *n*  é válido antes de chamar o método stcurven ():  
  
 `DECLARE @g geography;`  
  
 `DECLARE @n int;`  
  
 `SET @n = 2;`  
  
 `SET @g = geography::Parse('LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');`  
  
 `IF @n >= 1 AND @n <= @g.STNumCurves()`  
  
 `BEGIN`  
  
 `SELECT @g.STCurveN(@n).ToString();`  
  
 `END`  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de Geografia](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
