---
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
ms.openlocfilehash: 5a0c123b367fa2a85a1a3732200452a474b032c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088921"
---
# <a name="stnumgeometries-geometry-data-type"></a>STNumGeometries  (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o número de geometrias que compõem uma instância de **geometry**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STNumGeometries ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de retorno CLR: **SqlInt32**  
  
## <a name="remarks"></a>Remarks  
 Esse método retornará 1 se a instância de **geometry** não for uma instância de **MultiPoint**, **MultiLineString**, **MultiPolygon** ou **GeometryCollection** e retornará 0 se a instância de **geometry** estiver vazia.  
  
> [!NOTE]  
>  Se uma **GeometryCollection** tiver aninhado elementos em branco, `STNumGeometries()` não retornará 0. Embora os elementos na instância **GeometryCollection** estejam vazios, a instância em si não é um conjunto vazio.  
  
  

