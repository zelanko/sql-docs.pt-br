---
title: ALTER DATABASE (Banco de Dados SQL do Azure) | Microsoft Docs
ms.custom: ''
ms.date: 02/13/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: t-sql|statements
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6fc5fd95-2045-4f20-a914-3598091bc7cc
caps.latest.revision: 37
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: c7d3f93304f08cbbf316e092b62ed7c4b62e199d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="alter-database-azure-sql-database"></a>ALTER DATABASE (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Modifica um [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Altera o nome de um banco de dados, a edição e o objetivo de serviço de um banco de dados, une a um pool elástico e define as opções do banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Azure SQL Database Syntax  
ALTER DATABASE { database_name }  
{  
    MODIFY NAME = new_database_name  
  | MODIFY ( <edition_options> [, ... n] ) 
  | SET { <option_spec> [ ,... n ] } 
  | ADD SECONDARY ON SERVER <partner_server_name>  
    [WITH ( <add-secondary-option>::= [, ... n] ) ]  
  | REMOVE SECONDARY ON SERVER <partner_server_name>  
  | FAILOVER  
  | FORCE_FAILOVER_ALLOW_DATA_LOSS  
}  
[;] 

<edition_options> ::= 
{  

  MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 … 1024 … 4096 GB }  
  | EDITION = { 'basic' | 'standard' | 'premium' | 'GeneralPurpose' | 'BusinessCritical'} 
  | SERVICE_OBJECTIVE = 
       {  <service-objective>
       | { ELASTIC_POOL (name = <elastic_pool_name>) } 
       } 
}  

<add-secondary-option> ::=  
   {  
      ALLOW_CONNECTIONS = { ALL | NO }  
     | SERVICE_OBJECTIVE = 
       {  <service-objective> 
       | { ELASTIC_POOL ( name = <elastic_pool_name>) } 
       } 
   }  

<service-objective> ::=  { 'S0' | 'S1' | 'S2' | 'S3'| 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |
       | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'
      | 'GP_GEN4_1' | 'GP_GEN4_2' | 'GP_GEN4_4' | 'GP_GEN4_8' | 'GP_GEN4_16' 
      | 'BC_GEN4_1' | 'BC_GEN4_2' | 'BC_GEN4_4' | 'BC_GEN4_8' | 'BC_GEN4_16' | 
      }

```  
  
```
-- SET OPTIONS AVAILABLE FOR SQL Database  
-- Full descriptions of the set options are available in the topic 
-- ALTER DATABASE SET Options. The supported syntax is listed here.  

<option_spec> ::= 
{  
    <auto_option> 
  | <change_tracking_option> 
  | <cursor_option> 
  | <db_encryption_option>  
  | <db_update_option> 
  | <db_user_access_option> 
  | <delayed_durability_option>  
  | <parameterization_option>  
  | <query_store_options>  
  | <snapshot_option>  
  | <sql_option> 
  | <target_recovery_time_option> 
  | <termination>  
  | <temporal_history_retention>  
}  
  
<auto_option> ::= 
{  
    AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] } 
  | AUTO_SHRINK { ON | OFF } 
  | AUTO_UPDATE_STATISTICS { ON | OFF } 
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
}  

<change_tracking_option> ::=  
{  
  CHANGE_TRACKING 
   { 
       = OFF  
     | = ON [ ( <change_tracking_option_list > [,...n] ) ] 
     | ( <change_tracking_option_list> [,...n] )  
   }  
}  

   <change_tracking_option_list> ::=  
   {  
       AUTO_CLEANUP = { ON | OFF } 
     | CHANGE_RETENTION = retention_period { DAYS | HOURS | MINUTES }  
   }  

<cursor_option> ::= 
{  
    CURSOR_CLOSE_ON_COMMIT { ON | OFF } 
}  
  
<db_encryption_option> ::=  
  ENCRYPTION { ON | OFF }  
  
<db_update_option> ::=  
  { READ_ONLY | READ_WRITE }  
  
<db_user_access_option> ::=  
  { RESTRICTED_USER | MULTI_USER }  
  
<delayed_durability_option> ::=  DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }  
  
<parameterization_option> ::=  
  PARAMETERIZATION { SIMPLE | FORCED }  
  
<query_store_options> ::=  
{  
  QUERY_STORE 
  {  
    = OFF 
    | = ON [ ( <query_store_option_list> [,... n] ) ]  
    | ( < query_store_option_list> [,... n] )  
    | CLEAR [ ALL ]  
  }  
} 
  
