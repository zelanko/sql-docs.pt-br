---
title: NumRings (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NumRings_TSQL
- NumRings
dev_langs: TSQL
helpviewer_keywords: NumRings method
ms.assetid: 0e4e4fa2-b608-4cc4-98ba-0845ddb4214c
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4816f581690b5d68d970310a406de3f48ddb4fff
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="numrings-geography-data-type"></a>NumRings (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o número total de anéis em uma **polígono** instância. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **geografia** digite, externo e internos anéis não são diferenciados, pois qualquer anel pode ser usado como anel externo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.NumRings ()  
```  
  
## <a name="return-type"></a>Tipo de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **int**  
  
 Tipo de retorno CLR: **SqlInt32**  
  
## <a name="remarks"></a>Comentários  
 Esse método retornará NULL se não for um **polígono** instância e retornará 0 se a instância está vazia. Esse método é preciso.  
  
## <a name="examples"></a>Exemplos  
 Esse exemplo cria uma instância `Polygon` com dois anéis e confirma que tem dois anéis.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653), (-122.357 47.654, -122.357 47.657, -122.349 47.657, -122.349 47.650, -122.357 47.654))', 4326);  
SELECT @g.NumRings();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
