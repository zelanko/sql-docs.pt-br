---
title: IsNull (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IsNull (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull (geometry Data Type)
ms.assetid: f95813a5-26c0-48aa-bfb8-56d2a0980788
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4b861d170316dbc9d66c7f8e7954910438031f1b
ms.sourcegitcommit: 032273bfbc240fe22ac6c1f6601a14a6d99573f7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2019
ms.locfileid: "55513796"
---
# <a name="isnull-geometry-data-type"></a>IsNull (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

O tipo de uma instância de **geometry** é nulo. Retornará 0 se a instância não for nula.
  
## <a name="syntax"></a>Sintaxe  
  
```  
.IsNull  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 O `IsNull` pode ser usado para testar se uma instância de **geometry** é nula. `IsNull` retorna 0 se a instância não for nula, mas null se a instância for nula.  
  
 Esse método é usado basicamente pela infraestrutura do SQL Server; não é recomendável o uso de `IsNull` para testar se uma instância é nula.  
  

## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

