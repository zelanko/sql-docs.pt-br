---
title: UnionAggregate (tipo de dados geography) | Microsoft Docs
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
- UnionAggregate
- UnionAggregate_TSQL
dev_langs: TSQL
helpviewer_keywords: UnionAggregate method (geography)
ms.assetid: 1a3aeef1-5b0e-4ae8-aeb7-c4aab22f42ab
caps.latest.revision: "13"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 24e2504d9b3ab79ac6abec7ea3a21452928e255f
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="unionaggregate-geography-data-type"></a>UnionAggregate (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Executa uma operação de união em um conjunto de objetos de geografia.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
UnionAggregate ( geography_operand )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geography_operand*  
 É um **geografia** coluna de tipo de tabela que contém o conjunto de **geografia** objetos no qual executar uma operação de união.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
## <a name="remarks"></a>Remarks  
 Método retornará **nulo** se a entrada tiver SRIDs diferentes. Consulte [Spatial Reference Identifiers &#40; SRIDs &#41; ](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
 Método ignora **nulo** entradas.  
  
> [!NOTE]  
>  Método retornará **nulo** se todos os valores inseridos forem **nulo**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir executa um `UnionAggregate` em um conjunto de **geografia** pontos local dentro de uma cidade.  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT City,  
 geography::UnionAggregate(SpatialLocation) AS SpatialLocation  
 FROM Person.Address  
 WHERE PostalCode LIKE('981%')  
 GROUP BY City;
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Extended Static Geography Methods](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
