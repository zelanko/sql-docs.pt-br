---
description: STConvexHull (tipo de dados de geografia)
title: STConvexHull (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STConvexHull method (geography)
ms.assetid: fb435db7-31bb-4243-9d8b-35379184cfb4
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 0db7ad59585b2ff0c57526ca40f7caa3576e99fc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479322"
---
# <a name="stconvexhull-geography-data-type"></a>STConvexHull (tipo de dados de geografia)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna um objeto que representa a envoltória convexa de uma instância de **geography**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STConvexHull ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentários  
 Retorna um objeto `FullGlobe` da instância de **geography** que tem um ângulo de envelope maior que 90 graus.  
  
 Retorna uma coleção de **geography** vazia para uma instância de **geography** vazia.  
  
 Retorna **nulo** para uma instância de **geography** não inicializada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-stconvexhull-on-an-uninitialized-geography-instance"></a>a. Usando STConvexHull() em uma instância de geografia não inicializada  
 O exemplo a seguir usa `STConvexHull()` em uma instância de **geography** não inicializada.  
  
```
 DECLARE @g geography;  
 SELECT @g.STConvexHull();
 ```  
  
### <a name="b-using-stconvexhull-on-an-empty-geography-instance"></a>B. Usando STConvexHull em uma instância de geografia vazia  
 O exemplo a seguir usa `STConvexHull()` em uma instância de `Polygon` vazia.  
  
```
 DECLARE @g geography = 'POLYGON EMPTY';  
 SELECT @g.STConvexHull().ToString();
 ```  
  
### <a name="c-finding-the-convex-hull-of-a-non-convex-polygon-instance"></a>C. Localizando a superfície convexa de uma instância de Polígono não convexa  
 O exemplo a seguir usa `STConvexHull()` para localizar a superfície convexa de uma instância `Polygon` não convexa.  
  
```  
 DECLARE @g geography;  
 SET @g = geography::Parse('POLYGON((-120.533 46.566, -118.283 46.1, -122.3 47.45, -120.533 46.566))');  
 SELECT @g.STConvexHull().ToString();  
```  
  
### <a name="d-finding-the-convex-hull-on-a-geography-instance-with-an-envelope-angle-larger-than-90-degrees"></a>D. Localizando a superfície convexa de uma instância de geografia em um ângulo de envelope maior que 90 graus  
 O exemplo a seguir usa `STConvexHull()` em uma instância de **geography** com um ângulo de envelope maior que 90 graus.  
  
```
 DECLARE @g geography = 'POLYGON((20.533 46.566, -18.283 46.1, -22.3 47.45, 20.533 46.566))';  
 SELECT @g.STConvexHull().ToString();
 ```  
  
  
