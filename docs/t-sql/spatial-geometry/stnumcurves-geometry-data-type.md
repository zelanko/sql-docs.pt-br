---
description: STNumCurves (tipo de dados geometry)
title: STNumCurves (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geometry)
ms.assetid: 20c2fa0b-656b-4519-b34c-cc8f094290d4
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: fe3418284131577051e48f8300bd89df2abc0ec1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444943"
---
# <a name="stnumcurves-geometry-data-type"></a>STNumCurves (tipo de dados geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Esse método retorna o número de curvas em uma instância de **geometry** quando a instância é um tipo de dados espacial unidimensional. Os tipos de dados espaciais unidimensionais incluem **LineString**, **CircularString** e **CompoundCurve**. `STNumCurves`() funciona somente em tipos simples. Ele não funciona com coleções de **geometrias** como **MultiLineString**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STNumCurves()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentários  
 Uma instância de **geometry** unidimensional vazia retorna 0. **NULL** é retornado quando a instância de **geometry** não é uma instância unidimensional ou é uma instância não inicializada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>a. Usando STNumCurves() em uma instância de CircularString  
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
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral de tipos de dados espaciais](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

