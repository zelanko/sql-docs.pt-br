---
title: MakeValid (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- MakeValid method (geography)
ms.assetid: f67038e3-4f62-4465-994e-e95ac27d8ada
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: b4d60632de0ccc60d2c07f501334a64d31692fed
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65937638"
---
# <a name="makevalid-geography-data-type"></a>MakeValid (tipos de dados de geografia)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Converte uma instância de**geografia** que não é válida em uma instância de **geography** válida com um tipo do OGC (Open Geospatial Consortium) válido.  
  
 Se um objeto de entrada retornar False para STIsValid(), `MakeValid()` converterá a instância que não é válida em uma instância válida.  
  
 Esse método de tipo de dados de geography é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.MakeValid ()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Esse método pode alterar o tipo de instância de **geography**. Além disso, os pontos de uma instância de **geography** podem mudar um pouco. Os resultados de alguns métodos como NumPoint() podem ser alterados.  
  
 Nos casos em que a instância espacial inválida interseccionar o equador e tiver um EnvelopeAngle() = 180, uma instância de **FullGlobe** será retornada. O método do tipo de dados de `MakeValid()`**geography** fará a melhor tentativa possível de retornar instâncias válidas, mas não há garantias de que os resultados serão precisos.  
  
> [!NOTE]  
>  Os objetos que não são válidos podem ser armazenados no banco de dados. Os métodos que podem ser executados em instâncias inválidas (instâncias para as quais STIsValid() retorna False) são métodos que verificam a validade ou permitem a exportação: STIsValid(), MakeValid(), STAsText(), STAsBinary(), ToString(), AsTextZM() e AsGml().  
  
 Esse método não é preciso.  
  
## <a name="examples"></a>Exemplos  
 O primeiro exemplo cria uma instância inválida de `LineString` que se sobrepõe e usa `STIsValid()` para confirmar que é uma instância inválida. `STIsValid()` retorna o valor 0 para uma instância inválida.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(0 2, 1 1, 1 0, 1 1, 2 2)', 4326);  
SELECT @g.STIsValid();  
```  
  
 O segundo exemplo usa `MakeValid()` pata tornar a instância válida e testar se ela é realmente válida. `STIsValid()` retorna o valor 1 para uma instância válida.  
  
```  
SET @g = @g.MakeValid();  
SELECT @g.STIsValid();  
```  
  
 O terceiro exemplo verifica como a instância foi alterada para se tornar uma instância válida.  
  
```  
SELECT @g.ToString();  
```  
  
 Neste exemplo, quando a instância de `LineString` é selecionada, os valores são retornados como uma instância de `MultiLineString` válida.  
  
```  
MULTILINESTRING ((0 2, 1 1, 2 2), (1 1, 1 0))  
```  
  
## <a name="see-also"></a>Consulte Também  
 [STIsValid &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
