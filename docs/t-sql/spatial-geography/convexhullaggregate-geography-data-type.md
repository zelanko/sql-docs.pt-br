---
description: ConvexHullAggregate (tipo de dados geography)
title: ConvexHullAggregate (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ConvexHullAggregate_TSQL
- ConvexHullAggregate
dev_langs:
- TSQL
helpviewer_keywords:
- ConvexHullAggregate method (geography)
ms.assetid: 21784c66-2725-471b-9e2d-a8c2e3695197
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a43aad8c89ff1fccdcb8165c77140283a3d10b20
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479390"
---
# <a name="convexhullaggregate-geography-data-type"></a>ConvexHullAggregate (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna uma envoltória convexa para um determinado conjunto de objetos de **geografia**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ConvexHullAggregate ( geography_operand )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *geography_operand*  
 É uma coluna da tabela do tipo **geografia** que representa um conjunto de objetos de **geografia**.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
## <a name="exception"></a>Exceção  
 Gera uma `FormatException` quando há valores de entrada que não são válidos. Consulte [STIsValid &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/stisvalid-geography-data-type.md)  
  
## <a name="remarks"></a>Comentários  
 O método retornará **nulo** quando a entrada estiver vazia ou tiver SRIDs diferentes. Confira [SRIDs &#40;Spatial Reference Identifiers&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 O método ignora entradas **nulas**.  
  
> [!NOTE]  
>  O método retornará **nulo** se todos os valores inseridos forem **nulos**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna uma envoltória convexa do conjunto de objetos de **geografia**.  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT geography::ConvexHullAggregate(SpatialLocation).ToString() AS SpatialLocation  
 FROM Person.Address  
 WHERE City LIKE ('Bothell')
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [Extended Static Geography Methods](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
