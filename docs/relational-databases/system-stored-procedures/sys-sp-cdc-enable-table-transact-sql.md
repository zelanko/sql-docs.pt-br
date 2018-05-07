---
title: sp_cdc_enable_table (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_enable_table_TSQL
- sp_cdc_enable_table_TSQL
- sys.sp_cdc_enable_table
- sp_cdc_enable_table
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], enabling tables
- sys.sp_cdc_enable_table
- sp_cdc_enable_table
ms.assetid: 26150c09-2dca-46ad-bb01-3cb3165bcc5d
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 0ed70b21e667a1738433335e3e3c869c3b410523
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysspcdcenabletable-transact-sql"></a>sys.sp_cdc_enable_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Habilita o Change Data Capture para a tabela de origem especificada no banco de dados atual. Quando uma tabela está habilitada para Change Data Capture, um registro de cada operação DML (Linguagem de Manipulação de Dados) aplicado à tabela é gravado no log de transações. O processo do Change Data Capture recupera essas informações a partir do log e grava-as nas tabelas de alteração que são acessadas usando um conjunto de funções.  
  
 A captura de dados de alteração não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_cdc_enable_table   
  [ @source_schema = ] 'source_schema',   
  [ @source_name = ] 'source_name' ,  [,[ @capture_instance = ] 'capture_instance' ]  
  [,[ @supports_net_changes = ] supports_net_changes ]  
  , [ @role_name = ] 'role_name'  
  [,[ @index_name = ] 'index_name' ]  
  [,[ @captured_column_list = ] 'captured_column_list' ]  
  [,[ @filegroup_name = ] 'filegroup_name' ]  
  [,[ @allow_partition_switch = ] 'allow_partition_switch' ]  
  [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@source_schema =** ] **'***source_schema***'**  
 É o nome do esquema ao qual a tabela de origem pertence. *source_schema* é **sysname**, sem padrão, e não pode ser NULL.  
  
 [  **@source_name =** ] **'***source_name***'**  
 É o nome da tabela de origem na qual habilitar a captura de dados de alteração. *source_name* é **sysname**, sem padrão, e não pode ser NULL.  
  
 *source_name* deve existir no banco de dados atual. Tabelas de **cdc** esquema não pode ser habilitado para change data capture.  
  
 [  **@role_name =** ] **'***nome_da_função***'**  
 É o nome da função de banco de dados usada como acesso aos dados de alteração. *nome_da_função* é **sysname** e deve ser especificado. Se explicitamente definido como NULL, nenhuma função associada será usada para limitar o acesso aos dados de alteração.  
  
 Se a função existir atualmente, ela será usada. Se a função não existir, será feita uma tentativa de criar uma função de banco de dados com o nome especificado. Os espaços em branco do nome da função à direita da cadeia de caracteres são eliminados antes de tentar criar a função. Se o chamador não for autorizado a criar uma função dentro do banco de dados, a operação de procedimento armazenado irá falhar.  
  
 [  **@capture_instance =** ] **'***capture_instance***'**  
 É o nome da instância de captura usada para nomear objetos do Change Data Capture específicos. *capture_instance* é **sysname** e não pode ser NULL.  
  
 Se não for especificado, o nome é derivado do nome de esquema de origem mais o nome da tabela de origem no formato *schemaname_sourcename*. *capture_instance* não pode exceder 100 caracteres e deve ser exclusivo no banco de dados. Se especificado ou derivado, *capture_instance* é cortados de qualquer espaço em branco à direita da cadeia de caracteres.  
  
 Uma tabela de origem pode ter um máximo de duas instâncias de captura. Para obter mais informações, consulte [sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md).  
  
 [  **@supports_net_changes =** ] *supports_net_changes*  
 Indica se o suporte à consulta de alterações líquidas será habilitado para esta instância de captura. *supports_net_changes* é **bit** com um padrão de 1, se a tabela tem uma chave primária ou a tabela tem um índice exclusivo identificado usando o @index_name parâmetro. Caso contrário, o parâmetro será padronizado como 0.  
  
 Se for 0, somente as funções de suporte à consulta de todas as alterações serão geradas.  
  
 Se for 1, as funções necessárias à consulta de alterações líquidas também serão geradas.  
  
 Se *supports_net_changes* é definido como 1, *index_name* devem ser especificados, ou a tabela de origem deve ter uma chave primária definida.  
  
 [  **@index_name =** ] **' * index_name*'  
 O nome de um índice exclusivo a ser usado para identificar exclusivamente as linhas na tabela de origem. *index_name* é **sysname** e pode ser NULL. Se especificado, *index_name* deve ser um índice exclusivo válido na tabela de origem. Se *index_name* for especificado, as colunas de índice identificadas tem precedência sobre quaisquer colunas de chave primária definidas como o identificador de linha exclusivo para a tabela.  
  
 [  **@captured_column_list =** ] **'***captured_column_list***'**  
 Identifica as colunas da tabela de origem a serem incluídas na tabela de alteração. *captured_column_list* é **nvarchar (max)** e pode ser NULL. Se for NULL, todas as colunas serão incluídas na tabela de alteração.  
  
 Nomes de Coluna devem ser colunas válidas na tabela de origem. Colunas definidas em um índice de chave primária ou colunas definidas em um índice referenciado por *index_name* devem ser incluídos.  
  
 *captured_column_list* é uma lista separada por vírgulas de nomes de coluna. Nomes de colunas individuais na lista podem ser citados opcionalmente usando aspas duplas ("") ou colchetes ([]). Se um nome de coluna contiver uma vírgula inserida, o nome de coluna deve ser citado.  
  
 *captured_column_list* não pode conter os seguintes nomes de coluna reservados: **_ $start_lsn**, **_ $end_lsn**, **_ $seqval**, **_ $ operação**, e **_ $update_mask**.  
  
 [  **@filegroup_name =** ] **'***filegroup_name***'**  
 É o grupo de arquivos a ser usado para a tabela de alteração criada para a instância de captura. *filegroup_name* é **sysname** e pode ser NULL. Se especificado, *filegroup_name* deve ser definida para o banco de dados atual. Se for NULL, o grupo de arquivos padrão será usado.  
  
 Recomendamos a criação de um grupo de arquivos separado para tabelas de alteração do Change Data Capture.  
  
 [  **@allow_partition_switch=** ] **'***allow_partition_switch***'**  
 Indica se o comando SWITCH PARTITION de ALTER TABLE pode ser executado em uma tabela que está habilitada para o Change Data Capture. *allow_partition_switch* é **bit**, com um padrão de 1.  
  
 Para tabelas não particionadas, a configuração de alternância é sempre 1 e a configuração real é ignorada. Se a alternância estiver explicitamente definida como 0 para uma tabela não particionada, o aviso 22857 será emitido para indicar que a configuração de alternância foi ignorada. Se a alternância estiver explicitamente definida como 0 para uma tabela particionada, o aviso 22356 será emitido para indicar que as operações de alternância da partição na tabela de origem não serão permitidas. Finalmente, se a configuração de alternância estiver explicitamente definida como 1 ou permitida para ser padronizada como 1 e a tabela habilitada estiver particionada, o aviso 22855 será emitido para indicar que as alternâncias de partição não serão bloqueadas. Se ocorrer qualquer alternância de partição, o Change Data Capture não controlará as alterações resultantes da alternância. Isso provocará inconsistências de dados quando os dados de alteração forem consumidos.  
  
