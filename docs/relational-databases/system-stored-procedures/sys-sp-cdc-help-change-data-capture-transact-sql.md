---
title: sys. sp_cdc_help_change_data_capture (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_help_change_data_capture_TSQL
- sys.sp_cdc_help_change_data_capture_TSQL
- sp_cdc_help_change_data_capture
- sys.sp_cdc_help_change_data_capture
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], querying metadata
- sys.sp_cdc_help_change_data_capture
- sp_cdc_help_change_data_capture
ms.assetid: 91fd41f5-1b4d-44fe-a3b5-b73eff65a534
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7935bc8e0472b90d22a93190f5af81c8e5910e67
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891092"
---
# <a name="syssp_cdc_help_change_data_capture-transact-sql"></a>sys.sp_cdc_help_change_data_capture (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna a configuração de captura dos dados de alteração para cada tabela habilitada para a captura de dados de alteração no banco de dados atual. Podem ser retornadas até duas linhas para cada tabela de origem, uma linha para cada instância de captura. A captura de dados de alteração não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_cdc_help_change_data_capture   
  [ [ @source_schema = ] 'source_schema' ]  
  [, [ @source_name = ] 'source_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @source_schema =] '*source_schema*'  
 É o nome do esquema ao qual a tabela de origem pertence. *source_schema* é **sysname**, com um padrão de NULL. Quando *source_schema* é especificado, *source_name* também deve ser especificado.  
  
 Se não for nulo, *source_schema* deverá existir no banco de dados atual.  
  
 Se *source_schema* não for null, *source_name* também deverá ser não nulo.  
  
 [ @source_name =] '*source_name*'  
 É o nome da tabela de origem. *source_name* é **sysname**, com um padrão de NULL. Quando *source_name* é especificado, *source_schema* também deve ser especificado.  
  
 Se não for nulo, *source_name* deverá existir no banco de dados atual.  
  
 Se *source_name* não for null, *source_schema* também deverá ser não nulo.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|Nome do esquema de tabela de origem.|  
|source_table|**sysname**|Nome da tabela de origem.|  
|capture_instance|**sysname**|Nome da instância de captura.|  
|object_id|**int**|ID da tabela de alteração associada à tabela de origem.|  
|source_object_id|**int**|ID da tabela de origem.|  
|start_lsn|**binary(10)**|LSN (Número de Sequência de Log) representando o ponto de extremidade inferior para consulta da tabela de alteração.<br /><br /> NULL = o ponto de extremidade inferior não foi definido.|  
|end_lsn|**binary(10)**|LSN representando o ponto de extremidade superior para consulta da tabela de alteração. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], esta coluna é sempre NULL.|  
|supports_net_changes|**bit**|O suporte à alteração de rede está habilitado.|  
|has_drop_pending|**bit**|Não é usado no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].|  
|role_name|**sysname**|Nome da função de banco de dados usada para controlar o acesso aos dados de alteração.<br /><br /> NULL = uma função não é usada.|  
|index_name|**sysname**|Nome do índice usado para identificar exclusivamente linhas na tabela de origem.|  
|filegroup_name|**sysname**|Nome do grupo de arquivos no qual a tabela de alteração reside.<br /><br /> NULL = tabela de alteração no grupo de arquivos padrão do banco de dados|  
|create_date|**datetime**|Data em que a instância de captura foi habilitada.|  
|index_column_list|**nvarchar(max)**|Lista de colunas de índice usadas para identificar exclusivamente linhas na tabela de origem.|  
|captured_column_list|**nvarchar(max)**|Lista de colunas de origem capturadas.|  
  
## <a name="remarks"></a>Comentários  
 Quando ambos *source_schema* e *source_name* são padrão como nulos ou são explicitamente definidos como NULL, esse procedimento armazenado retorna informações para todas as instâncias de captura de banco de dados às quais o chamador selecionou acesso. Quando *source_schema* e *SOURCE_NAME* são não nulos, apenas as informações sobre a tabela específica com o nome habilitado são retornadas.  
  
## <a name="permissions"></a>Permissões  
 Quando *source_schema* e *source_name* são nulas, a autorização do chamador determina quais tabelas habilitadas são incluídas no conjunto de resultados. Os chamadores devem ter a permissão SELECT em todas as colunas capturadas da instância de captura e também a associação em todas as funções associadas definidas para as informações sobre a tabela a serem incluídas. Os membros da função de banco de dados db_owner podem exibir informações sobre todas as instâncias de captura definidas. Quando informações para uma tabela habilitada específica são solicitadas, os mesmos critérios de associação e de SELECT são aplicados para a tabela nomeada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-change-data-capture-configuration-information-for-a-specified-table"></a>a. Retornando informações de configuração da captura de dados de alteração de uma tabela específica  
 O exemplo a seguir retorna a configuração da captura de dados de alteração da tabela `HumanResources.Employee`.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_help_change_data_capture   
    @source_schema = N'HumanResources',   
    @source_name = N'Employee';  
GO  
```  
  
### <a name="b-returning-change-data-capture-configuration-information-for-all-tables"></a>B. Retornando informações de configuração da captura de dados de alteração de todas as tabelas  
 O exemplo a seguir retorna informações de configuração de todas as tabelas habilitadas no banco de dados que contêm dados de alteração que o chamador está autorizado a acessar.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_help_change_data_capture;  
GO  
```  
  
  
