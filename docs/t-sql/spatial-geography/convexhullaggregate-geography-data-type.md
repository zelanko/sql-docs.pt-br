---
title: ConvexHullAggregate (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
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
- ConvexHullAggregate_TSQL
- ConvexHullAggregate
dev_langs: TSQL
helpviewer_keywords: ConvexHullAggregate method (geography)
ms.assetid: 21784c66-2725-471b-9e2d-a8c2e3695197
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bc709bdd7837c60513304695a8ed6a871b21549d
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="convexhullaggregate-geography-data-type"></a>ConvexHullAggregate (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um envoltório convexo para um determinado conjunto de **geografia** objetos.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ConvexHullAggregate ( geography_operand )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geography_operand*  
 É um **geografia** coluna da tabela de tipo que representa um conjunto de **geografia** objetos.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
## <a name="exception"></a>Exceção  
 Gera uma `FormatException` quando há valores de entrada que não são válidos. Consulte [STIsValid &#40; tipo de dados geography &#41;](../../t-sql/spatial-geography/stisvalid-geography-data-type.md)  
  
## <a name="remarks"></a>Remarks  
 Método retornará **nulo** quando a entrada estiver vazia ou tiver SRIDs diferentes. Consulte [Spatial Reference Identifiers &#40; SRIDs &#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 Método ignora **nulo** entradas.  
  
> [!NOTE]  
>  Método retornará **nulo** se todos os valores inseridos forem **nulo**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna uma forma convexa do conjunto de **geografia** objetos.  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT geography::ConvexHullAggregate(SpatialLocation).ToString() AS SpatialLocation  
 FROM Person.Address  
 WHERE City LIKE ('Bothell')
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Extended Static Geography Methods](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
