---
description: BufferWithTolerance (tipo de dados geography)
title: BufferWithTolerance (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BefferWithTolerance method
ms.assetid: f1783e6b-0f17-464f-b1c7-1c3f7d8aa042
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: e278c50b6a467660c827e3e59181945fdb9985e7
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035799"
---
# <a name="bufferwithtolerance-geography-data-type"></a>BufferWithTolerance (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna um objeto geométrico que representa a união de todos os valores de pontos cuja distância em relação a uma instância de **geography** é menor ou igual a um valor especificado, permitindo uma tolerância especificada.  
  
Esse método de tipo de dados de geography é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
_distance_  
É uma expressão **float** que especifica a distância da instância de **geography** ao redor da qual calcular o buffer.  
  
A distância máxima do buffer não pode exceder 0,999 \* _π_ * minorAxis \* minorAxis / majorAxis (~0,999 \* 1/2 circunferência da Terra) ou o globo inteiro.  
  
_tolerance_  
É uma expressão **float** que especifica a tolerância da distância do buffer.  
  
A variação máxima na distância ideal do buffer para a aproximação linear retornada é o valor de _tolerance_.  
  
Por exemplo, a distância ideal de buffer de um ponto é um círculo, mas essa distância deve ser aproximada por um polígono. Quanto menor a tolerância, mais pontos o polígono terá. Esse resultado aumenta a complexidade do resultado, mas minimiza o erro.  
  
O limite mínimo é 0,1 por cento da distância; qualquer tolerância menor que isso será arredondada até o limite mínimo.  
  
_relative_  
É um **bit** que especifica se o valor de _tolerance_ é relativo ou absoluto. Se o valor for 'TRUE' ou 1, a tolerância é relativa. Esse valor é o produto do parâmetro _tolerance_ e da extensão angular \* o raio equatorial do elipsoide. A tolerância será absoluta se o valor for 'FALSE' ou 0. O valor de _tolerance_ é a variação máxima absoluta na distância ideal do buffer para a aproximação linear retornada.  
  
## <a name="return-types"></a>Tipos de retorno  
Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentários  
Esse método gerará uma **ArgumentException** se a _distance_ for NaN (não é um número) ou se _distance_ for um infinito positivo ou negativo.  Este método também gerará uma **ArgumentException** se _tolerance_ for zero (0), NaN (não é um número), negativo ou infinito positivo ou negativo.  
  
`STBuffer()` retornará uma instância de **FullGlobe** em alguns casos; por exemplo, `STBuffer()` retorna uma instância de **FullGlobe** em dois pólos quando a distância do buffer é maior que a distância do Equador para os pólos.  
  
Esse método gerará uma **ArgumentException** em instâncias de **FullGlobe** nas quais a distância do buffer exceder a seguinte limitação:  
  
0,999 \* _π_ * minorAxis \* minorAxis / majorAxis (~0,999 \* 1/2 circunferência da Terra)  
  
O erro entre o buffer teórico e o calculado é max(tolerance, extents \* 1.E-7), em que a tolerância é o valor do parâmetro _tolerance_. Para obter mais informações sobre extensões, consulte [Referência de método do tipo de dados geography](./stequals-geography-data-type.md).  
  
Esse método não oferece precisão.  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir cria uma instância `Point` e usa `BufferWithTolerance()` para obter um buffer grosseiro à sua volta.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
[STBuffer &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/stbuffer-geography-data-type.md)   
[Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
