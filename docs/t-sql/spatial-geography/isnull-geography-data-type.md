---
title: IsNull (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IsNull (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull method
ms.assetid: c031074f-bfda-4584-a3bf-4e7c324f237f
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f2bfa2b771d02649f40e2e7b93a61777bfd38da8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
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
  
## <a name="remarks"></a>Remarks  
 `IsNull` pode ser usado para testar se uma instância de **geography** é nula. O resultado pode ser um pouco confuso, retornando 0 se a instância não for nula, mas null se a instância for nula.  
  
 Esse método é usado principalmente pela infraestrutura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; é recomendável o uso do predicado T-SQL IS NULL para testar se uma instância de **geography** é nula. Para obter mais informações sobre o predicado T-SQL IS NULL, consulte [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
