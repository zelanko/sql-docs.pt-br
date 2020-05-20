---
title: sys. dm_tran_active_snapshot_database_transactions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_active_snapshot_database_transactions_TSQL
- dm_tran_active_snapshot_database_transactions
- sys.dm_tran_active_snapshot_database_transactions
- dm_tran_active_snapshot_database_transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_active_snapshot_database_transactions dynamic management view
ms.assetid: 55b83f9c-da10-4e65-9846-f4ef3c0c0f36
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 42ed4cebfda43801cdbc3ab42225783c674612e0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82810950"
---
# <a name="sysdm_tran_active_snapshot_database_transactions-transact-sql"></a>sys.dm_tran_active_snapshot_database_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Em uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta exibição de gerenciamento dinâmico retorna uma tabela virtual para todas as transações ativas que geram ou potencialmente acessam versões de linhas. As transações são incluídas em uma ou mais das seguintes condições:  
  
-   Quando uma ou ambas as opções de banco de dados ALLOW_SNAPSHOT_ISOLATION  e READ_COMMITTED_SNAPSHOT estão definidas como ON:  
  
    -   Há uma linha para cada transação cuja execução aconteça em nível de isolamento do instantâneo ou em nível de isolamento confirmado por leitura utilizando controle de versão de linhas.  
  
    -   Há uma linha para cada transação que cause a criação de uma versão de linha no banco de dados atual. Por exemplo, a transação gera uma versão de linha pela atualização ou exclusão de uma linha no banco de dados atual.  
  
-   Quando um gatilho é ativado, há uma linha para a transação sob a qual o gatilho está executando.  
  
-   Quando um procedimento de indexação online está em execução, há uma linha para a transação que está criando o índice.  
  
-   Quando uma sessão MARS (Multiple Active Results Sets) está habilitada, há uma linha para cada transação que está acessando versões de linha.  
  
 Esta exibição de gerenciamento dinâmico não inclui transações de sistema.  
  
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys. dm_pdw_nodes_tran_active_snapshot_database_transactions**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.dm_tran_active_snapshot_database_transactions  
```  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**transaction_id**|**bigint**|Número de identificação exclusivo atribuído à transação. O ID transação é usado principalmente para identificar a transação em operações de bloqueio.|  
|**transaction_sequence_num**|**bigint**|Número de sequência da transação. Trata-se de um número de sequência exclusivo atribuído a uma transação quando ela se inicia. Transações que não geram registros de versão e não usam verificações de instantâneo não receberão um número de sequência de transação.|  
|**commit_sequence_num**|**bigint**|Número de sequência que indica quando a transação termina (confirmações ou paradas). Para transações ativas, o valor é NULL.|  
|**is_snapshot**|**int**|0 = Não é uma transação de isolamento de instantâneo.<br /><br /> 1 = É uma transação de isolamento de instantâneo.|  
|**session_id**|**int**|ID da sessão que iniciou a transação.|  
|**first_snapshot_sequence_num**|**bigint**|Número de sequência de transação mais baixo das transações que estavam ativas quando o instantâneo foi feito. Em execução, uma transação de instantâneo faz um instantâneo de todas as transações ativas naquele momento. No caso de transações não instantâneo, esta coluna mostra 0.|  
|**max_version_chain_traversed**|**int**|Comprimento máximo da cadeia de versão que é atravessada para localizar a versão consistente transacional.|  
|**average_version_chain_traversed**|**real**|Número médio de versões de linha nas cadeias de versão que são atravessadas.|  
|**elapsed_time_seconds**|**bigint**|Tempo decorrido desde que a transação obteve seu número de sequência de transação.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   

## <a name="remarks"></a>Comentários  
 **Sys. dm_tran_active_snapshot_database_transactions** relata as transações que recebem um XSN (número de sequência de transação). O XSN é atribuído quando a transação acessa o armazenamento de versões pela primeira vez. Em um banco de dados habilitado para isolamento de instantâneo ou isolamento confirmado por leitura utilizando controle de versão de linhas, os exemplos mostram quando um XSN é atribuído a uma transação:  
  
-   Se uma transação estiver executando em nível de isolamento de serializável, um XSN será atribuído quando a transação executar, pela primeira vez, uma instrução, como uma operação UPDATE, que cause a criação de uma versão de linha.  
  
-   Se uma transação estiver executando em isolamento de instantâneo, um XSN será atribuído quando alguma instrução de linguagem de manipulação de dados (DML), inclusive uma operação SELECT, for executada.  
  
 Números de sequência de transação são incrementados em série para cada transação iniciada em uma instância de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa um cenário de teste no qual quatro transações simultâneas, cada uma identificada por um XSN (número de sequência de transação), estão sendo executadas em um banco de dados no qual as opções ALLOW_SNAPSHOT_ISOLATION e READ_COMMITTED_SNAPSHOT estão definidas como ON. As seguintes transações estão sendo executadas:  
  
-   XSN-57 é uma operação de atualização sob o isolamento serializável.  
  
-   XSN-58 é o mesmo que XSN-57.  
  
-   XSN-59 é uma operação de seleção sob o isolamento de instantâneo  
  
-   XSN-60 é o mesmo que XSN-59.  
  
 A consulta a seguir é executada.  
  
```  
SELECT   
    transaction_id,  
    transaction_sequence_num,  
    commit_sequence_num,  
    is_snapshot session_id,  
    first_snapshot_sequence_num,  
    max_version_chain_traversed,  
    average_version_chain_traversed,  
    elapsed_time_seconds  
  FROM sys.dm_tran_active_snapshot_database_transactions;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
transaction_id  transaction_sequence_num  commit_sequence_num  
--------------  ------------------------  -------------------  
9295            57                        NULL  
9324            58                        NULL  
9387            59                        NULL  
9400            60                        NULL  
  
is_snapshot  session_id   first_snapshot_sequence_num  
-----------  -----------  ---------------------------  
0            54           0  
0            53           0  
1            52           57  
1            51           57  
  
max_version_chain_traversed  average_version_chain_traversed  
---------------------------  -------------------------------  
0                            0  
0                            0  
1                            1  
1                            1  
  
elapsed_time_seconds  
--------------------  
419  
397  
359  
333  
```  
  
 As informações a seguir avaliam os resultados de **Sys. dm_tran_active_snapshot_database_transactions**:  
  
-   XSN-57: como essa transação não está sendo executada sob isolamento de instantâneo, o `is_snapshot` valor e `first_snapshot_sequence_num` é `0` . O `transaction_sequence_num` mostra que um número de sequência de transação foi atribuído a esta transação, pois uma ou ambas as opções de banco de dados ALLOW_SNAPSHOT_ISOLATION e READ_COMMITTED_SNAPSHOT são ON.  
  
-   XSN-58: Esta transação não está sendo executada em isolamento de instantâneo, aplicando-se as mesma informações do XSN-57.  
  
-   XSN-59: Esta é a primeira transação ativa que está sendo executada em isolamento de instantâneo. Esta transação lê dados confirmados antes de XSN-57, como indicado por `first_snapshot_sequence_num`. A saída desta transação também mostra que a cadeia de versões máxima atravessada para uma linha é `1`, tendo atravessado uma média de `1` versão para cada linha que é acessada. Isso significa que as transações XSN-57, XSN-58 e XSN-60 não modificaram filas e foram confirmadas.  
  
-   XSN-60: Esta é a segunda transação que está sendo executada em isolamento de instantâneo. A saída mostra as mesmas informações de XSN-59.  
  
## <a name="see-also"></a>Consulte Também  
 [DEFINIR o nível de isolamento da transação &#40;&#41;Transact-SQL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à transação &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


