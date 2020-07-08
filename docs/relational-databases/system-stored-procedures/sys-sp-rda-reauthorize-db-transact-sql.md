---
title: sys. sp_rda_reauthorize_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sp_rda_reauthorize_db
- sp_rda_reauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reauthorize_db stored procedure
ms.assetid: f6f3e4b2-8c72-4d23-a5de-fe671ca5c5cd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a3fcac7c16de9acf851c623cf7eb1c582e78025c
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: pt-BR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86052986"
---
# <a name="syssp_rda_reauthorize_db-transact-sql"></a>sys.sp_rda_reauthorize_db (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Restaura a conexão autenticada entre um banco de dados local habilitado para Stretch e o banco de dados remoto.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_rda_reauthorize_db @credential = @credential, @with_copy = @with_copy [ , @azure_servername = @azure_servername, @azure_databasename = @azure_databasename ]  
```  
  
## <a name="arguments"></a>Argumentos  
 @credential= * \@ credencial*  
 É a credencial no escopo do banco de dados associada ao banco de dados local habilitado para Stretch.  
  
 @with_copy= * \@ with_copy*  
 Especifica se uma cópia dos dados remotos deve ser feita e conectada à cópia (recomendado). * \@ with_copy* é bit.  
  
 @azure_servername= * \@ azure_servername*  
 Especifica o nome do servidor do Azure que contém os dados remotos. * \@ azure_servername* é sysname.  
  
 @azure_databasename= * \@ azure_databasename*  
 Especifica o nome do banco de dados do Azure que contém o dado remoto. * \@ azure_databasename* é sysname.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou >0 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer db_owner permissões.  
  
## <a name="remarks"></a>Comentários  
 Quando você executa [Sys. sp_rda_reauthorize_db (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) para se reconectar ao banco de dados remoto do Azure, essa operação redefine automaticamente o modo de consulta como LOCAL_AND_REMOTE, que é o comportamento padrão para Stretch Database. Ou seja, as consultas retornam resultados de dados locais e remotos.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir restaura a conexão autenticada entre um banco de dados local habilitado para Stretch e o banco de dados remoto. Ele faz uma cópia dos dados remotos (recomendado) e conecta-se à nova cópia.  
  
```sql  
DECLARE @credentialName nvarchar(128);   
SET @credentialName = N'<existing_database_scoped_credential_name>';   
EXEC sp_rda_reauthorize_db @credential = @credentialName, @with_copy = 1;  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys. sp_rda_deauthorize_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
