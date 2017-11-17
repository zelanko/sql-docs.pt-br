---
title: STNumCurves (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STNumCurves
- STNumCurves_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geography)
ms.assetid: e98a56c2-8496-4dfd-9b37-7f3c4ca9b2b5
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c92c6dec90faf08d69ed49de506ba8c4371141ba
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stnumcurves-geography-data-type"></a>STNumCurves (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna o número de curvas em uma unidimensional **geografia** instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STNumCurves()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentários  
 Os tipos de dados espaciais unidimensionais incluem **LineString**, **CircularString**, e **CompoundCurve**. Vazio unidimensional **geografia** instância retorna 0.  
  
 `STNumCurves`() funciona somente em tipos simples; ele não funciona com **geografia** coleções como **MultiLineString**. **NULO** é retornado quando o **geografia** instância não é um tipo de dados unidimensional.  
  
 **Nulo** é retornado para não inicializado **geografia** instâncias.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>A. Usando STNumCurves() em uma instância de CircularString  
 O exemplo a seguir mostra como obter o número de curvas em uma instância `CircularString`:  
  
```
 DECLARE @g geography; 
 SET @g = geography::Parse('CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 SELECT @g.STNumCurves();
 ```  
  
### <a name="b-using-stnumcurves-on-a-compoundcurve-instance"></a>B. Usando STNumCurves() em uma instância de CompoundCurve  
 O exemplo a seguir usa `STNumCurves()` para retornar o número de curvas em uma instância `CompoundCurve`.  
  
```
 DECLARE @g geography;  
 SET @g = geography::Parse('COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))');  
 SELECT @g.STNumCurves();
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de tipos de dados espaciais](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [Métodos do OGC em instâncias de Geografia](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

