---
title: STNumCurves (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumCurves
- STNumCurves_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geography)
ms.assetid: e98a56c2-8496-4dfd-9b37-7f3c4ca9b2b5
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 07626f3ded35ee9c4075e08765b76974d1c1b209
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86556042"
---
# <a name="stnumcurves-geography-data-type"></a>STNumCurves (tipo de dados geography)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  Retorna o número de curvas em uma instância de **geography** unidimensional.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STNumCurves()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentários  
 Os tipos de dados espaciais unidimensionais incluem **LineString**, **CircularString** e **CompoundCurve**. Uma instância de **geography** unidimensional vazia retorna 0.  
  
 `STNumCurves`() funciona apenas em tipos simples e não funciona com coleções de **geografia** como **MultiLineString**. **NULL** é retornado quando a instância de **geography** não é um tipo de dados unidimensional.  
  
 **Nulo** é retornado para instâncias de **geography** não inicializadas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>a. Usando STNumCurves() em uma instância de CircularString  
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
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral de tipos de dados espaciais](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
