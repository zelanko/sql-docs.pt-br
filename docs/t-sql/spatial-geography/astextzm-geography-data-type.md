---
title: AsTextZM (tipo de dados geography) | Microsoft Docs
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
f1_keywords:
- AsTextZM (geography Data Type)
- AsTextZM_TSQL
- AsTextZM
- AsTextZM_(geography_Data_Type)_TSQL
dev_langs: TSQL
helpviewer_keywords: AsTextZM method
ms.assetid: e9dc27f6-e945-4457-8498-7644db34008e
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c3672470989920d677958a9e4063f3585288c20a
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="astextzm-geography-data-type"></a>AsTextZM (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna a representação de texto do Open Geospatial Consortium (OGC) conhecido (WKT) de um **geografia** instância aumentada com qualquer **Z** (elevação) e **M** (medida) valores transportados pela instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.AsTextZM ()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **nvarchar (max)**  
  
 Tipo de retorno CLR: **SqlChars**  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um `Point` instância que contém **Z** (elevação) e **M** valores (medida). `STAsText()`Seleciona valores WKT (-122.34900 47.65100); `AsTextZM()` seleciona os mesmos valores WKT e também retorna os valores para **Z** e **M**, produzindo (-122.34900 47.65100 10.3 12).  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.STAsText();  
SELECT @g.AsTextZM();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de Geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40; tipo de dados geography &#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [Z &#40; tipo de dados geography &#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
