---
title: DBCC FREESYSTEMCACHE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 70de1caf9d8bceab6b596952044bb7b3961f60f2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-freesystemcache-transact-sql"></a>DBCC FREESYSTEMCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Libera todas as entradas não utilizadas de todos os caches. De forma pró-ativa, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] limpa em segundo plano as entradas de cache para tornar a memória disponível para entradas atuais. Porém, você pode usar este comando para remover manualmente entradas não usadas de todos os caches ou de um cache de pool do Administrador de Recursos especificado.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
```sql
DBCC FREESYSTEMCACHE   
    ( 'ALL' [, pool_name ] )   
    [WITH   
    { [ MARK_IN_USE_FOR_REMOVAL ] , [ NO_INFOMSGS ]  }  
    ]  
```  
  
## <a name="arguments"></a>Argumentos  
 ('Todos' [,*nome_do_pool* ])  
 ALL especifica todos os caches suportados.  
 *nome_do_pool* Especifica um cache de pool do administrador de recursos. Somente as entradas associadas a esse pool serão liberadas.  
  
 MARK_IN_USE_FOR_REMOVAL  
 Remove de forma assíncrona as entradas atualmente utilizadas de seus respectivos caches quando elas não são mais utilizadas. As novas entradas criadas no cache depois que o DBCC FREESYSTEMCACHE WITH MARK_IN_USE_FOR_REMOVAL for executado não serão afetadas.  
  
 NO_INFOMSGS  
 Suprime todas as mensagens informativas.  
  
## <a name="remarks"></a>Comentários  
A execução de DBCC FREESYSTEMCACHE limpa o cache de planos para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A limpeza do cache de planos gera uma recompilação de todos os planos de execução subsequentes e pode provocar uma redução repentina e temporária do desempenho de consultas. Para cada armazenamento em cache limpo no cache de planos, o log de erros de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém a seguinte mensagem informativa: "O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou %d ocorrência(s) de liberação de armazenamento em cache '% s' (parte do cache de planos) devido às operações 'DBCC FREEPROCCACHE' ou 'DBCC FREESYSTEMCACHE'". Essa mensagem é registrada a cada cinco minutos, contanto que o cache seja liberado dentro desse intervalo de tempo.

## <a name="result-sets"></a>Conjuntos de resultados  
DBCC FREESYSTEMCACHE retorna: "execução do DBCC foi concluída. Se o DBCC imprimiu mensagens de erro, entre em contato com o administrador do sistema".
  
## <a name="permissions"></a>Permissões  
Exige a permissão ALTER SERVER STATE no servidor.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-releasing-unused-cache-entries-from-a-resource-governor-pool-cache"></a>A. Removendo entradas de cache não utilizadas de um cache do pool do Administrador de Recursos  
O exemplo a seguir ilustra como limpar caches que são específicos de pool de recursos do Administrador de Recursos.
  
```sql
-- Clean all the caches with entries specific to the resource pool named "default".  
DBCC FREESYSTEMCACHE ('ALL', default);  
```  
  
### <a name="b-releasing-entries-from-their-respective-caches-after-they-become-unused"></a>B. Removendo entradas de seus respectivos caches quando elas não são mais utilizadas.  
O exemplo seguinte usa a cláusula MARK_IN_USE_FOR_REMOVAL para remover entradas de todos os caches atuais quando elas não são mais utilizadas.
  
```sql
DBCC FREESYSTEMCACHE ('ALL') WITH MARK_IN_USE_FOR_REMOVAL;  
```  
  
## <a name="see-also"></a>Consulte também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)  
[DBCC FREESESSIONCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)  
[Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)
  
  

