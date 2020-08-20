---
description: STCurveN (tipo de dados geography)
title: STCurveN (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STCurveN
- STCurveN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveN method (geography)
ms.assetid: 99ef7100-2c4b-4f07-8d66-b343da94b023
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 18d3a992b3f3d5eeecb09a16ce3fb6d582ee2fb2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479329"
---
# <a name="stcurven-geography-data-type"></a>STCurveN (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna a curva especificada de um instância de **geography** que é uma **LineString**, uma **CircularString** ou uma **CompoundCurve**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STCurveN( n )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *n*  
 É uma expressão **int** entre 1 e o número de curvas na instância de **geography**.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="exceptions"></a>Exceções  
 Se n < 1, uma **ArgumentOutOfRangeException** será gerada.  
  
## <a name="remarks"></a>Comentários  
 **NULL** será retornado quando o seguinte critério ocorrer.  
  
-   A instância de **geography** for declarada, mas não for criada uma instância dela  
  
-   A instância de **geography** estiver vazia  
  
-   n exceder o número de curvas na instância de **geography** (confira [STNumCurves &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md)  
  
-   A dimensão da instância de **geography** não for igual a (confira [STDimension &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/stdimension-geography-data-type.md)  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-stcurven-on-a-circularstring"></a>a. Usando STCurveN() em uma CircularString  
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
 [Métodos do OGC em instâncias de geografia](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
