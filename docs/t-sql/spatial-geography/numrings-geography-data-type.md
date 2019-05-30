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
manager: craigg
ms.openlocfilehash: ad07cdaffd8e7cd207691e218ad8eaabf293b0db
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65937548"
---
# <a name="numrings-geography-data-type"></a>NumRings (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o número total de anéis em uma instância de **polígono**. No tipo de **geografia** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os anéis externos e internos não são diferenciados, pois qualquer anel pode ser considerado como externo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.NumRings ()  
```  
  
## <a name="return-type"></a>Tipo de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de retorno CLR: **SqlInt32**  
  
## <a name="remarks"></a>Remarks  
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
  
  
