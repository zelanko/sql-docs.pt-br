---
title: STPointFromText (tipo de dados geography) | Microsoft Docs
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
- STPointFromText (geography Data Type)
- STPointFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STPointFromText method
ms.assetid: e5fe54dc-0007-4631-8dde-7ae4d4c41f6e
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1b887aa5f33d40b047a81837ea91bfff8ecca7d1
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stpointfromtext-geography-data-type"></a>STPointFromText (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um **geografia** instância de uma representação de texto do Open Geospatial Consortium (OGC) conhecido (WKT), aumentada com qualquer valor Z (elevação) e m (medida) transportados pela instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
STPointFromText ( 'point_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *point_tagged_text*  
 É a representação WKT do **geographyPoint** instância que você deseja retornar. *point_tagged_text* é um **nvarchar (max)** expressão.  
  
 *SRID*  
 É um **int** SRID (ID) de fazer referência a expressão que representa o espaciais a **geographyPoint** instância que você deseja retornar.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
 Tipo OGC: **ponto**  
  
## <a name="remarks"></a>Comentários  
 Este método lança um **FormatException** se a entrada não for bem formatada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STPointFromText()` para criar uma instância `geography`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STPointFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos de Geografia estática do OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  