> [!IMPORTANT]  
>  SWITCH PARTITION é uma operação de metadados, mas provoca alterações nos dados. As alterações de dados associadas a essa operação não são capturadas nas tabelas de alteração do Change Data Capture. Considere uma tabela com três partições em que são feitas alterações. O processo de captura rastreará operações de inserção, atualização e exclusão de usuário que são executadas na tabela. Entretanto, se uma partição for alternada para outra tabela (por exemplo, para executar uma exclusão em massa), as linhas movidas como parte dessa operação não serão capturadas como linhas excluídas na tabela de alteração. Da mesma forma, se uma nova partição com linhas previamente populadas for adicionada à tabela, essas linhas não constarão na tabela de alteração. Isso pode causar inconsistência de dados quando as alterações forem consumidas por um aplicativo e aplicadas a um destino.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 Antes de habilitar uma tabela para Change Data Capture, o banco de dados deve estar habilitado. Para determinar se o banco de dados está habilitado para change data capture, consulte o **is_cdc_enabled** coluna o [sys. Databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) exibição do catálogo. Para habilitar o banco de dados, use o [sp_cdc_enable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md) procedimento armazenado.  
  
 Quando o Change Data Capture está habilitado para uma tabela, uma tabela de alteração e uma ou duas funções de consulta são geradas. A tabela de alteração serve como um repositório para as alterações da tabela de origem extraídas do log de transações pelo processo de captura. As funções de consulta são usadas para extrair dados da tabela de alteração. Os nomes dessas funções são derivados do *capture_instance* parâmetro das seguintes maneiras:  
  
-   Função de todas as alterações: **CDC. fn_cdc_get_all_changes_ < instância_de_captura >**  
  
-   Função de alterações líquidas: **CDC. fn_cdc_get_net_changes_ < capture_instance >**  
  
 **sp_cdc_enable_table** também cria os trabalhos de captura e limpeza do banco de dados se a tabela de origem é a primeira tabela no banco de dados a ser habilitada para change data capture e nenhuma publicação transacional existir para o banco de dados. Ele define o **is_tracked_by_cdc** coluna o [sys. Tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) exibição 1 do catálogo.  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não precisa estar em execução quando o Change Data Capture estiver habilitado para uma tabela. No entanto o processo de captura não processará o log de transações e não gravará as entradas na tabela de alteração, a não ser que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent esteja em execução.  
  
## <a name="permissions"></a>Permissões  
 Requer a participação no **db_owner** função fixa de banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-enabling-change-data-capture-by-specifying-only-required-parameters"></a>A. Habilitando o Change Data Capture especificando somente os parâmetros necessários  
 O exemplo a seguir habilita o Change Data Capture na tabela `HumanResources.Employee`. Somente os parâmetros necessários são especificados.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_enable_table  
    @source_schema = N'HumanResources'  
  , @source_name = N'Employee'  
  , @role_name = N'cdc_Admin';  
GO  
```  
  
### <a name="b-enabling-change-data-capture-by-specifying-additional-optional-parameters"></a>B. Habilitando o Change Data Capture especificando parâmetros opcionais adicionais  
 O exemplo a seguir habilita o Change Data Capture na tabela `HumanResources.Department`. Todos os parâmetros, exceto o `@allow_partition_switch` são especificados.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_enable_table  
    @source_schema = N'HumanResources'  
  , @source_name = N'Department'  
  , @role_name = N'cdc_admin'  
  , @capture_instance = N'HR_Department'   
  , @supports_net_changes = 1  
  , @index_name = N'AK_Department_Name'   
  , @captured_column_list = N'DepartmentID, Name, GroupName'   
  , @filegroup_name = N'PRIMARY';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_cdc_disable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-table-transact-sql.md)   
 [sys.sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [sp_cdc_help_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)  
  
  
