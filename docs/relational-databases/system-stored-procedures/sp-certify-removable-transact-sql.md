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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1d2586f1ad5f7be9b5916caea7699ca9c90f22db
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47691404"
---
# <a name="spcertifyremovable-transact-sql"></a>sp_certify_removable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verifica se um banco de dados está configurado corretamente para distribuição em mídias removíveis e informa qualquer problema ao usuário.  
  
> **IMPORTANTE:** [! INCLUIR[ssNoteDepFutureAvoid](../../t-sql/statements/create-database-sql-server-transact-sql.md) em vez disso.  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_certify_removable [ @dbname= ] 'dbname'  
     [ , [ @autofix = ] 'auto' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@dbname=**] **'***dbname***'**  
 Especifica o banco de dados a ser verificado. *DBName* está **sysname**.  
  
 [  **@autofix=**] **'auto'**  
 Atribui a propriedade do banco de dados e todos os objetos de banco de dados ao administrador de sistema e descarta quaisquer usuários de banco de dados criados pelo usuário e permissões não padrão. *auto* está **nvarchar(4)**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Se o banco de dados estiver configurado corretamente, **sp_certify_removable** executará o seguinte:  
  
-   Configura o banco de dados em modo offline para que os arquivos possam ser copiados.  
  
-   Atualiza estatísticas em todas as tabelas e informa qualquer problema de propriedade ou usuário  
  
-   Marca os grupos de arquivos de dados como somente leitura, para que esses arquivos possam ser copiados para mídia somente leitura.  
  
 O administrador de sistema deve ser o proprietário do banco de dados e de todos os objetos de banco de dados. O administrador do sistema é um usuário conhecido que existe em todos os servidores que estão executando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e podem ser esperados de existir quando o banco de dados mais tarde é distribuído e instalado.  
  
 Se você executar **sp_certify_removable** sem o **automático** valor e ele retorna informações sobre qualquer uma das seguintes condições:  
  
-   O administrador de sistema não é o proprietário do banco de dados.  
  
-   Existem usuários criados pelo usuário.  
  
-   O administrador de sistema não é proprietário de todos os objetos no banco de dados.  
  
-   Permissões não padrão foram concedidas.  
  
 Você pode corrigir estas condições das seguintes formas:  
  
-   Use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as ferramentas e procedimentos e execute **sp_certify_removable** novamente.  
  
-   Basta executar **sp_certify_removable** com o **automático** valor.  
  
 Note que este procedimento armazenado somente verifica os usuários e as permissões de usuário. Você pode adicionar grupos ao banco de dados e conceder permissões a esses grupos. Para obter mais informações, veja [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Execute permissões são restritas aos membros do **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir certifica que o banco de dados `inventory` está pronto para ser removido.  
  
```  
EXEC sp_certify_removable inventory, AUTO;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_create_removable &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-removable-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_dbremove &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
