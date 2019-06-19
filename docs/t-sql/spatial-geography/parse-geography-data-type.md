---
title: Parse (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Parse method
- Parse (geography Data Type)
ms.assetid: 21c402fa-fd0f-4d09-a097-49cee0316d4e
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 023af0279bdb848e299ec1dbe31ff82305ad109a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65935911"
---
# <a name="parse-geography-data-type"></a>Parse (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna uma instância de **geography** de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium). Parse() é equivalente a [STGeomFromText](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md), exceto que ele assume uma SRID (ID de referência espacial) igual a 4326 como um parâmetro. A entrada pode transportar valores opcionais Z (elevação) e M (medida).
  
Esse método de tipo de dados de **geography** é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Parse ( 'geography_tagged_text' )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geography_tagged_text*  
 É a representação WKT da instância de **geography** a ser retornada. *geography_tagged_text* é uma expressão **nvarchar**.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 O tipo do OGC da instância de **geography** retornado por `Parse()` é definido como a entrada de WKT correspondente.  
  
 A cadeia de caracteres 'Null' será interpretada como uma instância de **geography** nula.  
  
 Este método gerará **ArgumentException** se a entrada contiver uma borda oposta.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `Parse()` para criar uma instância `geography`.  
  
```  
DECLARE @g geography;   
SET @g = geography::Parse('LINESTRING(-122.360 47.656, -122.343 47.656)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos de geografia estática estendidos](../../t-sql/spatial-geography/extended-static-geography-methods.md)   
 [STGeomFromText &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)  
  
  