<query_store_option_list> ::=  
{  
  OPERATION_MODE = { READ_WRITE | READ_ONLY } 
  | CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = number )  
  | DATA_FLUSH_INTERVAL_SECONDS = number 
  | MAX_STORAGE_SIZE_MB = number 
  | INTERVAL_LENGTH_MINUTES = number 
  | SIZE_BASED_CLEANUP_MODE = [ AUTO | OFF ]  
  | QUERY_CAPTURE_MODE = [ ALL | AUTO | NONE ]  
  | MAX_PLANS_PER_QUERY = number  
}  
  
<snapshot_option> ::=  
{  
    ALLOW_SNAPSHOT_ISOLATION { ON | OFF }  
  | READ_COMMITTED_SNAPSHOT {ON | OFF }  
  | MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT {ON | OFF }  
}  
<sql_option> ::= 
{  
    ANSI_NULL_DEFAULT { ON | OFF }   
  | ANSI_NULLS { ON | OFF }   
  | ANSI_PADDING { ON | OFF }   
  | ANSI_WARNINGS { ON | OFF }   
  | ARITHABORT { ON | OFF }   
  | COMPATIBILITY_LEVEL = { 100 | 110 | 120 | 130 | 140 }  
  | CONCAT_NULL_YIELDS_NULL { ON | OFF }   
  | NUMERIC_ROUNDABORT { ON | OFF }   
  | QUOTED_IDENTIFIER { ON | OFF }   
  | RECURSIVE_TRIGGERS { ON | OFF }   
}  
  
<termination>  ::=   
{  
    ROLLBACK AFTER integer [ SECONDS ]   
  | ROLLBACK IMMEDIATE   
  | NO_WAIT  
}  

<temporal_history_retention>  ::=  TEMPORAL_HISTORY_RETENTION { ON | OFF }
```  
  
 Para obter descrições completas das opções set, confira [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) e [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="arguments"></a>Argumentos  

*database_name*  

É o nome do banco de dados a ser modificado.  
  
CURRENT  

Designa que o banco de dados em uso deve ser alterado.  
  
MODIFY NAME **=***new_database_name*  

Renomeia o banco de dados com o nome especificado como *novo_nome_do_banco_de_dados*. O exemplo a seguir altera o nome de um banco de dados `db1` para `db2`:   

```  
ALTER DATABASE db1  
    MODIFY Name = db2 ;  
```    

MODIFY (EDITION **=** ['basic' | 'standard' | 'premium' |'GeneralPurpose' | 'BusinessCritical'])    

Altera a camada de serviço do banco de dados. O suporte para 'premiumrs' foi removido. Em caso de dúvidas, use este alias de email: premium-rs@microsoft.com.

O exemplo a seguir altera a edição para `premium`:
  
```  
ALTER DATABASE current 
    MODIFY (EDITION = 'premium');
