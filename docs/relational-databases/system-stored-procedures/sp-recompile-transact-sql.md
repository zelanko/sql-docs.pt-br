---
title: sp_recompile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_recompile_TSQL
- sp_recompile
dev_langs:
- TSQL
helpviewer_keywords:
- sp_recompile
ms.assetid: 6192ca87-febd-4075-8199-14b4fa609b8c
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0f9b72c1a97c17f975144ad0fd364260afab1fb8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68002559"
---
# <a name="sp_recompile-transact-sql"></a>sp_recompile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Faz com que procedimentos armazenados, gatilhos e funções definidas pelo usuário sejam recompilados na próxima execução. Isso é feito com a remoção do plano existente do cache de procedimento que força um novo plano a ser criado na próxima vez que o procedimento ou gatilho é executado. Em uma coleção [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], o evento SP:CacheInsert é registrado em log em vez do evento SP:Recompile.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
  
sp_recompile [ @objname = ] 'object'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @objname= ] '*objeto*'  
 O nome qualificado ou não qualificado de um procedimento armazenado, gatilho, tabela, exibição ou função definida pelo usuário no banco de dados atual. *Object* é **nvarchar (776)**, sem padrão. Se *Object* for o nome de um procedimento armazenado, um gatilho ou uma função definida pelo usuário, o procedimento armazenado, o gatilho ou a função serão recompilados na próxima vez em que for executado. Se *Object* for o nome de uma tabela ou exibição, todos os procedimentos armazenados, gatilhos ou funções definidas pelo usuário que fazem referência à tabela ou exibição serão recompilados na próxima vez em que forem executados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número diferente de zero (falha)  
  
## <a name="remarks"></a>Comentários  
 sp_recompile procura um objeto somente no banco de dados atual.  
  
 As consultas usadas por procedimentos armazenados, gatilhos e funções definidas pelo usuário são otimizadas apenas quando são compiladas. Como índices ou outras alterações que afetam as estatísticas são feitos no banco de dados, os procedimentos armazenados compilados, gatilhos e funções definidas pelo usuário podem perder a eficiência. Recompilando procedimentos armazenados e gatilhos que agem em uma tabela, você pode reotimizar as consultas.  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recompila automaticamente procedimentos armazenados, gatilhos e funções definidas pelo usuário quando for vantajoso fazer isso.  
  
## <a name="permissions"></a>Permissões  
 Exige permissão ALTER no objeto especificado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir faz com que procedimentos armazenados, gatilhos e funções definidas pelo usuário que agem na tabela `Customer` sejam recompilados da próxima vez que forem executados.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_recompile N'Sales.Customer';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CRIAR procedimento &#40;&#41;Transact-SQL](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
