---
title: LOGON DROP (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP LOGIN
- DROP_LOGIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting login accounts
- logins [SQL Server], removing
- DROP LOGIN statement
- removing login accounts
- dropping login accounts
ms.assetid: acb5c3dc-7aa2-49f6-9330-573227ba9b1a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e43f37e0aa24cf6ab1ac7b01b378e461e5dea706
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="drop-login-transact-sql"></a>DROP LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Remove uma conta de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DROP LOGIN login_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *login_name*  
 Especifica o nome do logon a ser descartado.  
  
## <a name="remarks"></a>Comentários  
 Um logon não pode ser removido enquanto estiver ativo. Um logon que possui qualquer protegível, objeto em nível de servidor ou trabalho do SQL Server Agent não pode ser descartado.  
  
 É possível descartar um logon para o qual usuários de banco de dados são mapeados; porém, isso criará usuários órfãos. Para obter mais informações, consulte [Solução de problemas de usuários órfãos &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md).  
  
 Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], dados de logon necessárias para autenticar uma conexão e as regras de firewall de nível de servidor são armazenados em cache temporariamente em cada banco de dados. Esse cache é atualizado periodicamente. Para forçar uma atualização do cache de autenticação e certifique-se de que um banco de dados tem a versão mais recente da tabela de logons, execute [DBCC FLUSHAUTHCACHE &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY LOGIN no servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-dropping-a-login"></a>A. Descartar um logon  
 O exemplo a seguir descarta o logon `WilliJo`.  
  
```  
DROP LOGIN WilliJo;  
GO 
```  
 
  
## <a name="see-also"></a>Consulte também  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  

