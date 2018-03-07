---
title: Parse (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
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
dev_langs:
- TSQL
helpviewer_keywords:
- Parse method
- Parse (geography Data Type)
ms.assetid: 21c402fa-fd0f-4d09-a097-49cee0316d4e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c29c43af7034f86fa993fc5f12046200216ec57f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="parse-geography-data-type"></a>Parse (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um **geografia** instância de uma representação de texto do Open Geospatial Consortium (OGC) conhecido (WKT). Parse é equivalente a [STGeomFromText](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md), exceto que ele assume um SRID (ID) de 4326 como um parâmetro de referência espacial. A entrada pode transportar valores opcionais Z (elevação) e M (medida).
  
Isso **geografia** método dá suporte ao tipo de dados **FullGlobe** instâncias ou a instâncias espaciais maiores que um hemisfério.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Parse ( 'geography_tagged_text' )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geography_tagged_text*  
 É a representação WKT do **geografia** instância a ser retornada. *geography_tagged_text* é um **nvarchar** expressão.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 O tipo OGC do **geografia** instância retornada por `Parse()` é definido como a entrada WKT correspondente.  
  
 A cadeia de caracteres 'Nulo' será interpretado como um valor nulo **geografia** instância.  
  
 Este método gerará **ArgumentException** se a entrada contém uma borda oposta.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `Parse()` para criar uma instância `geography`.  
  
```  
DECLARE @g geography;   
SET @g = geography::Parse('LINESTRING(-122.360 47.656, -122.343 47.656)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos de Geografia estática estendidos](../../t-sql/spatial-geography/extended-static-geography-methods.md)   
 [STGeomFromText &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)  
  
  
