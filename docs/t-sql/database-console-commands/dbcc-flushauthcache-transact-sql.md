---
description: DBCC FLUSHAUTHCACHE (Transact-SQL)
title: DBCC FLUSHAUTHCACHE (Transact-SQL)
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC FLUSHAUTHCACHE
- FLUSHAUTHCACHE
- DBCC_FLUSHAUTHCACHE_TSQL
- FLUSHAUTHCACHE_TSQL
helpviewer_keywords:
- DBCC FLUSHAUTHCACHE
ms.assetid: 681ef31d-ceb9-4da5-86bf-bf1240df950f
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 78b584379113b32389f38bf0e6dd3f821758c95d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88367892"
---
# <a name="dbcc-flushauthcache-transact-sql"></a>DBCC FLUSHAUTHCACHE (Transact-SQL)

[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

Esvazia o cache de autenticação do banco de dados que contém informações sobre logons e as regras de firewall, para o banco de dados do usuário atual no [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Essa instrução não se aplica ao banco de dados mestre lógico, porque o banco de dados mestre contém o armazenamento físico para as informações sobre logons e regras de firewall. O usuário que executa a instrução e os outros usuários conectados no momento permanecem conectados. (No momento, o DBCC FLUSHAUTHCACHE não é compatível com o [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].)
 
![Ícone de link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do artigo") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DBCC FLUSHAUTHCACHE [ ; ]  
```

## <a name="arguments"></a>Argumentos  
Nenhum.
  
## <a name="remarks"></a>Comentários  
O cache de autenticação faz uma cópia dos logons e das regras de firewall do servidor que são armazenados no mestre e os coloca na memória no banco de dados de usuário.  Como as informações sobre os usuários de banco de dados independente já são armazenadas no banco de dados de usuário, os usuários de banco de dados independente não fazem parte do cache de autenticação.
As conexões com o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] que ficam ativas continuamente exigem uma nova autorização (executada pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)]) pelo menos a cada 10 horas. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] tenta a nova autorização usando a senha enviada originalmente e não é necessária nenhuma entrada do usuário. Por motivos de desempenho, quando uma senha for redefinida no [!INCLUDE[ssSDS](../../includes/sssds-md.md)], a conexão não será autenticada novamente, mesmo se a conexão for redefinida devido ao pooling de conexões. Esse comportamento é diferente do comportamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local. Se a senha for alterada depois que a conexão for autorizada inicialmente, a conexão precisará ser terminada e uma nova conexão deverá ser feita usando a nova senha. Um usuário com a permissão KILL DATABASE CONNECTION pode terminar explicitamente uma conexão com o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] usando o comando [KILL &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md).
  
## <a name="permissions"></a>Permissões  
Requer a conta do administrador do [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
## <a name="example"></a>Exemplo  
A instrução a seguir limpa o cache de autenticação do banco de dados atual.
  
```sql
DBCC FLUSHAUTHCACHE;  
```  
  
## <a name="see-also"></a>Consulte Também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
