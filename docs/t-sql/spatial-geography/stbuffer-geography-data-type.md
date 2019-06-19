---
title: STBuffer (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STBuffer (geography Data Type)
- STBuffer_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBuffer (geography Data Type)
ms.assetid: cb4deab8-642b-44d9-b3d9-85114d64021e
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 72e7f25c0bdc3ba77e90e8d9384537948efe4b3f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65937152"
---
# <a name="stbuffer-geography-data-type"></a>STBuffer (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna um objeto de geografia que representa a união de todos os pontos cujas distâncias de uma instância de **geography** é menor ou igual ao valor especificado.  
  
 Esse método de tipo de dados de geography é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STBuffer ( distance )  
```  
  
## <a name="arguments"></a>Argumentos  
 *distance*  
 É um valor do tipo **float** (**duplo** no .NET Framework) que especifica a distância da instância de **geography** a ser considerada para o cálculo do buffer.  
  
 A distância máxima do buffer não pode exceder 0,999 \* *π* * minorAxis \* minorAxis / majorAxis (~0,999 \* 1/2 circunferência da Terra) ou o globo inteiro.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 STBuffer() calcula um buffer da mesma maneira que [BufferWithTolerance](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md), especificando *tolerance* = abs(distance) \* 0,001 e *relative* = **false**.  
  
 Um buffer negativo remove todos os pontos dentro da distância determinada do limite da instância de **geography**.  
  
 `STBuffer()` retornará uma instância de **FullGlobe** em alguns casos. Por exemplo, `STBuffer()` retornará uma instância de **FullGlobe** quando a distância do buffer for maior que a distância do equador até os polos. Um buffer não pode exceder o globo completo.  
  
 Esse método gerará uma **ArgumentException** em instâncias de **FullGlobe** nas quais a distância do buffer exceder a seguinte limitação:  
  
 0,999 \* *π* * minorAxis \* minorAxis / majorAxis (~0,999 \* 1/2 da circunferência da Terra)  
  
 O limite de distância máximo permite que a construção do buffer seja a mais flexível possível.  
  
 O erro entre o buffer teórico e o computado é max(tolerance, extents * 1.E-7), em que tolerance = distância \* 0,001. Para obter mais informações sobre extensões, consulte [Referência de método do tipo de dados geography](https://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `LineString``geography`. Em seguida, usa `STBuffer()` para retornar a região dentro de 1 metro da instância.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STBuffer(1).ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [BufferWithTolerance &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md)   
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
