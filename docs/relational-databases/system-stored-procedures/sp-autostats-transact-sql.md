---
title: sp_autostats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_autostats_TSQL
- sp_autostats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_autostats
ms.assetid: d1df8c15-ee73-49eb-9d13-6e98943c3e38
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b57f708d24cff611e256915b9981e13ecf89d4e9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="spautostats-transact-sql"></a>sp_autostats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Exibe ou altera a opção de atualização das estatísticas automáticas, AUTO_UPDATE_STATISTICS, para um índice, um objeto de estatísticas, uma tabela ou uma exibição indexada.  
  
 Para obter mais informações sobre a opção AUTO_UPDATE_STATISTICS, consulte [opções ALTER DATABASE SET &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) e [estatísticas](../../relational-databases/statistics/statistics.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_autostats [ @tblname = ] 'table_or_indexed_view_name'   
    [ , [ @flagc = ] 'stats_value' ]   
    [ , [ @indname = ] 'statistics_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@tblname=** ] **'***table_or_indexed_view_name***'**  
 É o nome da tabela ou da exibição indexada na qual exibir a opção AUTO_UPDATE_STATISTICS. *table_or_indexed_view_name* é **nvarchar(776)**, sem padrão.  
  
 [  **@flagc=** ] **'***stats_value***'**  
 Atualiza a opção AUTO_UPDATE_STATISTICS para um destes valores:  
  
 **ON** = ON  
  
 **OFF** = OFF  
  
 Quando *stats_flag* não é especificado, exiba a configuração AUTO_UPDATE_STATISTICS atual. *stats_value* é **varchar (10)**, com um padrão NULL.  
  
 [  **@indname=** ] **'***statistics_name***'**  
 É o nome das estatísticas de exibição ou atualização da opção AUTO_UPDATE_STATISTICS. Para exibir as estatísticas de um índice, é possível usar o nome do índice; um índice e seu objeto de estatísticas correspondente têm o mesmo nome.  
  
 *statistics_name* é **sysname**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se *stats_flag* for especificado, **sp_autostats** informará a ação que foi executada mas não retorna nenhum conjunto de resultados.  
  
 Se *stats_flag* não for especificado, **sp_autostats** retorna o conjunto de resultados a seguir.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**Nome do Índice**|**varchar(60)**|Nome do índice ou das estatísticas.|  
|**AUTOSTATS**|**varchar(3)**|Valor atual da opção AUTO_UPDATE_STATISTICS.|  
|**Última atualização**|**datetime**|Data da atualização mais recente das estatísticas.|  
  
 O conjunto de resultados para uma tabela ou exibição indexada inclui estatísticas criadas para índices, estatísticas de coluna única geradas com a opção AUTO_CREATE_STATISTICS e estatísticas criadas com o [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) instrução.  
  
## <a name="remarks"></a>Remarks  
 Se o índice especificado for desabilitado ou a tabela especificada tiver um índice clusterizado desabilitado, uma mensagem de erro será exibida.  
  
 AUTO_UPDATE_STATISTICS será sempre OFF para tabelas otimizadas em memória.  
  
## <a name="permissions"></a>Permissões  
 Para alterar AUTO_UPDATE_STATISTICS opção exige associação ao **db_owner** fixo de função de banco de dados ou a permissão ALTER em *table_name*. Para exibir AUTO_UPDATE_STATISTICS, a opção exige associação a **pública** função.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-display-the-status-of-all-statistics-on-a-table"></a>A. Exibir o status de todas as estatísticas em uma tabela  
 O exemplo a seguir exibe o status de todas as estatísticas na tabela `Product`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product';  
GO  
```  
  
### <a name="b-enable-autoupdatestatistics-for-all-statistics-on-a-table"></a>B. Habilitar AUTO_UPDATE_STATISTICS para todas as estatísticas de uma tabela  
 O exemplo a seguir habilita a opção AUTO_UPDATE_STATISTICS para todas as estatísticas da tabela `Product`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product', 'ON';  
GO  
```  
  
### <a name="c-disable-autoupdatestatistics-for-a-specific-index"></a>C. Desabilitar AUTO_UPDATE_STATISTICS para um determinado índice  
 O exemplo a seguir desabilita a opção AUTO_UPDATE_STATISTICS para o índice `AK_Product_Name` na tabela `Product`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product', 'OFF', AK_Product_Name;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Estatística](../../relational-databases/statistics/statistics.md)   
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_createstats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
