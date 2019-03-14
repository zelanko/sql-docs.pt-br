---
title: DBCC FREESYSTEMCACHE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FREESYSTEMCACHE_TSQL
- DBCC_FREESYSTEMCACHE_TSQL
- DBCC FREESYSTEMCACHE
- FREESYSTEMCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- clearing unused cache entries
- DBCC FREESYSTEMCACHE statement
- unused cache entries
- releasing unused cache entries
- freeing unused cache entries
- cleaning unused cache entries
ms.assetid: 4b5c460b-e4ad-404a-b4ca-d65aba38ebbb
author: pmasl
ms.author: umajay
manager: craigg
ms.openlocfilehash: 00b6ddce8d5c69e16913290b0300fc6828352147
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685673"
---
# <a name="dbcc-freesystemcache-transact-sql"></a>DBCC FREESYSTEMCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Libera todas as entradas não utilizadas de todos os caches. De forma pró-ativa, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] limpa em segundo plano as entradas de cache para tornar a memória disponível para entradas atuais. Porém, você pode usar este comando para remover manualmente entradas não usadas de todos os caches ou de um cache de pool do Resource Governor especificado.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
```sql
DBCC FREESYSTEMCACHE   
    ( 'ALL' [, pool_name ] )   
    [WITH   
    { [ MARK_IN_USE_FOR_REMOVAL ] , [ NO_INFOMSGS ]  }  
    ]  
```  
  
## <a name="arguments"></a>Argumentos  
( 'ALL' [,_pool\_name_ ] )  
ALL especifica todos os caches suportados.  
_pool\_name_ especifica um cache de pool do Resource Governor. Somente as entradas associadas a esse pool são liberadas.  
  
MARK_IN_USE_FOR_REMOVAL  
Libera de forma assíncrona as entradas usadas no momento de seus respectivos caches quando elas deixam de ser usadas. As novas entradas criadas no cache não serão afetadas depois que o DBCC FREESYSTEMCACHE WITH MARK_IN_USE_FOR_REMOVAL for executado.  
  
NO_INFOMSGS  
Suprime todas as mensagens informativas.  
  
## <a name="remarks"></a>Remarks  
A execução de DBCC FREESYSTEMCACHE limpa o cache de planos da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A limpeza do cache de planos gera uma recompilação de todos os planos de execução subsequentes e pode provocar uma redução repentina e temporária no desempenho de consultas. Para cada armazenamento em cache limpo no cache de planos, o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conterá a seguinte mensagem informativa: "O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou %d ocorrências de liberação do armazenamento em cache '%s' (parte do cache de planos) devido às operações 'DBCC FREEPROCCACHE' ou 'DBCC FREESYSTEMCACHE'". Essa mensagem é registrada a cada cinco minutos, contanto que o cache seja liberado dentro desse intervalo de tempo.

## <a name="result-sets"></a>Conjuntos de resultados  
DBCC FREESYSTEMCACHE retorna: "A execução do DBCC foi concluída. Se o DBCC imprimiu mensagens de erro, entre em contato com o administrador do sistema".
  
## <a name="permissions"></a>Permissões  
Exige a permissão ALTER SERVER STATE no servidor.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-releasing-unused-cache-entries-from-a-resource-governor-pool-cache"></a>A. Removendo entradas de cache não utilizadas de um cache do pool do Administrador de Recursos  
O exemplo a seguir ilustra como limpar caches que são específicos de pool de recursos do Administrador de Recursos.
  
```sql
-- Clean all the caches with entries specific to the resource pool named "default".  
DBCC FREESYSTEMCACHE ('ALL', default);  
```  
  
### <a name="b-releasing-entries-from-their-respective-caches-after-they-become-unused"></a>b. Removendo entradas de seus respectivos caches quando elas não são mais utilizadas.  
O exemplo seguinte usa a cláusula MARK_IN_USE_FOR_REMOVAL para remover entradas de todos os caches atuais quando elas não são mais utilizadas.
  
```sql
DBCC FREESYSTEMCACHE ('ALL') WITH MARK_IN_USE_FOR_REMOVAL;  
```  
  
## <a name="see-also"></a>Consulte Também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)  
[DBCC FREESESSIONCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)  
[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)
  
  
