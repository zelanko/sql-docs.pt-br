---
title: STConvexHull (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STConvexHull method (geography)
ms.assetid: fb435db7-31bb-4243-9d8b-35379184cfb4
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bb70807d6c335e3aed67df98a9cf49271bfc806b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="stconvexhull-geography-data-type"></a>STConvexHull (tipo de dados de geografia)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna um objeto que representa a envoltória convexa de uma instância de **geography**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STConvexHull ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Retorna um objeto `FullGlobe` da instância de **geography** que tem um ângulo de envelope maior que 90 graus.  
  
 Retorna uma coleção de **geography** vazia para uma instância de **geography** vazia.  
  
 Retorna **nulo** para uma instância de **geography** não inicializada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-stconvexhull-on-an-uninitialized-geography-instance"></a>A. Usando STConvexHull() em uma instância de geografia não inicializada  
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
  
  
