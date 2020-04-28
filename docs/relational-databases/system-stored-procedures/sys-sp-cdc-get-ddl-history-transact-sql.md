---
title: sys. sp_cdc_get_ddl_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_get_ddl_history
- sp_cdc_get_ddl_history_TSQL
- sys.sp_cdc_get_ddl_history_TSQL
- sys.sp_cdc_get_ddl_history
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], querying metadata
- sp_cdc_get_ddl_history
- sys.sp_cdc_get_ddl_history
ms.assetid: 4dee5e2e-d7e5-4fea-8037-a4c05c969b3a
author: rothja
ms.author: jroth
ms.openlocfilehash: bb4622b36901afc7ff04eacbfe840a9adda5b214
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68083730"
---
# <a name="syssp_cdc_get_ddl_history-transact-sql"></a>sys.sp_cdc_get_ddl_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o histórico de alteração DDL (linguagem de definição de dados) associado à instância de captura especificada desde que Change Data Capture foi habilitado para aquela instância de captura. A captura de dados de alteração não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_cdc_get_ddl_history [ @capture_instance = ] 'capture_instance'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @capture_instance = ] '*capture_instance*'  
 É o nome da instância de captura associada à tabela de origem. *capture_instance* é **sysname** e não pode ser nulo.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|Nome do esquema de tabela de origem.|  
|source_table|**sysname**|Nome da tabela de origem.|  
|capture_instance|**sysname**|Nome da instância de captura.|  
|required_column_update|**bit**|Indica que a alteração de DDL requereu que uma coluna na tabela de alteração fosse alterada para refletir uma alteração de tipo de dados feita na coluna de origem.|  
|ddl_command|**nvarchar(max)**|A instrução DDL aplicada à tabela de origem.|  
|ddl_lsn|**binary(10)**|Número de sequência de log (LSN) associado com a alteração de DDL.|  
|ddl_time|**datetime**|Hora associada à alteração de DDL.|  
  
## <a name="remarks"></a>Comentários  
 As modificações de DDL na tabela de origem que alteram a estrutura de coluna da tabela de origem, como adicionar ou descartar uma coluna, ou alterar o tipo de dados de uma coluna existente, são mantidas na tabela [CDC. ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md) . Essas mudanças podem ser informadas usando este procedimento armazenado. Entradas em cdc.ddl_history são realizadas no momento em que o processo de captura lê a transação de DDL no log.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função de banco de dados fixa db_owner, para retornar linhas de todas as instâncias de captura no banco de dados. Para todos os outros usuários, requer a permissão SELECT em todas as colunas capturadas na tabela de origem e, se uma função associada para a instância de captura tiver sido definida, faça associação nessa função de banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir acrescenta uma coluna à tabela de origem `HumanResources.Employee` e, então, executa o procedimento armazenado `sys.sp_cdc_get_ddl_history`, para informar as alterações na DDL que se aplicam à tabela de origem associada à instância de captura `HumanResources_Employee`.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER TABLE HumanResources.Employee  
ADD Test_Column int NULL;  
GO  
-- Pause 10 seconds to allow the event to be logged.   
WAITFOR DELAY '00:00:10';  
GO   
EXECUTE sys.sp_cdc_get_ddl_history   
    @capture_instance = 'HumanResources_Employee';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys.sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
