---
title: DBCC SQLPERF (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SQLPERF
- DBCC_SQLPERF_TSQL
- SQLPERF_TSQL
- DBCC SQLPERF
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], transaction logs
- transaction logs [SQL Server], space usage
- space [SQL Server], transaction logs
- DBCC SQLPERF statement
ms.assetid: ec9225ce-e20f-4b03-8b3a-7bcad8a649df
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 41f854ce5ff1261829df621931d3a736426f32c8
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-sqlperf-transact-sql"></a>DBCC SQLPERF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Fornece estatísticas de uso do espaço do log de transações para todos os bancos de dados. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também pode ser usado para redefinir as estatísticas de espera e trava.
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([visualização em algumas regiões](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DBCC SQLPERF   
(  
     [ LOGSPACE ]  
     |  
          [ "sys.dm_os_latch_stats" , CLEAR ]  
     |  
     [ "sys.dm_os_wait_stats" , CLEAR ]  
)   
     [WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
LOGSPACE  
Retorna o tamanho atual do log de transações e a porcentagem de espaço usado pelo log para cada banco de dados. Você pode usar essas informações para monitorar a quantidade de espaço usada em um log de transações.  
  
**"** **sys.DM os_latch_stats",** limpar  
Zera as estatísticas de trava. Para obter mais informações, consulte [sys.DM os_latch_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md). Essa opção não está disponível no [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
**"sys.DM os_wait_stats"** limpar  
Zera as estatísticas de espera. Para obter mais informações, consulte [sys.DM os_wait_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). Essa opção não está disponível no [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
WITH NO_INFOMSGS  
Suprime todas as mensagens informativas com níveis de severidade de 0 a 10.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 A tabela a seguir descreve as colunas do conjunto de resultados.  
  
|Nome da coluna|Definição|  
|---|---|
|**Nome do Banco de Dados**|Nome do banco de dados da estatística de logs exibida.|  
|**Tamanho do log (MB)**|Tamanho atual alocado ao log. Esse valor sempre é menor que a quantidade alocada originalmente para o espaço de log porque o [!INCLUDE[ssDE](../../includes/ssde-md.md)] reserva uma quantidade pequena de espaço em disco para informações de cabeçalho internas.|  
|**Espaço de log usado (%)**|Porcentagem do arquivo de log em uso para armazenar informações de log de transação no momento.|  
|**Status**|Status do arquivo de log. Sempre 0.|  
  
## <a name="remarks"></a>Comentários  
O log de transações registra cada transação feita em um banco de dados. Para obter mais informações, consulte [o Log de transações &#40; SQL Server &#41; ](../../relational-databases/logs/the-transaction-log-sql-server.md).
  
## <a name="permissions"></a>Permissões  
Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executar DBCC SQLPERF requer permissão VIEW SERVER STATE no servidor. Zerar estatísticas de espera e trava requer a permissão ALTER SERVER STATE no servidor.
  
Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)] camadas Premium requer a permissão VIEW DATABASE STATE no banco de dados. Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)] camadas Standard e Basic requer o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] conta de administrador. Não há suporte para reiniciar as estatísticas de espera e de trava.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-displaying-log-space-information-for-all-databases"></a>A. Exibindo informações de espaço de log para todos os bancos de dados  
O exemplo a seguir exibe informações de `LOGSPACE` sobre todos os bancos de dados contidos na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
```sql  
DBCC SQLPERF(LOGSPACE);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Database Name Log Size (MB) Log Space Used (%) Status        
------------- ------------- ------------------ -----------   
master         3.99219      14.3469            0   
tempdb         1.99219      1.64216            0   
model          1.0          12.7953            0   
msdb           3.99219      17.0132            0   
AdventureWorks 19.554688    17.748701          0  
```  
  
### <a name="b-resetting-wait-statistics"></a>B. Redefinindo estatísticas de espera  
O exemplo a seguir zera as estatísticas de espera da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
```sql  
DBCC SQLPERF("sys.dm_os_wait_stats",CLEAR);  
```  
  
## <a name="see-also"></a>Consulte também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_spaceused &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
  
  


