---
title: sp_validate_redirected_publisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validate_redirected_publisher
- sp_validate_redirected_publisher_TSQL
helpviewer_keywords:
- sp_validate_redirected_publisher
ms.assetid: 2b7fdbad-17e4-4442-b0b2-9b5e8f84b91d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8a38d4a197b5e86b41b8a7b791321d8a7ded7ab3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723027"
---
# <a name="sp_validate_redirected_publisher-transact-sql"></a>sp_validate_redirected_publisher (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Verifica se o host atual do banco de dados de publicação pode dar suporte à replicação. Deve ser executado em um banco de dados de distribuição. Esse procedimento é chamado por **sp_get_redirected_publisher**.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
      sp_validate_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @original_publisher = ] 'original_publisher'`O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que originalmente publicou o banco de dados. *original_publisher* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'`O nome do banco de dados que está sendo publicado. *publisher_db* é **sysname**, sem padrão.  
  
`[ @redirected_publisher = ] 'redirected_publisher'`O destino do redirecionamento especificado quando **sp_redirect_publisher** foi chamado para o par Publicador/banco de dados. *redirected_publisher* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum.  
  
## <a name="remarks"></a>Comentários  
 Se não existir nenhuma entrada para o Publicador e o banco de dados de publicação, **sp_validate_redirected_publisher** retornará NULL no parâmetro de saída * \@ redirected_publisher*. Se uma entrada existir, ela será retornada no parâmetro de saída nos casos de êxito e de falha.  
  
 Se a validação for bem-sucedida, **sp_validate_redirected_publisher** retornará uma indicação de êxito.  
  
 Se a validação falhar, ocorrerão erros descrevendo a falha.  
  
## <a name="permissions"></a>Permissões  
 O chamador deve ser um membro da função de servidor fixa **sysadmin** , a **db_owner** função fixa de banco de dados para o banco de dados de distribuição ou um membro de uma lista de acesso à publicação para uma publicação definida associada ao banco de dados Publicador.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_get_redirected_publisher](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_redirect_publisher](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_validate_replica_hosts_as_publishers](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
