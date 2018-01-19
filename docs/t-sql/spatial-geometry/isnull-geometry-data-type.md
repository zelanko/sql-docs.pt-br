---
title: IsNull (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: IsNull (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: IsNull (geometry Data Type)
ms.assetid: f95813a5-26c0-48aa-bfb8-56d2a0980788
caps.latest.revision: "13"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ce93833e05e083f2ed7efad0267700480a5c155a
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="isnull-geometry-data-type"></a>IsNull (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

O tipo de um **geometria** instância é nula. Retornará 0 se a instância não for nula.
  
## <a name="syntax"></a>Sintaxe  
  
```  
.IsNull  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo: **bits**  
  
 Tipo CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 `IsNull`pode ser usado para testar se um **geometria** instância é nula. O resultado pode ser um pouco confuso, retornando 0 se a instância não for nula, mas null se a instância for nula.  
  
 Esse método é usado basicamente pela infraestrutura do SQL Server; é recomendável o uso de `IsNull` para testar se uma instância é nula.  
  

## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