``` 

A alteração da edição falhará se a propriedade MAXSIZE do banco de dados estiver definida como um valor fora do intervalo válido compatível com essa edição.  

MODIFY (MAXSIZE **=** [100 MB | 500 MB | 1 | 1024…4096] GB)  

Especifica o tamanho máximo do banco de dados. O tamanho máximo deve estar em conformidade com o conjunto válido de valores da propriedade EDITION do banco de dados. A alteração do tamanho máximo do banco de dados pode fazer com que a EDIÇÃO do banco de dados seja alterada. A tabela a seguir lista os valores MAXSIZE com suporte e os padrões (D) para as camadas de serviço do [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
**Modelo com base em DTU**

|**MAXSIZE**|**Basic**|**S0-S2**|**S3-S12**|**P1-P6**|**P11-P15**|  
|-----------------|---------------|------------------|-----------------|-----------------|-----------------|-----------------|  
|100 MB|√|√|√|√|√|  
|250 MB|√|√|√|√|√|  
|500 MB|√|√|√|√|√|  
|1 GB|√|√|√|√|√|  
|2 GB|√ (D)|√|√|√|√|  
|5 GB|N/A|√|√|√|√|  
|10 GB|N/A|√|√|√|√|  
|20 GB|N/A|√|√|√|√|  
|30 GB|N/A|√|√|√|√|  
|40 GB|N/A|√|√|√|√|  
|50 GB|N/A|√|√|√|√|  
|100 GB|N/A|√|√|√|√|  
|150 GB|N/A|√|√|√|√|  
|200 GB|N/A|√|√|√|√|  
|250 GB|N/A|√ (D)|√ (D)|√|√|  
|300 GB|N/A|√|√|√|√|  
|400 GB|N/A|√|√|√|√|  
|500 GB|N/A|√|√|√ (D)|√|  
|750 GB|N/A|√|√|√|√|  
|1024 GB|N/A|√|√|√|√ (D)|  
|De 1024 GB até 4096 GB em incrementos de 256 GB*|N/A|N/A|N/A|N/A|√|√|  
  
\* P11 e P15 permitem MAXSIZE até 4 TB com 1024 GB sendo o tamanho padrão.  P11 e P15 podem usar até 4 TB de armazenamento incluído sem custos adicionais. Na camada Premium, MAXSIZE maior do que 1 TB está disponível no momento nas seguintes regiões: Leste dos EUA2, Oeste dos EUA, Gov. EUA – Virgínia, Europa Ocidental, Alemanha Central, Sudeste Asiático, Leste do Japão, Leste da Austrália, Canadá Central e Leste do Canadá. Para obter detalhes adicionais sobre limitações de recursos para o modelo com base em DTU, veja [Limites de recurso baseado em DTU](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits).  

O valor MAXSIZE do modelo baseado em DTU, se especificado, deve ser um valor válido exibido na tabela acima para a camada de serviço especificada.
 
**Modelo com base em vCore**

**Camada de serviço de Uso Geral**

|MAXSIZE|GP_Gen4_1|GP_Gen4_2|GP_Gen4_4|GP_Gen4_8|GP_Gen4_16|
|:--- | --: |--: |--: |--: |--: |
|Tamanho máximo de dados (GB)|1024|1024|1536|3072|4096|

**Camada de serviços Comercialmente Críticos**

|Nível de desempenho|BC_Gen4_1|BC_Gen4_2|BC_Gen4_4|BC_Gen4_8|BC_Gen4_16|
|:--- | --: |--: |--: |--: |--: |
|Tamanho máximo de dados (GB)|1024|1024|1536|2048|2048|

Se nenhum `MAXSIZE`valor for definido ao usar o modelo vCore, o padrão será de 32 GB. Para obter detalhes adicionais sobre limitações de recursos para o modelo com base em vCore, veja [Limites de recurso baseado em vCore](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits).
  
As regras a seguir se aplicam aos argumentos MAXSIZE e EDITION:  
  
- Se EDITION for especificado, mas MAXSIZE não for especificado, o valor padrão da edição será usado. Por exemplo, se EDITION for definido como Standard e MAXSIZE não for especificado, MAXSIZE será automaticamente definido como 500 MB.  
  
- Se nem MAXSIZE nem EDITION forem especificados, EDITION será definido como Standard (S0) e MAXZISE será definido como 250 GB.  

MODIFY (SERVICE_OBJECTIVE = \<service-objective>)  

Especifica o nível de desempenho. A exemplo a seguir altera o objetivo de serviço de um banco de dados Premium para `P6`:
 
```sql  
ALTER DATABASE current 
    MODIFY (SERVICE_OBJECTIVE = 'P6');
