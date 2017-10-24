---
title: ALTER DATABASE (banco de dados do SQL Azure) | Microsoft Docs
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 09/25/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6fc5fd95-2045-4f20-a914-3598091bc7cc
caps.latest.revision: 37
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: e3c781449a8f7a1b236508cd21b8c00ff175774f
ms.openlocfilehash: f525c0ca01f49be05c1920897951059b126c83e9
ms.contentlocale: pt-br
ms.lasthandoff: 09/30/2017

---
# <a name="alter-database-azure-sql-database"></a>ALTER DATABASE (banco de dados do SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Modifica um [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Altera o nome de um objetivo de banco de dados, a edição e o serviço de um banco de dados, um pool Elástico de junção e define opções de banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
    | EDITION = { 'basic' | 'standard' | 'premium' | 'premiumrs' }   
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
                 | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15' | 
                 | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' | }

```  
  
```
-- SET OPTIONS AVAILABLE FOR SQL Database  
-- Full descriptions of the set options are available in the topic   
-- ALTER DATABASE SET Options. The supported syntax is listed here.  

<optionspec> ::=   
{  
    <auto_option>   
  | <compatibility_level_option>  
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
  
<compatibility_level_option>::=  
COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 }  
  
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
  
<delayed_durability_option> ::=    DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }  
  
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
  | COMPATIBILITY_LEVEL = { 90 | 100 | 110 | 120}  
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
  
 Para obter descrições completas das opções set, consulte [opções ALTER DATABASE SET &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) e [alterar o nível de compatibilidade do banco de dados &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 É o nome do banco de dados a ser modificado.  
  
 CURRENT  
 Designa que o banco de dados em uso deve ser alterado.  
  
 MODIFY NAME  **=**  *new_database_name*  
 Renomeia o banco de dados com o nome especificado como *new_database_name*. O exemplo a seguir altera o nome de um banco de dados `db1` para `db2`:   

```  
ALTER DATABASE db1  
    MODIFY Name = db2 ;  
```    

 MODIFICAR (edição  **=**  ['basic' | 'padrão' | 'premium' | 'premiumrs']).    
 Altera a camada de serviço do banco de dados. O exemplo a seguir altera a edição para `premium`:
  
```  
ALTER DATABASE current 
    MODIFY (EDITION = 'premium');
``` 

A alteração da edição falhará se a propriedade MAXSIZE do banco de dados é definida como um valor fora do intervalo válido admitido por essa edição.  

 MODIFICAR (MAXSIZE  **=**  [100 MB | 500 MB | 1 | 1024... 4096] GB)  
 Especifica o tamanho máximo do banco de dados. O tamanho máximo deve estar em conformidade com o conjunto válido de valores da propriedade EDITION do banco de dados. A alteração do tamanho máximo do banco de dados pode fazer com que a EDIÇÃO do banco de dados seja alterada. A tabela a seguir lista os valores MAXSIZE com suporte e os padrões (D) para as camadas de serviço do [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
|**MAXSIZE**|**Basic**|**S2 S0**|**/S12 S3**|**P1 P6 e PRS1 PRS6**|**P11 P15**|  
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
|De 1024 GB até 4096 GB em incrementos de 256 GB *|N/A|N/A|N/A|N/A|√|√|  
  
 \*P11 e P15 permitem MAXSIZE até 4 TB com 1024 GB, sendo o tamanho padrão.  P11 e P15 podem usar até 4 TB de armazenamento incluído sem custos adicionais. Na camada Premium, MAXSIZE maior que 1 TB está atualmente disponível nas seguintes regiões: US East2, oeste dos EUA, nos Gov Virgínia, Europa Ocidental, Alemanha Central, Sul Leste da Ásia, Leste do Japão, Leste da Austrália, Canadá Central e Leste do Canadá. Para limitações atuais, consulte [único bancos de dados](https://docs.microsoft.com/azure/sql-database-single-database-resources).  

  
 As regras a seguir se aplicam aos argumentos MAXSIZE e EDITION:  
  
-   O valor MAXSIZE, se especificado, deve ser um valor válido, mostrado na tabela anterior.  
  
-   Se EDITION for especificado, mas MAXSIZE não for especificado, o valor padrão da edição será usado. Por exemplo, se EDITION for definido como Standard e MAXSIZE não for especificado, MAXSIZE será automaticamente definido como 500 MB.  
  
-   Se MAXSIZE nem EDITION for especificado, a edição é definida como padrão (S0) e MAXSIZE for definido como 250 GB.  
 

 MODIFICAR (SERVICE_OBJECTIVE = \<objetivo de serviço >)  
 Especifica o nível de desempenho. A exemplo a seguir altera o objetivo de um banco de dados premium do serviço `P6`:
 
```  
ALTER DATABASE current 
    MODIFY (SERVICE_OBJECTIVE = 'P6');
```  
 Os valores disponíveis para o objetivo de serviço são: `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `PRS1`, `PRS2`, `PRS4`, e `PRS6`. Para descrições de objetivo de serviço e obter mais informações sobre o tamanho, as edições e as combinações de objetivos de serviço, consulte [camadas de serviço de banco de dados SQL do Azure e níveis de desempenho](http://msdn.microsoft.com/library/azure/dn741336.aspx). Se o SERVICE_OBJECTIVE especificado não é suportada pela edição, você receberá um erro. Para alterar o valor SERVICE_OBJECTIVE de uma camada para outra (por exemplo, de S1 para P1), você deve alterar também o valor EDITION.  
  
 MODIFICAR (SERVICE_OBJECTIVE = ELÁSTICA\_POOL (nome = \<elastic_pool_name >)  
 Para adicionar um banco de dados existente para um pool Elástico, defina o SERVICE_OBJECTIVE do banco de dados como ELASTIC_POOL e forneça o nome do pool Elástico. Você também pode usar esta opção para alterar o banco de dados para um pool Elástico diferente no mesmo servidor. Para obter mais informações, consulte [criar e gerenciar um pool Elástico de banco de dados SQL](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/). Para remover um banco de dados de um pool Elástico, use ALTER DATABASE para definir o SERVICE_OBJECTIVE para um nível de desempenho do banco de dados único.  

 Adicionar SECUNDÁRIO ON SERVER \<partner_server_name >  
 Cria um banco de dados replicação geográfica secundária com o mesmo nome em um servidor de parceiro, tornando o banco de dados local em uma replicação geográfica primário e começa a replicação de dados assíncrona do primário para o novo secundário. Se um banco de dados com o mesmo nome já existir no secundário, o comando falhará. O comando é executado no banco de dados mestre no servidor que hospeda o banco de dados local que se torna o principal.  
  
 COM ALLOW_CONNECTIONS {TODOS | **NÃO** }  
 Quando ALLOW_CONNECTIONS não for especificado, ele é definido como não, por padrão. Se estiver definido como todos, é um banco de dados somente leitura que permite que todos os logons com as permissões apropriadas para se conectar.  
  
 COM SERVICE_OBJECTIVE {'S0' | 'S1' | 'S2' | ' S3 "| 'S4' | 'S6' | 'S7' | 'S9' | '/S12' | 'P1' | 'P2' | 'P4' | 'P6' | 'P11' | 'P15' | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6'}  
 Quando o SERVICE_OBJECTIVE não for especificado, o banco de dados secundário é criado no mesmo nível de serviço do banco de dados primário. Quando SERVICE_OBJECTIVE for especificado, o banco de dados secundário é criado no nível especificado. Essa opção oferece suporte à criação secundários replicados geograficamente com os níveis de serviço mais baratos. O SERVICE_OBJECTIVE especificado deve estar dentro a mesma edição como a origem. Por exemplo, você não pode especificar S0 se a edição premium.  
  
 ELASTIC_POOL (nome = \<elastic_pool_name)  
 Quando ELASTIC_POOL não for especificado, o banco de dados secundário não é criado em um pool Elástico. Quando ELASTIC_POOL for especificado, o banco de dados secundário é criado no pool especificado.  
  
> [!IMPORTANT]  
>  O usuário que executa o comando Adicionar SECUNDÁRIO deve ser DBManager no servidor primário, ter membros de db_owner no banco de dados local e DBManager no servidor secundário.  
  
 Remover SECUNDÁRIO ON SERVER \<partner_server_name >  
 Remove a replicação geográfica secundário banco de dados especificado no servidor especificado. O comando é executado no banco de dados mestre no servidor que hospeda o banco de dados primário.  
  
> [!IMPORTANT]  
>  O usuário que executa o comando Remover SECUNDÁRIO deve ser DBManager no servidor primário.  
  
 FAILOVER  
 Promove o banco de dados secundário na parceria de replicação geográfica na qual o comando é executado para se tornar primário e rebaixa o primário atual para se tornar o novo secundário. Como parte desse processo, o modo de replicação geográfica temporariamente é alternado de modo assíncrono, de modo síncrono. Durante o processo de failover:  
  
1.  O principal para colocar novas transações.  
  
2.  Todas as transações pendentes são liberadas para o secundário.  
  
3.  O secundário se torna o principal e começa a replicação geográfica assíncrona com o antigo primário / secundário novo.  
  
 Esta sequência garante que nenhuma perda de dados. O período durante o qual os bancos de dados não estão disponíveis é de 0 a 25 segundos, enquanto as funções são alternadas. A operação total deve levar não mais do que cerca de um minuto. Se o banco de dados primário estiver indisponível quando esse comando é emitido, o comando falhará com uma mensagem de erro indicando que o banco de dados primário não está disponível. Se o processo de failover não for concluída e aparece preso, você pode usar o comando para forçar o failover e aceitar a perda de dados - e, em seguida, se for necessário recuperar os dados perdidos, chamar devops (CSS) para recuperar os dados perdidos.  
  
> [!IMPORTANT]  
>  O usuário que executa o comando FAILOVER deve ser DBManager no servidor primário e o servidor secundário.  
  
 FORCE_FAILOVER_ALLOW_DATA_LOSS  
 Promove o banco de dados secundário na parceria de replicação geográfica na qual o comando é executado para se tornar primário e rebaixa o primário atual para se tornar o novo secundário. Use este comando somente quando a réplica primária atual não está mais disponível. Ele foi projetado para recuperação de desastres, quando a restauração de disponibilidade é crítico e perda de dados é aceitável.  
  
 Durante um failover forçado:  
  
1.  O banco de dados secundário especificado imediatamente se torna o banco de dados primário e começa a aceitar novas transações.  
  
2.  Quando a primária original pode reconectar-se com o novo primário, um backup incremental é colocado no original primário, e a primária original se torna um novo secundário.  
  
3.  Para recuperar dados esse backup incremental no primário antigo, o usuário emprega devops/CSS.  
  
4.  Se houver secundários adicionais, sejam reconfigurados automaticamente para se tornar secundários do novo primário. Esse processo é assíncrono e pode haver um atraso até que esse processo for concluído. Até que a reconfiguração seja concluída, secundários continuarão secundários do antigo primário.  
  
> [!IMPORTANT]  
>  O usuário que executa o comando FORCE_FAILOVER_ALLOW_DATA_LOSS deve ser DBManager no servidor primário e o servidor secundário.  
  
## <a name="remarks"></a>Comentários  
 Para remover um banco de dados, use [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md).  
  
 Para diminuir o tamanho de um banco de dados, use [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
 A instrução ALTER DATABASE deve ser executada em modo de confirmação automática (o modo padrão de administração de transações) e não deve ser permitida em uma transação explícita ou implícita.  
  
 A limpeza do cache de planos gera uma recompilação de todos os planos de execução subsequentes e pode provocar uma redução repentina e temporária do desempenho de consultas. Para cada armazenamento em cache limpo no cache de planos, o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém a seguinte mensagem informativa: "O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou %d ocorrência(s) de liberação de armazenamento em cache '% s' (parte do cache de planos) devido à manutenção do banco de dados ou operações de reconfiguração". Essa mensagem é registrada a cada cinco minutos, contanto que o cache seja liberado dentro desse intervalo de tempo.  
  
 O cache de procedimento também é liberado nos seguintes cenários:  
  
-   Um banco de dados tem a opção de banco de dados AUTO_CLOSE definida como ON. Quando nenhuma conexão de usuário fizer referência ou usar o banco de dados, a tarefa de banco de dados tentará fechar e encerrar o banco de dados automaticamente.  
  
-   Execute diversas consultas em um banco de dados que tem opções padrão. O banco de dados é removido.  
  
-   Você recria com sucesso o log de transação para um banco de dados.  
  
-   Você restaura um backup de banco de dados.  
  
-   Você desanexa um banco de dados.  
  
## <a name="viewing-database-information"></a>Exibindo informações do banco de dados  
 É possível usar exibições do catálogo, funções do sistema e procedimentos armazenados do sistema para retornar informações sobre bancos de dados, arquivos e grupos de arquivos.  
  
## <a name="permissions"></a>Permissões  
 Somente o logon de entidade de segurança no nível do servidor (criado pelo processo de provisionamento) ou os membros da função de banco de dados `dbmanager` podem alterar um banco de dados.  
  
> [!IMPORTANT]  
>  O proprietário do banco de dados não pode alterar o banco de dados, a menos que seja um membro da função `dbmanager`.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-check-the-edition-options-and-change-them"></a>A. Verifique as opções de edição e alterá-los:

```
SELECT Edition = DATABASEPROPERTYEX('db1', 'EDITION'),
        ServiceObjective = DATABASEPROPERTYEX('db1', 'ServiceObjective'),
        MaxSizeInBytes =  DATABASEPROPERTYEX('db1', 'MaxSizeInBytes');

ALTER DATABASE [db1] MODIFY (EDITION = 'Premium', MAXSIZE = 1024 GB, SERVICE_OBJECTIVE = 'P15');
```

### <a name="b-moving-a-database-to-a-different-elastic-pool"></a>B. Mover um banco de dados para um pool Elástico diferente  
 Move um banco de dados existente em um pool chamado pool1:  
  
```  
ALTER DATABASE db1   
MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = pool1 ) ) ;  
```  
  
### <a name="c-add-a-geo-replication-secondary"></a>C. Adicionar um secundário de replicação geográfica  
 Cria um banco de dados secundário não legível db1 no servidor `secondaryserver` de db1 no servidor local.  
  
```  
ALTER DATABASE db1   
ADD SECONDARY ON SERVER secondaryserver   
WITH ( ALLOW_CONNECTIONS = NO )  
```  
  
### <a name="d-remove-a-geo-replication-secondary"></a>D. Remover um secundário de replicação geográfica  
 Remove o banco de dados secundário db1 no servidor `secondaryserver`.  
  
```  
ALTER DATABASE db1   
REMOVE SECONDARY ON SERVER testsecondaryserver   
```  
  
### <a name="e-failover-to-a-geo-replication-secondary"></a>E. Failover para um secundário de replicação geográfica  
 Promove db1 um banco de dados secundário no servidor `secondaryserver` se torne o novo banco de dados primário quando executada no servidor `secondaryserver`.  
  
```  
ALTER DATABASE db1 FAILOVER  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criar banco de dados &#40; Banco de dados SQL do Azure &#41;](../../t-sql/statements/create-database-azure-sql-database.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [Definir nível de ISOLAMENTO da transação &#40; Transact-SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [database_mirroring_witnesses &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys. filegroups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys. master_files &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Bancos de dados do sistema](../../relational-databases/databases/system-databases.md)  
  
  

