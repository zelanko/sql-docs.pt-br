---
title: sys. sp_rda_reauthorize_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_rda_reauthorize_db
- sp_rda_reauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reauthorize_db stored procedure
ms.assetid: f6f3e4b2-8c72-4d23-a5de-fe671ca5c5cd
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a62cae8b4c47975d7d0941458fefbafea7c6288a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="syssprdareauthorizedb-transact-sql"></a>sys.sp_rda_reauthorize_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Restaura a conexão autenticada entre um banco de dados local habilitado para Stretch e o banco de dados remoto.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_rda_reauthorize_db @credential = @credential, @with_copy = @with_copy [ , @azure_servername = @azure_servername, @azure_databasename = @azure_databasename ]  
```  
  
## <a name="arguments"></a>Argumentos  
 @credential = *@credential*  
 É a credencial no escopo do banco de dados associada com o banco de dados local habilitado para Stretch.  
  
 @with_copy = *@with_copy*  
 Especifica se deve fazer uma cópia dos dados remotos e conectar-se à cópia (recomendada). *@with_copy* é bit.  
  
 @azure_servername = *@azure_servername*  
 Especifica o nome do servidor do Azure que contém os dados remotos. *@azure_servername* é sysname.  
  
 @azure_databasename = *@azure_databasename*  
 Especifica o nome do banco de dados do Azure que contém os dados remotos. *@azure_databasename* é sysname.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou >0 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer permissões db_owner.  
  
## <a name="remarks"></a>Remarks  
 Quando você executa [sys. sp_rda_reauthorize_db (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) para se reconectar ao banco de dados remoto do Azure, essa operação redefine automaticamente o modo de consulta para LOCAL_AND_REMOTE, que é o comportamento padrão para o Stretch Database. Ou seja, consultas retornam resultados de dados locais e remotos.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir restaura a conexão autenticada entre um banco de dados local habilitado para Stretch e o banco de dados remoto. Ele faz uma cópia dos dados remotos (recomendados) e conecta-se a nova cópia.  
  
```sql  
DECLARE @credentialName nvarchar(128);   
SET @credentialName = N'<existing_database_scoped_credential_name>';   
EXEC sp_rda_reauthorize_db @credential = @credentialName, @with_copy = 1;  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.sp_rda_deauthorize_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