```  

Especifica o nível de desempenho. Os valores disponíveis para o objetivo de serviço são: `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_4`, `GP_GEN4_8`, `GP_GEN4_16`, `BC_GEN4_1` `BC_GEN4_2` `BC_GEN4_4` `BC_GEN4_8` `BC_GEN4_16`. 

Para obter descrições de objetivos de serviço e mais informações sobre o tamanho, as edições e as combinações de objetivo de serviço, veja [Camadas de serviço e níveis de desempenho do Banco de Dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/), [Limites de recurso baseado em DTU](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) e [Limites de recurso baseado em vCore](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits). O suporte para objetivos de serviço PRS foi removido. Em caso de dúvidas, use este alias de email: premium-rs@microsoft.com. 
  
MODIFY (SERVICE_OBJECTIVE = ELASTIC\_POOL (name = \<elastic_pool_name>)  

Para adicionar um banco de dados existente a um pool elástico, defina o SERVICE_OBJECTIVE do banco de dados como ELASTIC_POOL e forneça o nome do pool elástico. Você também pode usar esta opção para alterar o banco de dados para um pool elástico diferente no mesmo servidor. Para obter mais informações, confira [Criar e gerenciar um pool elástico do Banco de Dados SQL](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/). Para remover um banco de dados de um pool elástico, use ALTER DATABASE para definir o SERVICE_OBJECTIVE para um único nível de desempenho do banco de dados.  

ADD SECONDARY ON SERVER \<partner_server_name>  

Cria um banco de dados de replicação geográfica secundário com o mesmo nome em um servidor parceiro, tornando o banco de dados local o primário da replicação geográfica e começa a replicação de dados assíncrona do primário para o novo secundário. Se um banco de dados com o mesmo nome já existir no secundário, o comando falhará. O comando é executado no banco de dados mestre no servidor que hospeda o banco de dados local que se torna o primário.  
  
WITH ALLOW_CONNECTIONS { **ALL** | NO }  

Quando ALLOW_CONNECTIONS não for especificado, ele será definido como ALL por padrão. Se estiver definido como ALL, ele será um banco de dados somente leitura que permite que todos os logons com as permissões apropriadas se conectem.  
  
WITH SERVICE_OBJECTIVE {  `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_4`, `GP_GEN4_8`, `GP_GEN4_16`, `BC_GEN4_1` `BC_GEN4_2` `BC_GEN4_4` `BC_GEN4_8` `BC_GEN4_16` }  

Quando SERVICE_OBJECTIVE não for especificado, o banco de dados secundário será criado no mesmo nível de serviço que o banco de dados primário. Quando SERVICE_OBJECTIVE for especificado, o banco de dados secundário será criado no nível especificado. Essa opção permite a criação de secundários replicados geograficamente com níveis de serviço mais baratos. O SERVICE_OBJECTIVE especificado precisa estar na mesma edição que a origem. Por exemplo, não é possível especificar S0 se a edição for Premium.  
  
ELASTIC_POOL (name = \<elastic_pool_name)  

Quando ELASTIC_POOL não for especificado, o banco de dados secundário não será criado em um pool elástico. Quando ELASTIC_POOL for especificado, o banco de dados secundário será criado no pool especificado.  
  
> [!IMPORTANT]  
>  O usuário que executa o comando ADD SECONDARY precisa ser DBManager no servidor primário, ter associação a db_owner no banco de dados local e DBManager no servidor secundário.  
  
REMOVE SECONDARY ON SERVER \<partner_server_name>  

Remove o banco de dados secundário replicado geograficamente especificado no servidor indicado. O comando é executado no banco de dados mestre no servidor que hospeda o banco de dados primário.  
  
> [!IMPORTANT]  
>  O usuário que executa o comando REMOVE SECONDARY precisa ser DBManager no servidor primário.  
  
FAILOVER  

Promove o banco de dados secundário na parceria de replicação geográfica na qual o comando é executado para tornar-se o primário e rebaixa o primário atual para tornar-se o novo secundário. Como parte desse processo, o modo de replicação geográfica é temporariamente alternado de modo assíncrono para modo síncrono. Durante o processo de failover:  
  
1.  O primário deixa de assumir novas transações.  
  
2.  Todas as transações pendentes são liberadas para o secundário.  
  
3.  O secundário torna-se o primário e inicia a replicação geográfica assíncrona com o antigo primário que agora é o novo secundário.  
  
Esta sequência garante que não haja nenhuma perda de dados. O período durante o qual os dois bancos de dados não estão disponíveis é de 0 a 25 segundos, enquanto as funções são trocadas. A operação total não deve durar mais que cerca de um minuto. Se o banco de dados primário estiver indisponível quando esse comando for emitido, o comando falhará com uma mensagem de erro indicando que o banco de dados primário não está disponível. Se o processo de failover não for concluído e parecer paralisado, você poderá usar o comando para forçar o failover e aceitar a perda de dados. Em seguida, se for necessário recuperar os dados perdidos, chame DevOps (CSS).  
  
> [!IMPORTANT]  
>  O usuário que executa o comando FAILOVER precisa ser DBManager no servidor primário e no servidor secundário.  
  
FORCE_FAILOVER_ALLOW_DATA_LOSS  

Promove o banco de dados secundário na parceria de replicação geográfica na qual o comando é executado para tornar-se o primário e rebaixa o primário atual para tornar-se o novo secundário. Use este comando somente quando o primário atual não estiver mais disponível. Ele foi projetado somente para recuperação de desastre, quando a restauração da disponibilidade é crítica e a perda de alguns dados é aceitável.  
  
Durante um failover forçado:  
  
1. O banco de dados secundário especificado torna-se imediatamente o banco de dados primário e começa a aceitar novas transações.  
  
2. Quando o primário original pode se reconectar com o novo primário, um backup incremental é realizado no primário original e ele se torna o novo secundário.  
  
3. Para recuperar dados desse backup incremental no antigo primário, o usuário emprega DevOps/CSS.  
  
4. Se houver outros secundários, eles serão reconfigurados automaticamente para tornarem-se secundários do novo primário. Esse processo é assíncrono e pode haver um atraso até que ele seja concluído. Até que a reconfiguração seja concluída, os secundários continuarão como secundários do antigo primário.  
  
> [!IMPORTANT]  
>  O usuário que executa o comando FORCE_FAILOVER_ALLOW_DATA_LOSS precisa ser DBManager no servidor primário e no servidor secundário.  
  
## <a name="remarks"></a>Remarks  

Para remover um banco de dados, use [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md).  
Para diminuir o tamanho de um banco de dados, use [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
A instrução ALTER DATABASE deve ser executada em modo de confirmação automática (o modo padrão de administração de transações) e não deve ser permitida em uma transação explícita ou implícita.  
  
A limpeza do cache de planos gera uma recompilação de todos os planos de execução subsequentes e pode provocar uma redução repentina e temporária do desempenho de consultas. Para cada armazenamento em cache limpo no cache de planos, o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém a seguinte mensagem informativa: "O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou %d ocorrência(s) de liberação de armazenamento em cache '% s' (parte do cache de planos) devido à manutenção do banco de dados ou operações de reconfiguração". Essa mensagem é registrada a cada cinco minutos, contanto que o cache seja liberado dentro desse intervalo de tempo.  
  
O cache de procedimento também é liberado nos seguintes cenários:  
  
- Um banco de dados tem a opção de banco de dados AUTO_CLOSE definida como ON. Quando nenhuma conexão de usuário fizer referência ou usar o banco de dados, a tarefa de banco de dados tentará fechar e encerrar o banco de dados automaticamente.  
  
- Execute diversas consultas em um banco de dados que tem opções padrão. O banco de dados é removido.  
  
- Você recria com sucesso o log de transação para um banco de dados.  
  
- Você restaura um backup de banco de dados.  
  
- Você desanexa um banco de dados.  
  
## <a name="viewing-database-information"></a>Exibindo informações do banco de dados  

É possível usar exibições do catálogo, funções do sistema e procedimentos armazenados do sistema para retornar informações sobre bancos de dados, arquivos e grupos de arquivos.  
  
## <a name="permissions"></a>Permissões  

Somente o logon de entidade de segurança no nível do servidor (criado pelo processo de provisionamento) ou os membros da função de banco de dados `dbmanager` podem alterar um banco de dados.  
  
> [!IMPORTANT]  
>  O proprietário do banco de dados não pode alterar o banco de dados, a menos que seja um membro da função `dbmanager`.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-check-the-edition-options-and-change-them"></a>A. Verifique as opções de edição e altere-as:

```sql
SELECT Edition = DATABASEPROPERTYEX('db1', 'EDITION'),
        ServiceObjective = DATABASEPROPERTYEX('db1', 'ServiceObjective'),
        MaxSizeInBytes =  DATABASEPROPERTYEX('db1', 'MaxSizeInBytes');

