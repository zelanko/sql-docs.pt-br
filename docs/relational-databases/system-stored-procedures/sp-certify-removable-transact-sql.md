---
title: sp_certify_removable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_certify_removable_TSQL
- sp_certify_removable
dev_langs:
- TSQL
helpviewer_keywords:
- sp_certify_removable
ms.assetid: ca12767f-0ae5-4652-b523-c23473f100a1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b873931c5d09f3c54f61e872f8ea6646408c1a04
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715958"
---
# <a name="sp_certify_removable-transact-sql"></a>sp_certify_removable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Verifica se um banco de dados está configurado corretamente para distribuição em mídias removíveis e informa qualquer problema ao usuário.  
  
> **IMPORTANTE:** [! INCLUA[ssNoteDepFutureAvoid](../../t-sql/statements/create-database-sql-server-transact-sql.md) em vez disso.  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_certify_removable [ @dbname= ] 'dbname'  
     [ , [ @autofix = ] 'auto' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] 'dbname'`Especifica o banco de dados a ser verificado. *dbname* é **sysname**.  
  
`[ @autofix = ] 'auto'`Fornece a propriedade do banco de dados e todos os objetos de banco de dados para o administrador do sistema e descarta quaisquer usuários de banco de dados criados pelo usuário e permissões não padrão. *auto* é **nvarchar (4)**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Se o banco de dados estiver configurado corretamente, **sp_certify_removable** executará o seguinte:  
  
-   Configura o banco de dados em modo offline para que os arquivos possam ser copiados.  
  
-   Atualiza estatísticas em todas as tabelas e informa qualquer problema de propriedade ou usuário  
  
-   Marca os grupos de arquivos de dados como somente leitura, para que esses arquivos possam ser copiados para mídia somente leitura.  
  
 O administrador de sistema deve ser o proprietário do banco de dados e de todos os objetos de banco de dados. O administrador do sistema é um usuário conhecido que existe em todos os servidores que estão em execução [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e pode esperar que exista quando o banco de dados for distribuído e instalado posteriormente.  
  
 Se você executar **sp_certify_removable** sem o valor **automático** e ele retornará informações sobre qualquer uma das seguintes condições:  
  
-   O administrador de sistema não é o proprietário do banco de dados.  
  
-   Existem usuários criados pelo usuário.  
  
-   O administrador de sistema não é proprietário de todos os objetos no banco de dados.  
  
-   Permissões não padrão foram concedidas.  
  
 Você pode corrigir estas condições das seguintes formas:  
  
-   Use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ferramentas e procedimentos e execute **sp_certify_removable** novamente.  
  
-   Basta executar **sp_certify_removable** com o valor **automático** .  
  
 Note que este procedimento armazenado somente verifica os usuários e as permissões de usuário. Você pode adicionar grupos ao banco de dados e conceder permissões a esses grupos. Para obter mais informações, veja [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução são restritas a membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir certifica que o banco de dados `inventory` está pronto para ser removido.  
  
```  
EXEC sp_certify_removable inventory, AUTO;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [&#41;&#40;Transact-SQL de sp_create_removable](../../relational-databases/system-stored-procedures/sp-create-removable-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dbremove](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
