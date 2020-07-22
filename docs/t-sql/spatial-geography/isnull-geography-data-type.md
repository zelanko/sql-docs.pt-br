---
title: IsNull (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IsNull (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull method
ms.assetid: c031074f-bfda-4584-a3bf-4e7c324f237f
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 98a68bfbdc39bd0731e047e5d6876410d4daf263
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552908"
---
# <a name="isnull-geography-data-type"></a>IsNull (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Uma propriedade que especifica se a instância de **geography** é nula. Retornará 'TRUE' se a instância for nula ou 0 se a instância não for nula.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.IsNull  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo do CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentários  
 `IsNull` pode ser usado para testar se uma instância de **geography** é nula. O resultado pode ser um pouco confuso, retornando 0 se a instância não for nula, mas null se a instância for nula.  
  
 Esse método é usado principalmente pela infraestrutura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; é recomendável o uso do predicado T-SQL IS NULL para testar se uma instância de **geography** é nula. Para obter mais informações sobre o predicado T-SQL IS NULL, consulte [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
