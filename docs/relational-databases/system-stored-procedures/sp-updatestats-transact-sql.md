---
title: sp_updatestats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_updatestats_TSQL
- sp_updatestats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatestats
ms.assetid: 01184651-6e61-45d9-a502-366fecca0ee4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 51fd5471ac678a1d61986aaa9219eec923c38485
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535758"
---
# <a name="spupdatestats-transact-sql"></a>sp_updatestats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Execuções `UPDATE STATISTICS` em relação a todas as tabelas internas e definidas pelo usuário no banco de dados atual.  
  
Para obter mais informações sobre `UPDATE STATISTICS`, consulte [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md). Para obter mais informações sobre estatísticas, consulte [Estatísticas](../../relational-databases/statistics/statistics.md).  
    
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_updatestats [ [ @resample = ] 'resample']  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="arguments"></a>Argumentos  
`[ @resample = ] 'resample'` Especifica que **sp_updatestats** usará a opção RESAMPLE das [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md) instrução. Se **'resample'** não for especificado, **sp_updatestats** atualizará as estatísticas usando a amostragem padrão. **Criar nova amostra** está **varchar(8)** com um valor padrão NO.  
  
## <a name="remarks"></a>Comentários  
 **sp_updatestats** executa `UPDATE STATISTICS`, especificando o `ALL` palavra-chave, em todas as tabelas internas e definidas pelo usuário no banco de dados. sp_updatestats exibe mensagens que indicam seu progresso. Quando a atualização é concluída, ela informa que as estatísticas foram atualizadas em todas as tabelas.  
  
O sp_updatestats atualiza estatísticas em índices não clusterizados desabilitados e não atualiza estatísticas em índices clusterizados desabilitados.  
  
Para tabelas baseadas em disco, **sp_updatestats** atualiza as estatísticas com base no **modification_counter** informações de **DM db_stats_properties** exibição do catálogo atualização de estatísticas em que pelo menos uma linha foi modificada. Estatísticas em tabelas com otimização de memória sempre são atualizadas durante a execução **sp_updatestats**. Portanto, não são executadas **sp_updatestats** mais do que necessário.  
  
**sp_updatestats** pode disparar uma recompilação de procedimentos armazenados ou outro código compilado. No entanto, **sp_updatestats** talvez não provoque uma recompilação, se apenas um plano de consulta é possível que as tabelas referenciadas e os índices. Uma recompilação será desnecessária nesses casos mesmo que as estatísticas sejam atualizadas.  
  
Para bancos de dados com um nível de compatibilidade inferior a 90, executando **sp_updatestats** não preserva a configuração mais recente de NORECOMPUTE para estatísticas específicas. Para bancos de dados com um nível de compatibilidade 90 ou superior, sp_updatestats preserva a opção NORECOMPUTE mais recente para estatísticas específicas. Para obter mais informações sobre como desabilitar e reabilitar atualizações de estatísticas, veja [Estatísticas](../../relational-databases/statistics/statistics.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **sysadmin** fixo de função de servidor ou a propriedade do banco de dados (**dbo**).  

## <a name="examples"></a>Exemplos  
O exemplo a seguir atualiza as estatísticas de tabelas no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_updatestats;   
```  

## <a name="automatic-index-and-statistics-management"></a>Índice automático e gerenciamento de estatísticas
Aproveite soluções como a [Desfragmentação de índice adaptável](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag) para gerenciar automaticamente a desfragmentação de índice e as atualizações de estatísticas em um ou mais bancos de dados. Este procedimento escolhe automaticamente se deve recompilar ou reorganizar um índice de acordo com seu nível de fragmentação, entre outros parâmetros, e atualizar as estatísticas com um limite linear.

## <a name="see-also"></a>Consulte também  
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_createstats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [Procedimentos armazenados do sistema](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
 
