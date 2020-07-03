---
title: Core. sp_create_snapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_create_snapshot
- sp_create_snapshot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- management data warehouse, data collector stored procedures
- data collector [SQL Server], stored procedures
- core.sp_create_snapshot stored procedure
- sp_create_snapshot
ms.assetid: ff297bda-0ee2-4fda-91c8-7000377775e3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6b3ffe874615e58d276428548cb1c2ad318f111d
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898232"
---
# <a name="coresp_create_snapshot-transact-sql"></a>core.sp_create_snapshot (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Insere uma linha na exibição core.snapshots do data warehouse de gerenciamento. Esse procedimento é chamado sempre que um pacote de carregamento começa a carregar dados no data warehouse de gerenciamento.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
core.sp_create_snapshot [ @collection_set_uid = ] 'collection_set_uid'  
    , [ @collector_type_uid = ] 'collector_type_uid'  
    ,[ @machine_name = ] 'machine_name'  
    , [ @named_instance = ] 'named_instance'  
    , [ @log_id = ] log_id  
    , [ @snapshot_id = ] snapshot_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @collection_set_uid =] '*collection_set_uid*'  
 O GUID do conjunto de coleta. *collection_set_uid* é **uniqueidentifier** sem valor padrão. Para obter o GUID, consulte a exibição dbo.syscollector_collection_sets no banco de dados msdb.  
  
 [ @collector_type_uid =] '*collector_type_uid*'  
 O GUID de um tipo de coletor. *collector_type_uid* é **uniqueidentifier** sem valor padrão. Para obter o GUID, consulte a exibição dbo.syscollector_collector_types no banco de dados msdb.  
  
 [ @machine_name =] '*machine_name*'  
 O nome do servidor no qual o conjunto de coleta reside. *machine_name* é **sysname**, sem valor padrão.  
  
 [ @named_instance =] '*named_instance*'  
 O nome da instância do conjunto de coleta. *named_instance* é **sysname**, sem valor padrão.  
  
 [ @log_id =] *log_id*  
 O identificador exclusivo que é mapeado para o log de eventos do conjunto de coleta que coletou os dados. *log_id* é **bigint** sem valor padrão. Para obter o valor de *log_id*, consulte a exibição de collector_execution_log de dbo.sysno banco de dados msdb.  
  
 [ @snapshot_id =] *snapshot_id*  
 O identificador exclusivo de uma linha que é inserida na exibição core. Snapshots. *snapshot_id* é **int** e é retornada como saída.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Sempre que um pacote de carregamento começa a carregar dados no data warehouse de gerenciamento, o componente de tempo de execução do coletor de dados chama core.sp_create_snapshot.  
  
 Esse procedimento verifica se:  
  
-   O collection_set_uid corresponde a uma entrada existente na tabela core.source_info_internal.  
  
-   O collector_type_uid corresponde a uma entrada existente na exibição core.supported_collector_types.  
  
 Se alguma das verificações acima falhar, o procedimento falhará e retornará um erro.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa **mdw_writer** (com permissão de execução).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um instantâneo do conjunto de coleta Uso do Disco, adiciona-o ao data warehouse de gerenciamento e retorna o identificador do instantâneo. No exemplo, a instância padrão é usada.  
  
```  
USE <management_data_warehouse>;  
DECLARE @snapshot_id int;  
EXEC core.sp_create_snapshot   
    @collection_set_uid = '7B191952-8ECF-4E12-AEB2-EF646EF79FEF',   
    @collector_type_uid = '302E93D1-3424-4BE7-AA8E-84813ECF2419',  
    @machine_name = '<computername>',  
    @named_instance = 'MSSQLSERVER',  
    @log_id = 11, -- ID of the log for the collection set  
    @snapshot_id = @snapshot_id OUTPUT;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [data warehouse de gerenciamento](../../relational-databases/data-collection/management-data-warehouse.md)  
  
  
