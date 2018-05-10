---
title: STCurveN (tipo de dados geography) | Microsoft Docs
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
- STCurveN
- STCurveN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveN method (geography)
ms.assetid: 99ef7100-2c4b-4f07-8d66-b343da94b023
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c31bd46b13388d8ccb0fcb80d9af2ad8d79967f9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="stcurven-geography-data-type"></a>STCurveN (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna a curva especificada de um instância de **geography** que é uma **LineString**, uma **CircularString** ou uma **CompoundCurve**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STCurveN( n )  
```  
  
## <a name="arguments"></a>Argumentos  
 *n*  
 É uma expressão **int** entre 1 e o número de curvas na instância de **geography**.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="exceptions"></a>Exceções  
 Se n < 1, uma **ArgumentOutOfRangeException** será gerada.  
  
## <a name="remarks"></a>Remarks  
 **NULL** será retornado quando o seguinte critério ocorrer.  
  
-   A instância de **geography** for declarada, mas não for criada uma instância dela  
  
-   A instância de **geography** estiver vazia  
  
-   n exceder o número de curvas na instância de **geography** (confira [STNumCurves &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md)  
  
-   A dimensão da instância de **geography** não for igual a (confira [STDimension &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/stdimension-geography-data-type.md)  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-stcurven-on-a-circularstring"></a>A. Usando STCurveN() em uma CircularString  
 O exemplo a seguir retorna a segunda curva em uma instância de **CircularString**:  
  
```
 DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 Os resultados do exemplo.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve"></a>B. Usando STCurveN() em uma instância de CompoundCurve  
 O exemplo a seguir retorna a segunda curva em uma instância de **CompoundCurve**:  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 Os resultados do exemplo.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-containing-three-circularstrings"></a>C. Usando STCurveN() em um CompoundCurve que contém três CircularStrings  
 O exemplo a seguir usa uma instância de **CompoundCurve** que combina três instâncias de **CircularString** separadas na mesma sequência de curva, como no exemplo anterior:  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE (CIRCULARSTRING (-122.358 47.653, -122.348 47.649, -122.348 47.658), CIRCULARSTRING(-122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 Os resultados do exemplo.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
 `STCurveN()` retorna os mesmos resultados independentemente do formato de texto Conhecido (WKT) usado.  
  
### <a name="d-testing-for-validity-before-calling-stcurve"></a>D. Testando a validade antes de chamar STCurve()  
 O seguinte exemplo mostra como ter certeza de que *n* é válido antes de chamar o método STCurveN():  
  
```
 DECLARE @g geography;  
 DECLARE @n int;  
 SET @n = 2;  
 SET @g = geography::Parse('LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 IF @n >= 1 AND @n <= @g.STNumCurves()  
 BEGIN  
 SELECT @g.STCurveN(@n).ToString();  
 END
  ```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
