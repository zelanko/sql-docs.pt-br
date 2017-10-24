---
title: STGeomFromText (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STGeomFromText (geography Data Type)
- STGeomFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full globe
- STGeomFromText method
ms.assetid: 3717987b-77d8-4ccf-a1db-5a8016ac1083
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bdd52d6a9dc928d47db871ec9a84648797e64fe8
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stgeomfromtext-geography-data-type"></a>STGeomFromText (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um **geografia** instância de uma representação de texto do Open Geospatial Consortium (OGC) conhecido (WKT) aumentada com qualquer valor Z (elevação) e m (medida) transportados pela instância.
  
Isso **geografia** método dá suporte ao tipo de dados **FullGlobe** instâncias ou a instâncias espaciais maiores que um hemisfério.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
STGeomFromText ( 'geography_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geography_tagged_text*  
 É a representação WKT do **geografia** instância a ser retornada. *geography_tagged_text* é um **nvarchar (max)** expressão.  
  
 *SRID*  
 É um **int** SRID (ID) de fazer referência a expressão que representa o espaciais a **geografia** instância a ser retornada.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentários  
 O tipo OGC do **geografia** instância retornada por stgeomfromtext () é definida como a entrada WKT correspondente.  
  
 Esse método lançará um **ArgumentException** se a entrada contém uma borda oposta.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STGeomFromText()` para criar uma instância `geography`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos de Geografia estática do OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  

