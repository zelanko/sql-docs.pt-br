---
title: DBCC FLUSHAUTHCACHE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC FLUSHAUTHCACHE
- FLUSHAUTHCACHE
- DBCC_FLUSHAUTHCACHE_TSQL
- FLUSHAUTHCACHE_TSQL
helpviewer_keywords:
- DBCC FLUSHAUTHCACHE
ms.assetid: 681ef31d-ceb9-4da5-86bf-bf1240df950f
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3ba6a519ebcdbbc70bf19ec491539a3b07fb6c85
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-flushauthcache-transact-sql"></a>DBCC FLUSHAUTHCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Esvazia o cache de autenticação de banco de dados que contém informações sobre logons e as regras de firewall, o banco de dados do usuário atual em [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Essa instrução não é aplicável para o banco de dados mestre lógico, porque o banco de dados mestre contém o armazenamento físico para as informações sobre logons e as regras de firewall. O usuário que executa a instrução e outros usuários atualmente conectados permaneçam conectados. (DBCC FLUSHAUTHCACHE atualmente não há suporte para [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].)
 
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DBCC FLUSHAUTHCACHE [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
Nenhum.
  
## <a name="remarks"></a>Comentários  
O cache de autenticação faz uma cópia de logons e as regras de firewall de servidor que são armazenadas no mestre e os coloca na memória no banco de dados do usuário.  Como informações sobre usuários de banco de dados independente já são armazenados no banco de dados de usuário, os usuários de banco de dados independente não fazem parte do cache de autenticação.
Conexões ativas continuamente [!INCLUDE[ssSDS](../../includes/sssds-md.md)] exigir autorização (executadas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)]) pelo menos a cada 10 horas. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] tentativas de autorização usando a senha originalmente enviada e nenhum usuário de entrada é necessária. Por motivos de desempenho, quando uma senha é redefinida no [!INCLUDE[ssSDS](../../includes/sssds-md.md)], a conexão não será autenticado novamente, mesmo se a conexão for redefinida devido ao pooling de conexão. Isso é diferente do comportamento do local [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se a senha foi alterada desde que a conexão foi autorizado inicialmente, a conexão deve ser terminada e uma nova conexão feita usando a nova senha. Um usuário com a permissão KILL DATABASE CONNECTION explicitamente pode encerrar uma conexão para [!INCLUDE[ssSDS](../../includes/sssds-md.md)] usando o [KILL &#40; Transact-SQL &#41; ](../../t-sql/language-elements/kill-transact-sql.md) comando.
  
## <a name="permissions"></a>Permissões  
Requer o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] conta de administrador.
  
## <a name="example"></a>Exemplo  
A instrução a seguir limpa o cache de autenticação para o banco de dados atual.
  
```sql
DBCC FLUSHAUTHCACHE;  
```  
  
## <a name="see-also"></a>Consulte também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  

