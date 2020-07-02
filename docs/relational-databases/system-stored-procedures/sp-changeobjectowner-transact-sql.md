---
title: sp_changeobjectowner (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_changeobjectowner_TSQL
- sp_changeobjectowner
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changeobjectowner
ms.assetid: 45b3dc1c-1cde-45b7-a248-5195c12973e9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1e6f664cc763e56135ddf1c35f5f0057d97ec2d7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771459"
---
# <a name="sp_changeobjectowner-transact-sql"></a>sp_changeobjectowner (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Altera o proprietário de um objeto no banco de dados atual.  
  
> [!IMPORTANT]
>  Esse procedimento armazenado funciona apenas com os objetos disponíveis no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] . [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use [ALTER Schema](../../t-sql/statements/alter-schema-transact-sql.md) ou [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) . **sp_changeobjectowner** altera o esquema e o proprietário. Para preservar a compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esse procedimento armazenado irá alterar proprietários de objetos somente quando o proprietário atual e o novo possuírem esquemas que tenham o mesmo nome que seus nomes de usuário do banco de dados.  
> 
> [!IMPORTANT]
>  Um novo requisito de permissão foi adicionado a esse procedimento armazenado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changeobjectowner [ @objname = ] 'object' , [ @newowner = ] 'owner'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @objname = ] 'object'`É o nome de uma tabela, exibição, função definida pelo usuário ou procedimento armazenado existente no banco de dados atual. *Object* é um **nvarchar (776)**, sem padrão. o *objeto* pode ser qualificado com o proprietário do objeto existente, no formato _existing_owner_**.** _objeto_ se o esquema e seu proprietário tiverem o mesmo nome.  
  
`[ @newowner = ] 'owner_ '`É o nome da conta de segurança que será o novo proprietário do objeto. *Owner* é **sysname**, sem padrão. o *proprietário* deve ser um usuário de banco de dados, uma função de servidor, um [!INCLUDE[msCoName](../../includes/msconame-md.md)] logon do Windows ou um grupo do Windows válido com acesso ao banco de dados atual. Se o novo proprietário for um usuário ou grupo do Windows para o qual não há uma entidade correspondente no nível de banco de dados, será criado um usuário de banco de dados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changeobjectowner** remove todas as permissões existentes do objeto. Você precisará reaplicar as permissões que deseja manter depois de executar **sp_changeobjectowner**. Portanto, é recomendável que você execute o script das permissões existentes antes de executar **sp_changeobjectowner**. Depois que propriedade do objeto foi alterada, você poderá usar o script para reaplicar permissões. É necessário modificar o proprietário do objeto no script de permissões antes de executar.  
  
 Para alterar o proprietário de um protegível, use ALTER AUTHORIZATION. Para alterar um esquema, use ALTER SCHEMA.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa **db_owner** ou associação tanto à função de banco de dados fixa **db_ddladmin** quanto à **db_securityadmin** função de banco de dados fixa, além de controlar a permissão no objeto.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera o proprietário da tabela `authors` para `Corporate\GeorgeW`.  
  
```  
EXEC sp_changeobjectowner 'authors', 'Corporate\GeorgeW';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changedbowner](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
