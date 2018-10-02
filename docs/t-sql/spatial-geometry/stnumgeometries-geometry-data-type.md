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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1c48a3560f960c90e8426a67e5b1b85af933d2ba
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804685"
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
  
 Tipo de retorno do CLR: **SqlInt32**  
  
## <a name="remarks"></a>Remarks  
 Esse método retornará 1 se a instância de **geometry** não for uma instância de **MultiPoint**, **MultiLineString**, **MultiPolygon** ou **GeometryCollection** e retornará 0 se a instância de **geometry** estiver vazia.  
  
> [!NOTE]  
>  Se uma **GeometryCollection** tiver aninhado elementos em branco, `STNumGeometries()` não retornará 0. Embora os elementos na instância **GeometryCollection** estejam vazios, a instância em si não é um conjunto vazio.  
  
  

