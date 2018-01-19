---
title: IsNull (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: IsNull (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: IsNull method
ms.assetid: c031074f-bfda-4584-a3bf-4e7c324f237f
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 79b35adec55e9a029335e5f4f402bb86e5afc688
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="isnull-geography-data-type"></a>IsNull (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Uma propriedade que especifica se o **geografia** instância é nula. Retornará 'TRUE' se a instância for nula ou 0 se a instância não for nula.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.IsNull  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo: **bits**  
  
 Tipo CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 `IsNull`pode ser usado para testar se um **geografia** instância é nula. O resultado pode ser um pouco confuso, retornando 0 se a instância não for nula, mas null se a instância for nula.  
  
 Esse método é usado principalmente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] infraestrutura; é recomendável que você use o predicado T-SQL IS NULL para testar se um **geografia** instância é nula. Para obter mais informações sobre o T-SQL de predicado IS NULL, consulte [IS NULL &#40; Transact-SQL &#41; ](../../t-sql/queries/is-null-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
