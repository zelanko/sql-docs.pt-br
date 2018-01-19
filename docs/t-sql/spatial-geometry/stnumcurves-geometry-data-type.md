---
title: STNumCurves (tipo de dados geometry) | Microsoft Docs
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
dev_langs: TSQL
helpviewer_keywords: STNumCurves method (geometry)
ms.assetid: 20c2fa0b-656b-4519-b34c-cc8f094290d4
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3cdd2b7f3cf7b5edac7da88320fbffd80abb149c
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="stnumcurves-geometry-data-type"></a>STNumCurves (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Esse método retorna o número de curvas em uma **geometria** instância quando a instância é um tipo de dados espacial unidimensional. Os tipos de dados espaciais unidimensionais incluem **LineString**, **CircularString**, e **CompoundCurve**. `STNumCurves`() funciona somente em tipos simples; ele não funciona com **geometria** coleções como **MultiLineString**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STNumCurves()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 Vazio unidimensional **geometria** instância retorna 0. **NULO** é retornado quando o **geometria** instância não é uma instância unidimensional ou é uma instância não inicializada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>A. Usando STNumCurves() em uma instância de CircularString  
 O exemplo a seguir mostra como obter o número de curvas em uma instância `CircularString`:  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)');  
 SELECT @g.STNumCurves();
 ```  
  
### <a name="b-using-stnumcurves-on-a-compoundcurve-instance"></a>B. Usando STNumCurves() em uma instância de CompoundCurve  
 O exemplo a seguir usa `STNumCurves()` para retornar o número de curvas em uma instância `CompoundCurve`.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))');  
 SELECT @g.STNumCurves();
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de tipos de dados espaciais](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

