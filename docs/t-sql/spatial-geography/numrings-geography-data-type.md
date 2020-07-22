---
title: NumRings (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- NumRings_TSQL
- NumRings
dev_langs:
- TSQL
helpviewer_keywords:
- NumRings method
ms.assetid: 0e4e4fa2-b608-4cc4-98ba-0845ddb4214c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 0b85a8842a7bc33753394c5de96582ca41b9d635
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552483"
---
# <a name="numrings-geography-data-type"></a>NumRings (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna o número total de anéis em uma instância de **polígono**. No tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]geography**do**, os anéis externos e internos não são diferenciados, pois qualquer anel pode ser considerado como externo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.NumRings ()  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-type"></a>Tipo de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de retorno do CLR: **SqlInt32**  
  
## <a name="remarks"></a>Comentários  
 Esse método retornará NULL se essa não for uma instância de **polígono** e retornará 0 se a instância estiver vazia. Esse método é preciso.  
  
## <a name="examples"></a>Exemplos  
 Esse exemplo cria uma instância `Polygon` com dois anéis e confirma que tem dois anéis.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653), (-122.357 47.654, -122.357 47.657, -122.349 47.657, -122.349 47.650, -122.357 47.654))', 4326);  
SELECT @g.NumRings();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
