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
ms.openlocfilehash: aaae21e3a47465011f6644901d0ac886da6846f2
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67930224"
---
# <a name="isnull-geography-data-type"></a>IsNull (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Uma propriedade que especifica se a instância de **geography** é nula. Retornará 'TRUE' se a instância for nula ou 0 se a instância não for nula.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.IsNull  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo do CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentários  
 `IsNull` pode ser usado para testar se uma instância de **geography** é nula. O resultado pode ser um pouco confuso, retornando 0 se a instância não for nula, mas null se a instância for nula.  
  
 Esse método é usado principalmente pela infraestrutura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; é recomendável o uso do predicado T-SQL IS NULL para testar se uma instância de **geography** é nula. Para obter mais informações sobre o predicado T-SQL IS NULL, consulte [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
