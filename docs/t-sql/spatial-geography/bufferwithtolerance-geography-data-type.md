---
title: BufferWithTolerance (tipo de dados geography) | Microsoft Docs
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
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BefferWithTolerance method
ms.assetid: f1783e6b-0f17-464f-b1c7-1c3f7d8aa042
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: feaa401cfd6e2077035d164412941392412011ae
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="bufferwithtolerance-geography-data-type"></a>BufferWithTolerance (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna valores de um objeto geométrico que representa a união de todos os pontos cuja distância de uma **geografia** instância é menor ou igual ao valor especificado, permitindo uma tolerância especificada.  
  
 Esses dados de Geografia digite método dá suporte a **FullGlobe** instâncias ou a instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumentos  
 *distância*  
 É um **float** expressão que especifica a distância entre o **geografia** instância em torno da qual calcular o buffer.  
  
 A distância máxima do buffer não pode exceder 0,999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 circunferência da Terra) ou o globo inteiro.  
  
 *tolerância*  
 É um **float** expressão que especifica a tolerância da distância do buffer.  
  
 O *tolerância* valor refere-se à variação máxima na distância ideal do buffer para a aproximação linear retornada.  
  
 Por exemplo, a distância ideal de buffer de um ponto é um círculo, mas deve ser aproximado por um polígono. Quanto menor a tolerância, mais pontos o polígono terá, o que aumenta a complexidade do resultado, mas diminui o erro.  
  
 O limite mínimo é 0,1 por cento da distância; qualquer tolerância menor que isso será arredondada até o limite mínimo.  
  
 *relativo*  
 É um **bit** especificando se o *tolerância* valor é relativo ou absoluto. Se 'TRUE' ou 1, tolerância será relativa e calculada como o produto do *tolerância* parâmetro e da extensão angular \* raio equatorial do elipsoide. Se 'FALSE' ou 0, tolerância será absoluta e o *tolerância* valor é a variação máxima absoluta na distância ideal do buffer para a aproximação linear retornada.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentários  
 Esse método lançará um **ArgumentException** se o *distância* não é um número (NAN), ou se *distância* é infinito positivo ou negativo.  Esse método também lançará um **ArgumentException** se *tolerância* é zero (0), e não um número (NaN), infinito negativo, ou positivo ou negativo.  
  
 `STBuffer()`retornará um **FullGlobe** instância em certos casos; por exemplo, `STBuffer()` retorna um **FullGlobe** instância em dois polos quando a distância do buffer é maior que a distância do Equador para os polos.  
  
 Esse método lançará um **ArgumentException** na **FullGlobe** instâncias onde a distância do buffer excede a seguinte limitação:  
  
 0,999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 circunferência da Terra)  
  
 O erro entre o buffer teórico e calculado é max (tolerância, extensões \* 1. e-7) onde a tolerância é o valor da *tolerância* parâmetro. Para obter mais informações sobre extensões, consulte [referência de método do tipo de dados geography](http://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e).  
  
 Esse método não é preciso.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `Point` e usa `BufferWithTolerance()` para obter um buffer grosseiro à sua volta.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [STBuffer &#40; tipo de dados geography &#41;](../../t-sql/spatial-geography/stbuffer-geography-data-type.md)   
 [Métodos estendidos em instâncias de Geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  

