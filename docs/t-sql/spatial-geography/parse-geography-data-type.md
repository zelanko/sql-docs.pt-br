---
title: Parse (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 953db8cfb7240b14ee2775ed01ee18d78cd7073f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="parse-geography-data-type"></a>Parse (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>Comentários  
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
  
  

