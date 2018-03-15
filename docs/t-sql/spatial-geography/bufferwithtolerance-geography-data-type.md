---
title: BufferWithTolerance (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
f1_keywords:
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BefferWithTolerance method
ms.assetid: f1783e6b-0f17-464f-b1c7-1c3f7d8aa042
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bb70f24c521fd5f0325ecbb718e7d76aa43f935d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="bufferwithtolerance-geography-data-type"></a>BufferWithTolerance (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna um objeto geométrico que representa a união de todos os valores de pontos cuja distância em relação a uma instância de **geography** é menor ou igual a um valor especificado, permitindo uma tolerância especificada.  
  
 Esse método de tipo de dados de geography é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumentos  
 *distance*  
 É uma expressão **float** que especifica a distância da instância de **geography** ao redor da qual calcular o buffer.  
  
 A distância máxima do buffer não pode exceder 0,999 \* *π* * minorAxis \* minorAxis / majorAxis (~0,999 \* 1/2 circunferência da Terra) ou o globo inteiro.  
  
 *tolerance*  
 É uma expressão **float** que especifica a tolerância da distância do buffer.  
  
 O valor de *tolerance* refere-se à variação máxima na distância ideal do buffer para a aproximação linear retornada.  
  
 Por exemplo, a distância ideal de buffer de um ponto é um círculo, mas deve ser aproximado por um polígono. Quanto menor a tolerância, mais pontos o polígono terá, o que aumenta a complexidade do resultado, mas diminui o erro.  
  
 O limite mínimo é 0,1 por cento da distância; qualquer tolerância menor que isso será arredondada até o limite mínimo.  
  
 *relative*  
 É um **bit** que especifica se o valor de *tolerance* é relativo ou absoluto. Se for 'TRUE' ou 1, a tolerância será relativa e será calculada como o produto do parâmetro *tolerance* e da extensão angular \* o raio equatorial do elipsoide. Se for 'FALSE' ou 0, a tolerância será absoluta e o valor de *tolerance* será a variação máxima absoluta na distância ideal do buffer para a aproximação linear retornada.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Esse método gerará uma **ArgumentException** se a *distance* for NaN (não é um número) ou se *distance* for um infinito positivo ou negativo.  Este método também gerará uma **ArgumentException** se *tolerance* for zero (0), NaN (não é um número), negativo ou infinito positivo ou negativo.  
  
 `STBuffer()` retornará uma instância de **FullGlobe** em alguns casos; por exemplo, `STBuffer()` retorna uma instância de **FullGlobe** em dois pólos quando a distância do buffer é maior que a distância do Equador para os pólos.  
  
 Esse método gerará uma **ArgumentException** em instâncias de **FullGlobe** nas quais a distância do buffer exceder a seguinte limitação:  
  
 0,999 \* *π* * minorAxis \* minorAxis / majorAxis (~0,999 \* 1/2 da circunferência da Terra)  
  
 O erro entre o buffer teórico e o calculado é max(tolerance, extents \* 1.E-7), em que a tolerância é o valor do parâmetro *tolerance*. Para obter mais informações sobre extensões, consulte [Referência de método do tipo de dados geography](http://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e).  
  
 Esse método não é preciso.  
  
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
  
  
