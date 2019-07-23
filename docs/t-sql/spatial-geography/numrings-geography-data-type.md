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
ms.openlocfilehash: e47aebb82c0cc3149dae7de697e92c965903a753
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101787"
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
  
  
