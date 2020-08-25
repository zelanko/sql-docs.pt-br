---
description: DROP EXTERNAL RESOURCE POOL (Transact-SQL)
title: DROP EXTERNAL RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: machine-learning-services
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL RESOURCE POOL
- DROP_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL RESOURCE POOL statement
ms.assetid: e2fa01bd-96ff-4ea9-bb08-6cb6b6adf68c
author: dphansen
ms.author: davidph
manager: cgronlund
ms.openlocfilehash: 7a32d1693f48ea56f3edd8c8c7373c88d6369bb0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88358512"
---
# <a name="drop-external-resource-pool-transact-sql"></a>DROP EXTERNAL RESOURCE POOL (Transact-SQL)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Exclui um pool de recursos externos do Resource Governor usado para definir recursos para processos externos. 

::: moniker range="=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Para o [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] no [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], o pool externo controla `rterm.exe`, `BxlServer.exe` e outros processos gerados por eles.
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Para [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)], o pool externo controla `rterm.exe`, `python.exe`, `BxlServer.exe` e outros processos gerados por eles.
::: moniker-end

Pools de recursos externos são criados com [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md) e modificados com [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md).  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```
DROP EXTERNAL RESOURCE POOL pool_name  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos

*pool_name*  
O nome do pool de recursos externos a ser excluído.  
  
## <a name="remarks"></a>Comentários

Não é possível remover um pool de recursos externos se ele contém grupos de carga de trabalho.  

Você não pode descartar os pools internos ou padrão do Administrador de recursos.  

Ao executar instruções DDL, é recomendável estar familiarizado com os estados do Administrador de Recursos. Para obter mais informações, consulte [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).  

## <a name="permissions"></a>Permissões

Requer a permissão `CONTROL SERVER`.  

## <a name="examples"></a>Exemplos

O exemplo a seguir remove o pool de recursos externos chamado `ex_pool`.  

```sql
DROP EXTERNAL RESOURCE POOL ex_pool;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  

> [!NOTE]
> Os Serviços de Machine Learning do SQL 2019 para Linux não dão suporte à capacidade de definir a afinidade de CPU.

## <a name="see-also"></a>Consulte Também

+ [Opção de Configuração do servidor external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)
+ [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)
+ [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
+ [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)
+ [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)
