---
title: MakeValid (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: MakeValid method (geography)
ms.assetid: f67038e3-4f62-4465-994e-e95ac27d8ada
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 796b06fb230cffbfe813d204017dc58c24d8c5b2
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="makevalid-geography-data-type"></a>MakeValid (tipos de dados de geografia)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Converte um **geografia** instância que não é válida em uma opção válida **geografia** instância com um tipo válido do Open Geospatial Consortium (OGC).  
  
 Se um objeto de entrada retornar False para stisvalid (), `MakeValid()` converterá a instância que não é válida para uma instância válida.  
  
 Esses dados de Geografia digite método dá suporte a **FullGlobe** instâncias ou a instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.MakeValid ()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Esse método pode alterar o tipo do **geografia** instância. Além disso, os pontos de um **geografia** instância pode mudar ligeiramente. Resultados de alguns métodos como NumPoint() podem ser alteradas.  
  
 Em casos onde a instância espacial inválida cruza o equador e tem um EnvelopeAngle() = 180, uma **FullGlobe** instância será retornada. O `MakeValid()` **geografia** método de tipo de dados fará com que a melhor tentativa no retorno de instâncias válidas, mas não há garantia que os resultados precisos.  
  
> [!NOTE]  
>  Os objetos que não são válidos podem ser armazenados no banco de dados. Os métodos que podem ser executados em instâncias inválidas (instâncias para as quais stisvalid () retornam False) são métodos que verificam a validade ou permitem exportação: stisvalid (), makevalid (), stastext (), STAsBinary(), ToString (), AsTextZM() e AsGml().  
  
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
  
## <a name="see-also"></a>Consulte também  
 [STIsValid &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
