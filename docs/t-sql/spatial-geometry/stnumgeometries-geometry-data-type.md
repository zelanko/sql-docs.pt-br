---
description: STNumGeometries  (tipo de dados geometry)
title: STNumGeometries (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumGeometries (geometry Data Type)
- STNumGeometries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumGeometries (geometry Data Type)
ms.assetid: 9402b03d-3039-42ca-ac59-f96b7f1a48de
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 8ef4aa6a47bdb974803d111a023b473c0c49cf0b
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88444928"
---
# <a name="stnumgeometries-geometry-data-type"></a>STNumGeometries  (tipo de dados geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna o número de geometrias que compõem uma instância de **geometry**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STNumGeometries ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de retorno do CLR: **SqlInt32**  
  
## <a name="remarks"></a>Comentários  
 Esse método retornará 1 se a instância de **geometry** não for uma instância de **MultiPoint**, **MultiLineString**, **MultiPolygon** ou **GeometryCollection** e retornará 0 se a instância de **geometry** estiver vazia.  
  
> [!NOTE]  
>  Se uma **GeometryCollection** tiver aninhado elementos em branco, `STNumGeometries()` não retornará 0. Embora os elementos na instância **GeometryCollection** estejam vazios, a instância em si não é um conjunto vazio.  
  
  