ALTER DATABASE [db1] MODIFY (EDITION = 'Premium', MAXSIZE = 1024 GB, SERVICE_OBJECTIVE = 'P15');
```

### <a name="b-moving-a-database-to-a-different-elastic-pool"></a>B. Movendo um banco de dados para um pool elástico diferente  

Move um banco de dados existente para um pool chamado pool1:  
  
```sql  
ALTER DATABASE db1   
MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = pool1 ) ) ;  
```  
  
### <a name="c-add-a-geo-replication-secondary"></a>C. Adicionar um secundário de replicação geográfica  

Cria o banco de dados secundário legível db1 no servidor `secondaryserver` do db1 no servidor local.  
  
```sql  
ALTER DATABASE db1   
ADD SECONDARY ON SERVER secondaryserver   
WITH ( ALLOW_CONNECTIONS = ALL )  
```  
  
### <a name="d-remove-a-geo-replication-secondary"></a>D. Remover um secundário de replicação geográfica  
 
Remove o banco de dados secundário db1 do servidor `secondaryserver`.  
  
```sql  
ALTER DATABASE db1   
REMOVE SECONDARY ON SERVER testsecondaryserver   
```  
  
### <a name="e-failover-to-a-geo-replication-secondary"></a>E. Failover para um secundário de replicação geográfica  

Promove o banco de dados secundário db1 no servidor `secondaryserver` para tornar-se o novo banco de dados primário quando executado no servidor `secondaryserver`.  
  
```sql  
ALTER DATABASE db1 FAILOVER  
```  
  
## <a name="see-also"></a>Confira também
  
[CREATE DATABASE – Banco de Dados SQL do Azure](../../t-sql/statements/create-database-azure-sql-database.md)   
 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Bancos de dados do sistema](../../relational-databases/databases/system-databases.md)  
  
  
