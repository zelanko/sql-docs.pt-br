---
title: sp_redirect_publisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_redirect_publisher_TSQL
- sp_redirect_publisher
helpviewer_keywords:
- sp_redirect_publisher
ms.assetid: af45e2b2-57fb-4bcd-a58b-e61401fb3b26
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 54a53c3e1678215ad2eb1410a00da4904d0f84e7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734308"
---
# <a name="sp_redirect_publisher-transact-sql"></a>sp_redirect_publisher (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Especifica um publicador redirecionado para um par de publicador/banco de dados existente. Se o banco de dados do Publicador pertencer a um grupo de disponibilidade Always On, o Publicador Redirecionado será o nome do ouvinte do grupo de disponibilidade associado ao grupo de disponibilidade.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_redirect_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name'   
    [ , [ @redirected_publisher = ] 'new_publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @original_publisher = ] 'original_publisher'`O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que originalmente publicou o banco de dados. *original_publisher* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'`O nome do banco de dados que está sendo publicado. *publisher_db* é **sysname**, sem padrão.  
  
`[ @redirected_publisher = ] 'redirected_publisher'`O nome do ouvinte do grupo de disponibilidade associado ao grupo de disponibilidade que será o novo Publicador. *redirected_publisher* é **sysname**, sem padrão. Quando o ouvinte do grupo de disponibilidade estiver configurado para a porta não padrão, especifique o número da porta junto com o nome do ouvinte, por exemplo, `'Listenername,51433'`  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **sp_redirect_publisher** é usado para permitir que um Publicador de replicação seja redirecionado para o primário atual de um grupo de disponibilidade Always on associando o par de Publicador/banco de dados ao ouvinte de um grupo de disponibilidade. Execute **sp_redirect_publisher** depois que o ouvinte AG tiver sido configurado para o grupo de disponibilidade que contém o banco de dados publicado.  
  
 Se o banco de dados de publicação no Publicador original for removido de um grupo de disponibilidade na réplica primária, execute **sp_redirect_publisher** sem especificar um valor para o parâmetro * \@ redirected_publisher* para remover o redirecionamento para o par Publicador/banco de dados. Para obter mais informações sobre como redirecionar o Publicador quando, consulte [mantendo um banco de dados de publicação AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md).  
  
## <a name="permissions"></a>Permissões  
 O chamador deve ser um membro da função de servidor fixa **sysadmin** , a **db_owner** função fixa de banco de dados para o banco de dados de distribuição ou um membro de uma lista de acesso à publicação para uma publicação definida associada ao banco de dados Publicador.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_validate_redirected_publisher](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_get_redirected_publisher](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_validate_replica_hosts_as_publishers](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
