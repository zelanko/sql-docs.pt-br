---
title: sp_databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_databases_TSQL
- sp_databases
dev_langs:
- TSQL
helpviewer_keywords:
- sp_databases
ms.assetid: 2a83b92a-9ecc-43c4-8ff4-e91e3a940b5a
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5356e3e2ceb67202d7ed9e64973eccd1c13e9f64
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="spdatabases-transact-sql"></a>sp_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista bancos de dados que residem em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou que podem ser acessados por um gateway de banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_databases  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhuma  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**DATABASE_NAME**|**sysname**|Nome do banco de dados. No [!INCLUDE[ssDE](../../includes/ssde-md.md)], esta coluna representa o nome do banco de dados, conforme armazenado no **sys. Databases** exibição do catálogo.|  
|**DATABASE_SIZE**|**Int**|Tamanho de banco de dados, em kilobytes.|  
|**COMENTÁRIOS**|**varchar(254)**|Para o [!INCLUDE[ssDE](../../includes/ssde-md.md)], esse campo sempre retorna NULL.|  
  
## <a name="remarks"></a>Remarks  
 Nomes de banco de dados retornados podem ser usados como parâmetros na instrução USE, para alterar o contexto de banco de dados atual.  
  
 **sp_databases** não tem nenhum equivalente em conectividade aberta de banco de dados (ODBC).  
  
## <a name="permissions"></a>Permissões  
 Requer uma das permissões: CREATE DATABASE, ALTER ANY DATABASE ou VIEW ANY DEFINITION, e ainda, permissão de acesso ao banco de dados. Não pode lhe ser negada permissão VIEW ANY DEFINITION.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir exibe a execução do `sp_databases`.  
  
```sql  
USE master;  
GO  
EXEC sp_databases;  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [HAS_DBACCESS &#40;Transact-SQL&#41;](../../t-sql/functions/has-dbaccess-transact-sql.md)  
  
  
