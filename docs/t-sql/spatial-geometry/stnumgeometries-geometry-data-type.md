---
title: STNumGeometries (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
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
- STNumGeometries (geometry Data Type)
- STNumGeometries_TSQL
dev_langs: TSQL
helpviewer_keywords: STNumGeometries (geometry Data Type)
ms.assetid: 9402b03d-3039-42ca-ac59-f96b7f1a48de
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f4094aa647ddfa3bf5ffaf191896c9e65677f027
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="stnumgeometries-geometry-data-type"></a>STNumGeometries  (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o número de geometrias que compõem um **geometria** instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STNumGeometries ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **int**  
  
 Tipo de retorno CLR: **SqlInt32**  
  
## <a name="remarks"></a>Remarks  
 Esse método retornará 1 se o **geometria** instância não é um **MultiPoint**, **MultiLineString**, **MultiPolygon**, ou  **GeometryCollection** instância e 0 se o **geometria** instância está vazia.  
  
> [!NOTE]  
>  Se um **GeometryCollection** aninhou elementos em branco, `STNumGeometries()` não retornará 0. Embora os elementos de **GeometryCollection** instância está vazia, a própria instância não é um conjunto vazio.  
  
  

