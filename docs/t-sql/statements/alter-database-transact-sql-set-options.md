---
title: Opções ALTER DATABASE SET (Transact-SQL) | Microsoft Docs
description: Saiba mais sobre como definir opções de banco de dados, como criptografia e ajuste automáticos, repositório de consultas em um Banco de Dados SQL do Azure ou SQL Server
ms.custom: ''
ms.date: 08/08/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- online database state [SQL Server]
- database options [SQL Server]
- emergency database state [SQL Server]
- databases [SQL Server], options
- read-only databases
- recovery models [SQL Server], switching
- ALTER DATABASE statement, SET options
- offline database state [SQL Server]
- snapshot isolation framework option
- checksums [SQL Server]
- automatic tuning
- SQL plan regression correction
- auto_create_statistics
- auto_update_statistics
ms.assetid: f76fbd84-df59-4404-806b-8ecb4497c9cc
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||=azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 34dfaa1d241c015ed94bc21997d9e6a3c8254339
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762624"
---
# <a name="alter-database-set-options-transact-sql"></a>Opções ALTER DATABASE SET (Transact-SQL) 

Define opções em banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e no Banco de Dados SQL do Azure. Para obter outras opções de ALTER DATABASE, confira [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md).

Clique em uma das guias a seguir para ver sintaxe, argumentos, comentários, permissões e exemplos de uma versão específica do SQL com a qual você está trabalhando.

Para obter mais informações sobre as convenções de sintaxe, veja [Convenções de sintaxe do Transact-SQL] (../../t-sql/language-elements/transact-sql-synt). Para obter mais informações sobre as convenções de sintaxe, veja [Convenções de sintaxe do Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md). 

## <a name="click-a-product"></a>Clique em um produto!

Na linha a seguir, clique em qualquer nome de produto de seu interesse. O clique exibe conteúdo diferente aqui nesta página da Web, apropriado para qualquer produto no qual você clicar.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> <table>
> <tr>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
> </tr>
> <tr>
>   <th><strong><em>* SQL Server *<br />&nbsp;</em></strong></th>
>   <th><a href="alter-database-transact-sql-set-options.md?view=azuresqldb-current">Banco de Dados SQL<br />Banco de Dados SQL</a></th>
>   <th><a href="alter-database-transact-sql-set-options.md?view=azuresqldb-mi-current">Banco de Dados SQL<br />Banco de Dados SQL</a></th>
> </tr>
> </table>

&nbsp;

# <a name="sql-server"></a>SQL Server
  
O espelhamento de banco de dados, [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] e os níveis de compatibilidade são opções `SET`, mas são descritos em artigos separados devido ao seu tamanho. Para saber mais, confira [Espelhamento de Banco de Dados de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md), [ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md) e [Nível de compatibilidade de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
> [!NOTE]  
> Muitas opções de definição de banco de dados podem ser configuradas para a sessão atual usando [Instruções SET](../../t-sql/statements/set-statements-transact-sql.md) e são configuradas com frequência por aplicativos quando eles são conectados. As opções definidas no nível de sessão substituem os valores de **ALTER DATABASE SET** . As opções de banco de dados descritas abaixo são os valores que podem ser definidos para as sessões que não fornecem explicitamente outros valores de definição de conjunto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ALTER DATABASE { database_name  | CURRENT }  
SET   
{  
    <option_spec> [ ,...n ] [ WITH <termination> ]   
}  
  
<option_spec> ::=   
{  
    <auto_option>   
  | <automatic_tuning_option>   
  | <change_tracking_option>   
  | <containment_option>   
  | <cursor_option>   
  | <database_mirroring_option>  
  | <date_correlation_optimization_option>  
  | <db_encryption_option>  
  | <db_state_option>  
  | <db_update_option>   
  | <db_user_access_option>   
  | <delayed_durability_option>  
  | <external_access_option>  
  | FILESTREAM ( <FILESTREAM_option> )  
  | <HADR_options>  
  | <mixed_page_allocation_option>  
  | <parameterization_option>  
  | <query_store_options>  
  | <recovery_option>  
  | <remote_data_archive_option>  
  | <service_broker_option>  
  | <snapshot_option>  
  | <sql_option>   
  | <target_recovery_time_option> 
  | <termination>  
}  
;
  
<auto_option> ::=   
{  
    AUTO_CLOSE { ON | OFF }   
  | AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] }   
  | AUTO_SHRINK { ON | OFF }   
  | AUTO_UPDATE_STATISTICS { ON | OFF }   
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
}  
  
<automatic_tuning_option> ::=  
{  
  AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = { ON | OFF } )
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
  
<containment_option> ::=   
   CONTAINMENT = { NONE | PARTIAL }  
  
<cursor_option> ::=   
{  
    CURSOR_CLOSE_ON_COMMIT { ON | OFF }   
  | CURSOR_DEFAULT { LOCAL | GLOBAL }   
}  
  
<database_mirroring_option>  
  ALTER DATABASE Database Mirroring  
  
<date_correlation_optimization_option> ::=  
    DATE_CORRELATION_OPTIMIZATION { ON | OFF }  
  
<db_encryption_option> ::=  
    ENCRYPTION { ON | OFF }  
  
<db_state_option> ::=  
    { ONLINE | OFFLINE | EMERGENCY }  
  
<db_update_option> ::=  
    { READ_ONLY | READ_WRITE }  
  
<db_user_access_option> ::=  
    { SINGLE_USER | RESTRICTED_USER | MULTI_USER }  
  
<delayed_durability_option> ::=  
    DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }  
  
<external_access_option> ::=  
{  
    DB_CHAINING { ON | OFF }  
  | TRUSTWORTHY { ON | OFF }  
  | DEFAULT_FULLTEXT_LANGUAGE = { <lcid> | <language name> | <language alias> }  
  | DEFAULT_LANGUAGE = { <lcid> | <language name> | <language alias> }  
  | NESTED_TRIGGERS = { OFF | ON }  
  | TRANSFORM_NOISE_WORDS = { OFF | ON }  
  | TWO_DIGIT_YEAR_CUTOFF = { 1753, ..., 2049, ..., 9999 }  
}  
<FILESTREAM_option> ::=  
{  
    NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL   
  | DIRECTORY_NAME = <directory_name>  
}  
<HADR_options> ::=  
    ALTER DATABASE SET HADR  
  
<mixed_page_allocation_option> ::=  
    MIXED_PAGE_ALLOCATION { OFF | ON }  
  
<parameterization_option> ::=  
    PARAMETERIZATION { SIMPLE | FORCED }  
  
<query_store_options> ::=  
{  
    QUERY_STORE   
    {  
          = OFF   
        | = ON [ ( <query_store_option_list> [,...n] ) ]  
        | ( < query_store_option_list> [,...n] )  
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
    | WAIT_STATS_CAPTURE_MODE = [ ON | OFF ]
}  
  
<recovery_option> ::=   
{  
    RECOVERY { FULL | BULK_LOGGED | SIMPLE }   
  | TORN_PAGE_DETECTION { ON | OFF }  
  | PAGE_VERIFY { CHECKSUM | TORN_PAGE_DETECTION | NONE }  
}  
  
<remote_data_archive_option> ::=  
{  
    REMOTE_DATA_ARCHIVE =  
    {  
        ON ( SERVER = <server_name> ,   
                  {   CREDENTIAL = <db_scoped_credential_name>  
                     | FEDERATED_SERVICE_ACCOUNT =  ON | OFF   
                  }  
               )  
      | OFF  
    }  
}  
  
<service_broker_option> ::=  
{  
    ENABLE_BROKER  
  | DISABLE_BROKER  
  | NEW_BROKER  
  | ERROR_BROKER_CONVERSATIONS  
  | HONOR_BROKER_PRIORITY { ON | OFF}  
}  
  
<snapshot_option> ::=  
{  
    ALLOW_SNAPSHOT_ISOLATION { ON | OFF }  
  | READ_COMMITTED_SNAPSHOT {ON | OFF }  
  | MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = {ON | OFF }  
}  
<sql_option> ::=   
{  
    ANSI_NULL_DEFAULT { ON | OFF }   
  | ANSI_NULLS { ON | OFF }   
  | ANSI_PADDING { ON | OFF }   
  | ANSI_WARNINGS { ON | OFF }   
  | ARITHABORT { ON | OFF }   
  | COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 | 90 }   
  | CONCAT_NULL_YIELDS_NULL { ON | OFF }   
  | NUMERIC_ROUNDABORT { ON | OFF }   
  | QUOTED_IDENTIFIER { ON | OFF }   
  | RECURSIVE_TRIGGERS { ON | OFF }   
}  
  
<target_recovery_time_option> ::=  
    TARGET_RECOVERY_TIME = target_recovery_time { SECONDS | MINUTES }  
  
<termination>  ::=   
{  
    ROLLBACK AFTER integer [ SECONDS ]   
  | ROLLBACK IMMEDIATE   
  | NO_WAIT  
}  
```  
  
## <a name="arguments"></a>Argumentos  
*database_name*  
É o nome do banco de dados a ser modificado.  
  
CURRENT  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
`CURRENT` executa a ação no banco de dados atual. `CURRENT` não é compatível com todas as opções em todos os contextos. Se `CURRENT` falhar, forneça o nome do banco de dados.  
  
**\<auto_option> ::=**
  
Controla opções automáticas.  
<a name="auto_close"></a> AUTO_CLOSE { ON | OFF }  
ON  
O banco de dados é desligado corretamente e seus recursos são liberados depois da saída do último usuário.  
  
O banco de dados é reaberto automaticamente quando um usuário tenta usá-lo de novo. Por exemplo, quando é emitida uma instrução `USE database_name`. Se o banco de dados for desligado corretamente enquanto AUTO_CLOSE estiver definido como ON, ele não será reaberto até que um usuário tente usá-lo na próxima vez que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] for reiniciado.  
  
OFF  
O banco de dados permanecerá aberto depois da saída do último usuário.  
  
A opção AUTO_CLOSE é útil para bancos de dados desktop porque permite que os arquivos de banco de dados sejam gerenciados como arquivos comuns. Eles podem ser movidos, copiados para fazer backups ou mesmo enviados por email a outros usuários. O processo AUTO_CLOSE é assíncrono; abrir e fechar o banco de dados repetidamente não mais prejudica o desempenho.  
  
> [!NOTE]  
>  A opção AUTO_CLOSE não está disponível em um Banco de Dados Independente nem em [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
O status dessa opção pode ser determinado examinando-se a coluna is_auto_close_on na exibição do catálogo sys.databases ou a propriedade IsAutoClose da função DATABASEPROPERTYEX.  
  
> [!NOTE]  
>  Quando AUTO_CLOSE for ON, algumas colunas da exibição de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) e da função DATABASEPROPERTYEX retornarão NULL, pois o banco de dados não está disponível para recuperar os dados. Para resolver isso, execute uma instrução USE para abrir o banco de dados.  
  
> [!NOTE]  
>  O espelhamento do banco de dados requer AUTO_CLOSE OFF.  
  
Quando o banco de dados é definido como AUTOCLOSE = ON, uma operação que inicia o desligamento automático do banco de dados limpa o cache do plano da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A limpeza do cache de planos gera uma recompilação de todos os planos de execução subsequentes e pode provocar uma redução repentina e temporária do desempenho de consultas. No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 e superior, para cada armazenamento em cache eliminado do cache de planos, o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém a seguinte mensagem informativa: "O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou %d ocorrência(s) de liberação de armazenamento em cache '% s' (parte do cache de planos) devido à manutenção do banco de dados ou operações de reconfiguração". Essa mensagem é registrada a cada cinco minutos, contanto que o cache seja liberado dentro desse intervalo de tempo.  
 
<a name="auto_create_statistics"></a> AUTO_CREATE_STATISTICS { ON | OFF }  
ON  
O otimizador de consulta cria estatísticas em colunas únicas em predicados de consulta, conforme necessário, para melhorar planos e desempenho de consulta. Estas estatísticas de coluna única são criadas quando o otimizador de consulta compila consultas. As estatísticas de coluna única só são criadas em colunas que ainda não são a primeira de um objeto de estatísticas existente.  
  
O padrão é ON. Nós recomendamos que você use a configuração padrão para a maioria dos bancos de dados.  
  
OFF  
O otimizador de consulta não cria estatísticas em colunas únicas em predicados de consulta quando estiver compilando consultas. Definir essa opção como OFF pode acarretar planos de consulta de qualidade inferior e menor desempenho de consulta.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_create_stats_on na exibição do catálogo sys.databases ou a propriedade IsAutoCreateStatistics da função DATABASEPROPERTYEX.  
  
Para obter mais informações, veja a seção “Usando as opções de estatísticas em todo o banco de dados” em [Estatística](../../relational-databases/statistics/statistics.md).  
  
INCREMENTAL = ON | OFF  
Quando AUTO_CREATE_STATISTICS estiver ON e INCREMENTAL estiver definido como ON, as estatísticas criadas automaticamente são criadas como incrementais sempre que as estatísticas incrementais tiverem suporte. O valor padrão é OFF. Para saber mais, veja [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md).  
  
**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
<a name="auto_shrink"></a> AUTO_SHRINK { ON | OFF }  
ON  
Os arquivos de banco de dados são candidatos à redução periódica.  
  
Arquivos de dados e arquivos de log podem ser reduzidos automaticamente. AUTO_SHRINK reduzirá o tamanho do log de transações somente se o banco de dados estiver definido como modelo de recuperação SIMPLE ou se foi feito backup do log. Quando definido como OFF, os arquivos de banco de dados não são reduzidos automaticamente durante as verificações periódicas de espaço não utilizado.  
  
A opção AUTO_SHRINK faz com que os arquivos sejam reduzidos quando mais que 25% do arquivo contém espaço não utilizado. O arquivo é reduzido de forma que 25% de seu tamanho seja de espaço não utilizado ou ele tenha o mesmo tamanho de quando foi criado, o que for maior.  
  
Não é possível reduzir um banco de dados somente leitura.  
  
OFF  
Os arquivos de banco de dados não são reduzidos automaticamente durante as verificações periódicas de espaço não utilizado.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_auto_shrink_on na exibição do catálogo sys.databases ou a propriedade IsAutoShrink da função DATABASEPROPERTYEX.  
  
> [!NOTE]  
> A opção AUTO_SHRINK não está disponível em um banco de dados independente.  
  
<a name="auto_update_statistics"></a> AUTO_UPDATE_STATISTICS { ON | OFF }  
ON  
Especifica que o otimizador de consultas atualiza estatísticas quando são usadas por uma consulta e quando podem estar desatualizadas. As estatísticas ficam desatualizadas depois que operações de inserção, atualização, exclusão ou mesclagem alteram a distribuição de dados na tabela ou na exibição indexada. O otimizador de consulta determina quando estatísticas podem estar desatualizadas contando o número de modificações de dados desde a última atualização das estatísticas e comparando o número de modificações a um limite. O limite se baseia no número de linhas na tabela ou na exibição indexada.  
  
O otimizador de consulta procura estatísticas desatualizadas antes de compilar uma consulta e antes de executar um plano de consulta em cache. Antes de compilar uma consulta, o otimizador de consulta usa as colunas, tabelas e exibições indexadas no predicado de consulta para determinar quais estatísticas podem estar desatualizadas. Antes de executar um plano de consulta em cache, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifica se o plano de consulta faz referência a estatísticas atualizadas.  
  
A opção AUTO_UPDATE_STATISTICS se aplica a estatísticas criadas para índices, colunas únicas em predicados de consulta, além de estatísticas criadas por meio da instrução CREATE STATISTICS. Essa opção também se aplica a estatísticas filtradas.  
  
O padrão é ON. Nós recomendamos que você use a configuração padrão para a maioria dos bancos de dados.  
  
Use a opção AUTO_UPDATE_STATISTICS_ASYNC para especificar se as estatísticas são atualizadas de forma síncrona ou assíncrona.  
  
OFF  
Especifica que o otimizador de consulta não atualiza estatísticas quando elas são usadas por uma consulta e quando elas podem ficar desatualizadas. Definir essa opção como OFF pode acarretar planos de consulta de qualidade inferior e menor desempenho de consulta.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_update_stats_on na exibição do catálogo sys.databases ou a propriedade IsAutoUpdateStatistics da função DATABASEPROPERTYEX.  
  
Para obter mais informações, veja a seção “Usando as opções de estatísticas em todo o banco de dados” em [Estatística](../../relational-databases/statistics/statistics.md).  
  
<a name="auto_update_statistics_async"></a> AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
ON  
Especifica que atualizações de estatísticas para a opção AUTO_UPDATE_STATISTICS são assíncronas. O otimizador de consulta não aguarda a conclusão das atualizações de estatísticas para compilar consultas.  
  
Definir essa opção como ON não tem nenhum efeito, a menos que AUTO_UPDATE_STATISTICS seja definida como ON.  
  
Por padrão, a opção AUTO_UPDATE_STATISTICS_ASYNC é definida como OFF e o otimizador de consulta atualiza estatísticas de forma síncrona.  
  
OFF  
Especifica que atualizações de estatísticas para a opção AUTO_UPDATE_STATISTICS são síncronas. O otimizador de consulta aguarda a conclusão das atualizações de estatísticas para compilar consultas.  
  
Definir essa opção como OFF não tem nenhum efeito, a menos que AUTO_UPDATE_STATISTICS seja definida como ON.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_auto_update_stats_async_on na exibição do catálogo sys.databases.  
  
Para obter mais informações que descrevem quando usar atualizações de estatísticas síncronas ou assíncronas, veja a seção que "Usando as opções de estatísticas em todo o banco de dados" em [Estatísticas](../../relational-databases/statistics/statistics.md).  
  
<a name="auto_tuning"></a> **\<automatic_tuning_option> ::=**  
**Aplica-se a**: [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  

Habilita ou desabilita a opção de `FORCE_LAST_GOOD_PLAN` [ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md).  
  
FORCE_LAST_GOOD_PLAN = { ON | OFF }  
ON  
O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] força automaticamente o último plano sabidamente válido nas consultas [!INCLUDE[tsql-md](../../includes/tsql-md.md)] em que o novo plano SQL provoca regressões de desempenho. O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] monitora continuamente o desempenho de consultas da consulta [!INCLUDE[tsql-md](../../includes/tsql-md.md)] com o plano forçado. Se não houver ganhos de desempenho, o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] continuará usando o último plano válido conhecido. Se os ganhos de desempenho não forem detectados, o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] produzirá um novo plano SQL. A instrução falhará se o repositório de consultas não estiver habilitado ou não estiver no modo de *Leitura-Gravação*.   
OFF  
O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] relata possíveis regressões de desempenho de consulta causadas por alterações de plano SQL na exibição [sys.dm_db_tuning_recommendations](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md). No entanto, essas recomendações não são aplicadas automaticamente. Usuário pode monitorar recomendações ativas e corrigir problemas identificados aplicando scripts [!INCLUDE[tsql-md](../../includes/tsql-md.md)] mostrados na exibição. Este é o valor padrão.

**\<change_tracking_option> ::=**  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDSFull](../../includes/sssds-md.md)].  
  
Controla as opções de controle de alterações. É possível habilitar o controle de alterações, definir opções, alterar opções e desabilitar o controle de alterações. Para obter exemplos, confira a seção Exemplos mais adiante neste artigo.  
  
ON  
Habilita o controle de alterações no banco de dados. Quando você habilita o controle de alterações, também pode definir as opções AUTO CLEANUP e CHANGE RETENTION.  
  
AUTO_CLEANUP = { ON | OFF }  
ON  
As informações de controle de alterações são removidas automaticamente depois do período de retenção especificado.  
  
OFF  
Os dados de controle de alterações não são removidos do banco de dados.  
  
CHANGE_RETENTION =*retention_period* { DAYS | HOURS | MINUTES }  
Especifica o período mínimo para manter as informações de controle de alterações no banco de dados. Os dados serão removidos somente quando o valor AUTO_CLEANUP for ON.  
  
*retention_period* é um inteiro que especifica o componente numérico do período de retenção.  
  
O período de retenção padrão é de 2 dias. O período de retenção mínimo é de 1 minuto. O tipo de retenção padrão é DAYS.  
  
OFF  
Desabilita o controle de alterações no banco de dados. É necessário desabilitar o controle de alterações em todas as tabelas antes de poder desabilitá-lo no banco de dados.  
  
**\<containment_option> ::=**  
  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Controla opções de contenção de banco de dados.  
  
CONTAINMENT = { NONE | PARTIAL}  
Nenhuma  
O banco de dados não é um banco de dados independente.  
  
PARTIAL  
O banco de dados é um banco de dados independente. Haverá falha na configuração da contenção do banco de dados como parcial, se o banco de dados tiver replicação, Change Data Capture ou controle de alterações habilitados. A verificação de erros é interrompida depois de uma falha. Para obter mais informações sobre bancos de dados independentes, consulte [Contained Databases](../../relational-databases/databases/contained-databases.md).  
  
**\<cursor_option> ::=**  
  
Controla opções de cursor.  
  
CURSOR_CLOSE_ON_COMMIT { ON | OFF }  
ON  
Qualquer cursor é aberto quando uma transação é confirmada ou quando uma transação revertida é fechada.  
  
OFF  
Os cursores permanecem abertos quando uma transação é confirmada; uma transação revertida fechará todos os cursores, exceto aqueles definidos como INSENSITIVE ou STATIC.  
  
As configurações no nível de conexão que são definidas com o uso da instrução SET substituem a configuração de banco de dados padrão por CURSOR_CLOSE_ON_COMMIT. Por padrão, clientes ODBC e OLE DB emitem uma configuração CURSOR_CLOSE_ON_COMMIT de instrução SET no nível de conexão como desativada para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET CURSOR_CLOSE_ON_COMMIT](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md).  
  
O status dessa opção pode ser determinado examinando-se a coluna is_cursor_close_on_commit_on na exibição do catálogo sys.databases ou a propriedade IsCloseCursorsOnCommitEnabled da função DATABASEPROPERTYEX.  
 
CURSOR_DEFAULT { LOCAL | GLOBAL }  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
Controla se o escopo do cursor usa LOCAL ou GLOBAL.  
  
LOCAL  
Quando LOCAL for especificado e um cursor não for definido como GLOBAL ao ser criado, o escopo do cursor será local para o lote, o procedimento armazenado ou o gatilho nos quais o cursor foi criado. O nome de cursor é válido somente dentro desse escopo. O cursor pode ser referenciado por meio de variáveis de cursor local no lote, no procedimento armazenado ou no gatilho, ou em um parâmetro OUTPUT do procedimento armazenado. O cursor será implicitamente desalocado quando o lote, o procedimento armazenado ou o gatilho for encerrado, a menos que seja repassado como um parâmetro OUTPUT. Se for repassado em um parâmetro OUTPUT, o cursor será desalocado quando a última variável que o referencia for desalocada ou sair do escopo.  
  
GLOBAL  
Quando GLOBAL for especificado e um cursor não for definido como LOCAL ao ser criado, o escopo do cursor será global para a conexão. O nome do cursor pode ser referenciado em qualquer procedimento armazenado ou lote executado pela conexão.  
  
O cursor é implicitamente desalocado somente na desconexão. Para saber mais, confira [DECLARE CURSOR](../../t-sql/language-elements/declare-cursor-transact-sql.md).  
  
O status dessa opção pode ser determinado examinando-se a coluna is_local_cursor_default na exibição do catálogo sys.databases ou a propriedade IsLocalCursorsDefault da função DATABASEPROPERTYEX.  
  
**\<database_mirroring>**  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
Veja as descrições de argumentos em [Espelhamento de banco de dados ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md).  
  
**\<date_correlation_optimization_option> ::=**  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
Controla a opção date_correlation_optimization.  
  
DATE_CORRELATION_OPTIMIZATION { ON | OFF }  
ON  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém as estatísticas de correlação entre quaisquer duas tabelas do banco de dados que estejam vinculadas por uma restrição FOREIGN KEY e que tenham colunas **datetime**.  
  
OFF  
Estatísticas de correlação não são mantidas.  
  
Para que seja possível definir DATE_CORRELATION_OPTIMIZATION como ON, não deve haver nenhuma conexão ativa com o banco de dados exceto aquela que está executando a instrução ALTER DATABASE. Depois, há suporte a várias conexões.  
  
A configuração atual dessa opção pode ser determinada examinando-se a coluna is_date_correlation_on na exibição do catálogo sys.databases.  
  
**\<db_encryption_option> ::=**  
  
Controla o estado de criptografia do banco de dados.  
  
ENCRYPTION {ON | OFF}  
Define o banco de dados a ser criptografado (ON) ou não criptografado (OFF). Para saber mais sobre criptografia de banco de dados, confira [Transparent Data Encryption](../../relational-databases/security/encryption/transparent-data-encryption.md) e [Transparent Data Encryption com o Banco de Dados SQL do Azure](../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md).  
  
Quando a criptografia estiver habilitada no nível de banco de dados, todos os grupos de arquivos serão criptografados. Qualquer novo grupo de arquivos herdará a propriedade criptografada. Se algum grupo de arquivos do banco de dados for definido como **READ ONLY**, haverá falha na operação de criptografia de banco de dados.  
  
É possível ver o estado da criptografia do banco de dados usando a exibição de gerenciamento dinâmico [sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md).  
  
**\<db_state_option> ::=**  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
Controla o estado do banco de dados.  
  
OFFLINE  
O banco de dados é fechado, desligado corretamente e marcado como offline. Não é possível modificar o banco de dados enquanto ele estiver offline.  
  
ONLINE  
O banco de dados está aberto e disponível para uso.  
  
EMERGENCY  
O banco de dados está marcado como READ_ONLY, o log está desabilitado e o acesso é limitado aos membros da função de servidor fixa sysadmin. EMERGENCY é usado principalmente para a solução de problemas. Por exemplo, um banco de dados marcado como suspeito devido a um arquivo de log corrompido pode ser definido com o estado EMERGENCY. Isso permite habilitar o acesso somente leitura do administrador do sistema ao banco de dados. Apenas membros da função de servidor fixa sysadmin podem definir um banco de dados com o estado EMERGENCY.  
  
> [!NOTE]  
> **Permissões:** a permissão ALTER DATABASE para o banco de dados de assunto é necessária para alterar um banco de dados para o estado offline ou emergência. A permissão ALTER ANY DATABASE no nível do servidor é necessária para mover um banco de dados de offline para online.  
  
O status dessa opção pode ser determinado examinando as colunas state e state_desc na exibição do catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) ou a propriedade Status da função [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md). Para obter mais informações, consulte [Database States](../../relational-databases/databases/database-states.md).  
  
Um banco de dados marcado como RESTORING não pode ser definido como OFFLINE, ONLINE ou EMERGENCY. Um banco de dados pode estar no estado RESTORING durante uma operação de restauração ativa ou quando uma operação de restauração de um banco de dados ou arquivo de log falhar devido a um arquivo de backup corrompido.  
  
**\<db_update_option> ::=**  
  
Controla se atualizações são permitidas no banco de dados.  
  
READ_ONLY  
Os usuários podem ler dados do banco de dados, mas não modificá-los.  
  
> [!NOTE]  
>  Para melhorar o desempenho da consulta, atualize as estatísticas antes de configurar um banco de dados como READ_ONLY. Se forem necessárias estatísticas adicionais depois de um banco de dados ser definido como READ_ONLY, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] criará estatísticas no tempdb. Para obter mais informações sobre estatísticas para um banco de dados somente leitura, veja [Estatísticas](../../relational-databases/statistics/statistics.md).  
  
READ_WRITE  
O banco de dados está disponível para operações de leitura e gravação.  
  
Para alterar esse estado, é necessário ter acesso exclusivo ao banco de dados. Para obter mais informações, consulte a cláusula SINGLE_USER.  
  
> [!NOTE]  
> Nos bancos de dados federados do [!INCLUDE[ssSDS](../../includes/sssds-md.md)], SET { READ_ONLY | READ_WRITE } é desabilitado.  
  
**\<db_user_access_option> ::=**  
  
Controla o acesso de usuários ao banco de dados.  
  
SINGLE_USER  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
Especifica que somente um usuário por vez pode acessar o banco de dados. Se SINGLE_USER for especificado e houver outros usuários conectados ao banco de dados, a instrução ALTER DATABASE será bloqueada até que todos os usuários se desconectem do banco de dados especificado. Para substituir esse comportamento, veja a cláusula WITH \<termination>.  
  
O banco de dados permanecerá no modo SINGLE_USER, mesmo que o usuário que definiu a opção faça logoff. Nesse momento, um usuário diferente, mas somente um, poderá se conectar ao banco de dados.  
  
Antes de definir o banco de dados como SINGLE_USER, verifique se a opção AUTO_UPDATE_STATISTICS_ASYNC está definida como OFF. Quando definida como ON, o thread em segundo plano usado para a atualização de estatísticas estabelece uma conexão com o banco de dados e não é possível acessar o banco de dados em modo de usuário único. Para exibir o status dessa opção, consulte a coluna is_auto_update_stats_async_on na exibição do catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md). Se a opção estiver definida como ON, execute as tarefas a seguir:  
  
1. Defina AUTO_UPDATE_STATISTICS_ASYNC como OFF.  
  
2. Verifique se há estatísticas assíncronas ativas, examinando a exibição de gerenciamento dinâmico [sys.dm_exec_background_job_queue](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md).  
  
Se houver tarefas ativas, permita que as tarefas sejam concluídas ou as termine manualmente usando [KILL STATS JOB](../../t-sql/language-elements/kill-stats-job-transact-sql.md).  
  
RESTRICTED_USER  
RESTRICTED_USER permite que somente os membros da função de banco de dados fixa db_owner e das funções de servidor fixas dbcreator e sysadmin conectem-se ao banco de dados, mas não limita seu número. Todas as conexões com o banco de dados são desconectadas no período especificado pela cláusula de término da instrução ALTER DATABASE. Depois que o banco de dados fizer a transição para o estado RESTRICTED_USER, as tentativas de conexão realizadas por usuários não qualificados serão recusadas.  
  
MULTI_USER  
Todos os usuários com permissões apropriadas para se conectar ao banco de dados são permitidos.  
  
O status dessa opção pode ser determinado examinando-se a coluna user_access na exibição do catálogo sys.databases ou a propriedade UserAccess da função DATABASEPROPERTYEX.  
  
**\<delayed_durability_option> ::=**  
  
**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Controla se as transações são confirmadas completamente duráveis ou duráveis atrasadas.  
  
DISABLED  
Todas as transações após SET DISABLED são completamente duráveis. Todas as opções de durabilidade definidas em um bloco atômico ou instrução de confirmação são ignoradas.  
  
ALLOWED  
Todas as transações após SET ALLOWED são completamente duráveis ou duráveis atrasadas, dependendo da opção de durabilidade definida no bloco atômico ou instrução de confirmação.  
  
FORCED  
Todas as transações após SET FORCED são duráveis atrasadas. Todas as opções de durabilidade definidas em um bloco atômico ou instrução de confirmação são ignoradas.  
  
**\<external_access_option> ::=**  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
Controla se o banco de dados pode ser acessado por recursos externos, como objetos de outro banco de dados.  
  
DB_CHAINING { ON | OFF }  
ON  
O banco de dados pode ser a origem ou o destino de um encadeamento de propriedades de bancos de dados.  
  
OFF  
O banco de dados não pode participar do encadeamento de propriedades de bancos de dados.  
  
> [!IMPORTANT]  
> A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reconhecerá essa configuração quando a opção do servidor Encadeamento de Propriedades de Bancos de Dados for 0 (OFF). Quando Encadeamento de Propriedades de BD for 1 (ON), todos os bancos de dados de usuário poderão participar de cadeias de propriedades de bancos de dados, independentemente do valor dessa opção. Essa opção é definida por meio de [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
Definir essa opção requer a permissão CONTROL SERVER no banco de dados.  
  
A opção DB_CHAINING não pode ser definida nestes bancos de dados do sistema: mestre, modelo e tempdb.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_db_chaining_on na exibição do catálogo sys.databases.  
  
TRUSTWORTHY { ON | OFF }  
ON  
Os módulos de banco de dados (por exemplo, funções definidas pelo usuário ou procedimentos armazenados) que usam um contexto de representação poderão acessar recursos fora do banco de dados.  
  
OFF  
Os módulos de banco de dados em um contexto de representação não poderão acessar recursos fora do banco de dados.  
  
TRUSTWORTHY será definido como OFF sempre que o banco de dados for anexado.  
  
Por padrão, todos os bancos de dados do sistema, exceto o banco de dados msdb, têm TRUSTWORTHY definido como OFF. O valor não pode ser alterado para os bancos de dados modelo e tempdb. É recomendável nunca definir a opção TRUSTWORTHY como ON para o banco de dados mestre.  
  
Definir essa opção requer a permissão CONTROL SERVER no banco de dados.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_db_trustworthy_on na exibição do catálogo sys.databases.  
  
DEFAULT_FULLTEXT_LANGUAGE  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Especifica o valor de idioma padrão para colunas indexadas de texto completo.  
  
> [!IMPORTANT]  
>  Essa opção será permitida apenas quando CONTAINMENT estiver definido como PARTIAL. Se CONTAINMENT não for definida como NOME, ocorrerão erros.  
  
DEFAULT_LANGUAGE  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Especifica a linguagem padrão para todos os logons recém-criados. O idioma pode ser especificado com o fornecimento da ID (lcid), do nome do idioma ou do alias do idioma. Para obter uma lista de nomes de idiomas e aliases aceitáveis, veja [sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md). Essa opção será permitida apenas quando CONTAINMENT estiver definido como PARTIAL. Se CONTAINMENT não for definida como NOME, ocorrerão erros.  
  
NESTED_TRIGGERS  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Especifica se um gatilho AFTER pode ser colocado em cascata, ou seja, executar uma ação que inicia outro gatilho que inicia outro gatilho e assim por diante. Essa opção será permitida apenas quando CONTAINMENT estiver definido como PARTIAL. Se CONTAINMENT não for definida como NOME, ocorrerão erros.  
  
TRANSFORM_NOISE_WORDS  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Usado para suprimir uma mensagem de erro se palavras de ruído ou palavras irrelevantes provocarem falha em uma operação Booliana em uma consulta de texto completo. Essa opção será permitida apenas quando CONTAINMENT estiver definido como PARTIAL. Se CONTAINMENT não for definida como NOME, ocorrerão erros.  
  
TWO_DIGIT_YEAR_CUTOFF  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Especifica um inteiro de 1753 a 9999 que representa o ano de corte para interpretar anos de dois dígitos e de quatro dígitos. Essa opção será permitida apenas quando CONTAINMENT estiver definido como PARTIAL. Se CONTAINMENT não for definida como NOME, ocorrerão erros.  
 
**\<FILESTREAM_option> ::=**  
  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Controla as configurações de FileTables.  
  
NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL }  
OFF  
O acesso não transacional a dados de FileTable está habilitado.  
  
READ_ONLY  
Os dados FILESTREAM em FileTables neste banco de dados podem ser lidos por processos não transacionais.  
  
FULL  
O acesso não transacional completo a dados FILESTREAM em FileTables está habilitado.  
  
DIRECTORY_NAME = *\<directory_name>*  
Um nome de diretório compatível com o Windows. Esse nome deve ser exclusivo entre todos os nomes de diretório no nível do banco de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A comparação de exclusividade não diferencia maiúsculas de minúsculas, independentemente das configurações de agrupamento. Essa opção deve ser definida antes da criação de um FileTable neste banco de dados.  
  
**\<HADR_options> ::=**  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
Veja [ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md).  
  
**\<mixed_page_allocation_option> ::=**  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)). 
  
MIXED_PAGE_ALLOCATION { OFF | ON } controla se o banco de dados pode criar páginas iniciais usando uma extensão mista para as primeiras oito páginas de uma tabela ou índice.  
 
OFF  
O banco de dados sempre cria páginas iniciais usando extensões uniformes. Este é o valor padrão.  
  
ON  
O banco de dados pode criar páginas iniciais usando extensões mistas.  
  
Essa configuração está ON para todos os bancos de dados do sistema. **tempdb** é o único banco de dados de sistema compatível com OFF.  
  
**\<PARAMETERIZATION_option> ::=**  
  
Controla a opção de parametrização.  
  
PARAMETERIZATION { SIMPLE | FORCED }  
SIMPLE  
As consultas são parametrizadas com base no comportamento padrão do banco de dados.  
  
FORCED  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parametriza todas as consultas feitas no banco de dados.  
  
A configuração atual dessa opção pode ser determinada examinando-se a coluna is_parameterization_forced na exibição do catálogo sys.databases.  
  
**\<query_store_options> ::=**  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
ON | OFF | CLEAR [ ALL ]  
Controla se o repositório de consultas está habilitado neste banco de dados, além de controlar a remoção de conteúdo do repositório de consultas.  
  
ON  
Habilita o repositório de consultas.  
  
OFF  
Desabilita o repositório de consultas.  Este é o valor padrão.   
  
CLEAR  
Remove o conteúdo do repositório de consultas.  
  
OPERATION_MODE  
Descreve o modo de operação do repositório de consultas. Os valores válidos são READ_ONLY e READ_WRITE. No modo READ_WRITE, o repositório de consultas coleta e persiste as informações das estatísticas de execução do plano de consulta e do tempo de execução. No modo READ_ONLY, as informações podem ser lidas do repositório de consultas, mas novas informações não são adicionadas. Se o espaço máximo alocado do repositório de consultas tiver se esgotado, o repositório de consultas alterará o modo de operação para READ_ONLY.  
  
CLEANUP_POLICY  
Descreve a política de retenção de dados do repositório de consultas. STALE_QUERY_THRESHOLD_DAYS determina o número de dias que as informações de uma consulta são mantidas no repositório de consultas. STALE_QUERY_THRESHOLD_DAYS é do tipo **bigint**.  
  
DATA_FLUSH_INTERVAL_SECONDS  
Determina a frequência na qual os dados gravados no repositório de consultas é persistida no disco. Para otimizar o desempenho, os dados coletados pelo repositório de consultas são gravados de maneira assíncrona no disco. A frequência em que essa transferência assíncrona ocorre é configurada usando o argumento DATA_FLUSH_INTERVAL_SECONDS. DATA_FLUSH_INTERVAL_SECONDS é do tipo **bigint**.  
  
MAX_STORAGE_SIZE_MB  
Determina o espaço alocado para o repositório de consultas. MAX_STORAGE_SIZE_MB é do tipo **bigint**.  
  
INTERVAL_LENGTH_MINUTES  
Determina o intervalo de tempo em que os dados de estatísticas de execução do tempo de execução são agregados no repositório de consultas. Para otimizar o uso de espaço, as estatísticas de execução de tempo de execução no repositório de estatísticas de tempo de execução são agregadas em uma janela de tempo fixo. Essa janela de tempo fixo é configurada usando o argumento INTERVAL_LENGTH_MINUTES. INTERVAL_LENGTH_MINUTES é do tipo **bigint**.  
  
SIZE_BASED_CLEANUP_MODE  
Controla se a limpeza será ativada automaticamente quando a quantidade total de dados se aproximar do tamanho máximo:  
  
OFF  
Limpeza com base no tamanho não será ativada automaticamente. 
  
AUTO  
A limpeza com base em tamanho será ativada automaticamente quando o tamanho em disco atingir 90% do **max_storage_size_mb**. Limpeza com base no tamanho remove as consultas menos dispendiosas e mais antigas primeiro. Ele para a aproximadamente 80% do **max_storage_size_mb**.  Esse é o valor de configuração padrão.  
  
SIZE_BASED_CLEANUP_MODE é do tipo **nvarchar**.  
  
QUERY_CAPTURE_MODE  
Designa o modo de captura de consulta ativo no momento:  
  
ALL Todas as consultas são capturadas. Esse é o valor de configuração padrão.  Esse é o valor de configuração padrão para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]
  
AUTO Captura consultas de relevantes com base na contagem de execução e no consumo de recursos.
  
NONE Parar de capturar novas consultas. O Repositório de Consultas continuará a coletar estatísticas de compilação e tempo de execução para consultas que já foram capturadas. Use essa configuração com cuidado, pois você poderá deixar de capturar consultas importantes.  
  
QUERY_CAPTURE_MODE é do tipo **nvarchar**.  
  
max_plans_per_query  
Um número inteiro que representa a quantidade máxima de planos de manutenção para cada consulta. O padrão é 200.  
  
**\<recovery_option> ::=**  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Controla as opções de recuperação de banco de dados e a verificação de erros de E/S de disco.  
  
FULL  
Fornece recuperação completa depois de falha de mídia usando backups do log de transação. Se um arquivo de dados for danificado, a recuperação de mídia poderá recuperar todas as transações confirmadas. Para saber mais, confira [Modelos de recuperação](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
BULK_LOGGED  
Fornece uma recuperação após uma falha de mídia, combinando o melhor desempenho e a quantidade mínima de uso do espaço de log para determinadas operações em larga escala ou em massa. Para saber mais sobre quais operações podem ser minimamente registradas, veja [O log de transações](../../relational-databases/logs/the-transaction-log-sql-server.md). No modelo de recuperação BULK_LOGGED, o registro para essas operações é mínimo. Para saber mais, confira [Modelos de recuperação](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
SIMPLE  
Uma estratégia simples de backup que usa um espaço de log mínimo é fornecida. O espaço de log poderá ser reutilizado automaticamente quando não for mais necessário à recuperação de falha de servidor. Para saber mais, confira [Modelos de recuperação](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
> [!IMPORTANT]  
> O modelo de recuperação simples é mais fácil de gerenciar que os outros dois modelos, mas às custas de uma exposição maior à perda de dados se um arquivo de dados for danificado. Todas as alterações desde o backup mais recente do banco de dados ou diferencial serão perdidas e terão que ser reinseridas manualmente.  
  
O modelo de recuperação padrão é determinado pelo modelo de recuperação do banco de dados **model** . Para saber mais sobre como selecionar o modelo de recuperação apropriado, veja [Modelos de recuperação](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
O status dessa opção pode ser determinado examinando-se as colunas **recovery_model** e **recovery_model_desc** na exibição do catálogo sys.databases ou a propriedade Recovery da função DATABASEPROPERTYEX.  
  
TORN_PAGE_DETECTION { ON | OFF }  
ON  
Páginas incompletas podem ser detectadas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
OFF  
Páginas incompletas não podem ser detectadas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
> [!IMPORTANT]  
> A estrutura de sintaxe TORN_PAGE_DETECTION ON | OFF será removida em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar essa estrutura de sintaxe em novos trabalhos de desenvolvimentos e planeje modificar os aplicativos que a utilizam atualmente. Use a opção PAGE_VERIFY em seu lugar.  
  
<a name="page_verify"></a> PAGE_VERIFY { CHECKSUM | TORN_PAGE_DETECTION | NONE }  
Descobre páginas de banco de dados danificadas por erros de caminho de E/S do disco. Os erros de caminho de E/S do disco podem ser a causa de problemas de corrompimento de banco de dados e, em geral, são causados por quedas de energia ou falhas no disco que ocorrem no momento da gravação no disco.  
  
CHECKSUM  
Calcula uma soma de verificação com base no conteúdo da página inteira e armazena o valor no cabeçalho da página quando a página é gravada em disco. Quando a página é lida pelo disco, a soma de verificação é recalculada e comparada ao valor da soma de verificação armazenado no cabeçalho da página. Se os valores não forem correspondentes, a mensagem de erro 824 (indicando uma falha na soma de verificação) será informada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e no log de eventos do Windows. Uma falha de soma de verificação indica um problema no caminho de E/S. Para determinar a causa principal, é necessária uma inspeção de hardware, drivers de firmware, BIOS, drivers de filtro (como software antivírus) e outros componentes de caminho de E/S.  
  
TORN_PAGE_DETECTION  
Salva um padrão específico de 2 bits para cada setor de 512 bytes na página de banco de dados de 8 quilobytes (KB) e o armazena no cabeçalho da página do banco de dados quando a página é gravada em disco. Quando a página for lida pelo disco, os bits desativados armazenados no cabeçalho da página serão comparados às informações do setor da página real. Valores não correspondentes indicam que apenas parte da página foi gravada em disco. Nessa situação, a mensagem de erro 824 (indicando um erro de página interrompida) é informada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e no log de eventos do Windows. Páginas interrompidas serão detectadas normalmente através da recuperação de banco de dados se realmente for uma gravação incompleta de uma página. Entretanto, outras falhas de caminho de E/S podem gerar uma página interrompida a qualquer momento.  
  
Nenhuma  
Gravações de páginas de banco de dados não gerarão um valor de CHECKSUM ou de TORN_PAGE_DETECTION. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não verificará uma soma de verificação ou uma página interrompida durante uma leitura, mesmo que um valor de CHECKSUM ou de TORN_PAGE_DETECTION esteja presente no cabeçalho da página.  
  
Considere os seguintes pontos importantes ao usar a opção PAGE_VERIFY:  
  
- O padrão é CHECKSUM.  
- Quando um usuário ou banco de dados do sistema é atualizado para o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior, o valor de PAGE_VERIFY (NONE ou TORN_PAGE_DETECTION) é retido. Recomendamos o uso de CHECKSUM.  
  
    > [!NOTE]  
    > Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a opção de banco de dados PAGE_VERIFY é definida como NONE para o banco de dados tempdb e não pode ser modificada. No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores, o valor padrão do banco de dados tempdb é CHECKSUM para novas instalações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao atualizar uma instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o valor padrão permanece como NONE. A opção pode ser modificada. É recomendável usar CHECKSUM para o banco de dados tempdb.  
  
- TORN_PAGE_DETECTION pode usar menos recursos, mas fornece um subconjunto mínimo da proteção CHECKSUM.  
- PAGE_VERIFY pode ser definido sem que o banco de dados fique offline, seja bloqueado ou a simultaneidade de usuário seja impedida nele.  
- CHECKSUM é mutuamente exclusivo com TORN_PAGE_DETECTION. As duas opções não podem ser habilitadas ao mesmo tempo.  
  
Quando a falha em uma página interrompida ou soma de verificação é detectada, é possível recuperá-las restaurando os dados ou recriando o índice se a falha estiver limitada apenas a páginas de índice. Se você encontrar uma falha de soma de verificação, para determinar o tipo de página de banco de dados ou páginas afetadas, execute DBCC CHECKDB. Para saber mais sobre as opções de restauração, veja [Argumentos de RESTORE](../../t-sql/statements/restore-statements-arguments-transact-sql.md). Embora a restauração de dados resolva o problema de corrupção de dados, sua causa, por exemplo, falha do hardware de disco, deve ser diagnosticada e corrigida assim que possível para evitar a repetição dos erros.  
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] repetirá mais quatro vezes qualquer leitura que falhe com uma soma de verificação, página interrompida ou outro erro de E/S. Se a leitura tiver êxito em qualquer uma das novas tentativas, uma mensagem será gravada no log de erros e o comando que disparou a leitura continuará. Se as novas tentativas falharem, o comando falhará com a mensagem de erro 824.  
  
Para obter mais informações sobre mensagens de erro 823, 824 e 825, veja [Como solucionar uma mensagem de erro 823 no SQL Server](http://support.microsoft.com/help/2015755), [Como solucionar a mensagem de erro 824 no SQL Server](http://support.microsoft.com/help/2015756) e [Como solucionar a mensagem de erro 825 &#40;repetição de leitura&#41; no SQL Server](http://support.microsoft.com/help/2015757).
  
A configuração atual dessa opção pode ser determinada examinando a coluna *page_verify_option* na exibição do catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) ou a propriedade *IsTornPageDetectionEnabled* da função [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md).  
  
**\<remote_data_archive_option> ::=**  
 
**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
Habilita ou desabilita o Stretch Database para o banco de dados. Para obter mais informações, consulte [Stretch Database](../../sql-server/stretch-database/stretch-database.md).  
  
REMOTE_DATA_ARCHIVE = { ON ( SERVER = \<server_name>, { CREDENTIAL = \<db_scoped_credential_name> | FEDERATED_SERVICE_ACCOUNT = ON | OFF } )| OFF ON  
Habilita o Stretch Database para o banco de dados. Para obter mais informações, incluindo os pré-requisitos adicionais, veja [Habilitar o Stretch Database para um banco de dados](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
**Permissões**. Habilitar o Stretch Database para um banco de dados ou uma tabela exige permissões db_owner. Habilitar o Stretch Database para um banco de dados também exige permissões CONTROL DATABASE.  
  
SERVER = \<server_name>  
Especifica o endereço do servidor do Azure. Inclua a parte `.database.windows.net` do nome. Por exemplo, `MyStretchDatabaseServer.database.windows.net`.  
  
CREDENTIAL = \<db_scoped_credential_name>  
Especifica a credencial no escopo do banco de dados que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa para se conectar ao servidor do Azure. Verifique se que a credencial existe antes de executar esse comando. Para saber mais, confira [CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  
  
FEDERATED_SERVICE_ACCOUNT = ON | OFF  
Você pode usar uma conta de serviço federado para o SQL Server local se comunicar com o servidor remoto do Azure quando todas as condições a seguir forem verdadeiras.  
  
- A conta do serviço na qual a instância do SQL Server está sendo executada é uma conta de domínio.  
- A conta de domínio pertence a um domínio cujo Active Directory é federado com o Azure Active Directory.  
- O servidor remoto do Azure está configurado para permitir a autenticação do Azure Active Directory.  
- A conta de serviço na qual a instância do SQL Server está sendo executada deve ser configurada como uma conta dbmanager ou sysadmin no servidor remoto do Azure.  
  
Se você especificar ON, não poderá também especificar o argumento CREDENTIAL. Se você especificar OFF, precisará fornecer o argumento CREDENTIAL.  
  
OFF  
Desabilita o Stretch Database para o banco de dados. Para obter mais informações, consulte [Desabilitar Stretch Database e trazer de volta dados remotos](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md).  
  
Você só pode desabilitar o Stretch Database para um banco de dados depois que o banco de dados não contiver nenhuma tabela habilitada para o Stretch Database. Depois de desabilitar o Stretch Database, a migração de dados é interrompida e os resultados da consulta não incluem mais resultados das tabelas remotas.  
  
Desabilitar o Stretch não remove o banco de dados remoto. Se você quiser excluir o banco de dados remoto, descarte-o usando o Portal do Azure.  
  
**\<service_broker_option> ::=**  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
Controla as seguintes opções do [!INCLUDE[ssSB](../../includes/sssb-md.md)]: habilita ou desabilita a entrega de mensagens, define um novo identificador do [!INCLUDE[ssSB](../../includes/sssb-md.md)] ou define as prioridades de conversa como ON ou OFF.  
  
ENABLE_BROKER  
Especifica que o [!INCLUDE[ssSB](../../includes/sssb-md.md)] está habilitado para o banco de dados especificado. A entrega de mensagens é iniciada e o sinalizador is_broker_enabled é definido como true na exibição do catálogo sys.databases. O banco de dados retém o identificador do [!INCLUDE[ssSB](../../includes/sssb-md.md)] existente. O Service Broker não pode ser habilitado quando o banco de dados é a entidade de segurança em uma configuração de espelhamento de banco de dados.  
  
> [!NOTE]  
>  ENABLE_BROKER requer um bloqueio de banco de dados exclusivo. Se outras sessões bloquearam recursos no banco de dados, ENABLE_BROKER esperará até que as outras sessões liberem os bloqueios. Para habilitar o [!INCLUDE[ssSB](../../includes/sssb-md.md)] em um banco de dados de usuário, verifique se nenhuma outra sessão está usando o banco de dados antes de executar a instrução ALTER DATABASE SET ENABLE_BROKER, por exemplo, colocando o banco de dados no modo de usuário único. Para habilitar o [!INCLUDE[ssSB](../../includes/sssb-md.md)] no banco de dados msdb, primeiro interrompe o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para que o [!INCLUDE[ssSB](../../includes/sssb-md.md)] possa obter o bloqueio necessário.  
  
DISABLE_BROKER  
Especifica que o [!INCLUDE[ssSB](../../includes/sssb-md.md)] está desabilitado para o banco de dados especificado. A entrega de mensagens é interrompida e o sinalizador is_broker_enabled é definido como false na exibição do catálogo sys.databases. O banco de dados retém o identificador do [!INCLUDE[ssSB](../../includes/sssb-md.md)] existente.  
  
NEW_BROKER  
Especifica que o banco de dados deve receber um novo identificador do Broker. Como o banco de dados é considerado como um novo Service Broker, todas as conversas existentes nele são imediatamente removidas sem produzir mensagens de caixa de diálogo de término. Qualquer rota que referencia o antigo identificador do [!INCLUDE[ssSB](../../includes/sssb-md.md)] deve ser recriada novamente com o novo identificador.  
  
ERROR_BROKER_CONVERSATIONS  
Especifica que a entrega de mensagens do [!INCLUDE[ssSB](../../includes/sssb-md.md)] está habilitada. Isso preserva o identificador [!INCLUDE[ssSB](../../includes/sssb-md.md)] existente para o banco de dados. [!INCLUDE[ssSB](../../includes/sssb-md.md)] termina todas as conversas no banco de dados com um erro. Isso permite que os aplicativos executem a limpeza regular das conversas existentes.  
  
HONOR_BROKER_PRIORITY {ON | OFF}  
ON  
As operações de envio levam em conta os níveis de prioridade atribuídos às conversas. As mensagens de conversas com altos níveis de prioridade são enviadas antes das mensagens de conversas com baixos níveis de prioridade atribuídos.  
  
OFF  
As operações de envio são executadas como se todas as conversas tivessem o nível de prioridade padrão.  
  
As alterações na opção HONOR_BROKER_PRIORITY entram em vigor imediatamente para os novos diálogos ou diálogos que não tenham mensagens esperando para serem enviadas. As caixas de diálogo com mensagens esperando para serem enviadas quando ALTER DATABASE for executado não assumirão a nova configuração até que algumas das mensagens da caixa de diálogo sejam enviadas. O tempo necessário para que todas as caixas de diálogo comecem a usar a nova configuração pode variar consideravelmente.  
  
A configuração atual dessa propriedade é relatada na coluna is_broker_priority_honored da exibição do catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
 
**\<snapshot_option> ::=**  
  
Determina o nível de isolamento da transação.  
  
ALLOW_SNAPSHOT_ISOLATION { ON | OFF }  
ON  
Habilita a opção de Instantâneo no nível do banco de dados. Quando habilitada, as instruções DML começam a gerar versões de linha mesmo quando nenhuma transação usar Isolamento de Instantâneo. Quando essa opção está habilitada, as transações podem especificar o nível de isolamento da transação SNAPSHOT. Ao executar uma transação no nível de isolamento SNAPSHOT, todas as instruções consultam um instantâneo de dados, se houver um no início da instrução. Se uma transação que executa no nível de isolamento SNAPSHOT acessar dados em vários bancos de dados, ALLOW_SNAPSHOT_ISOLATION deverá ser definido como ON em todos os bancos de dados ou cada instrução na transação deverá usar dicas de bloqueio em qualquer referência em uma cláusula FROM para uma tabela em um banco de dados onde ALLOW_SNAPSHOT_ISOLATION seja OFF.  
  
OFF  
Desativa a opção de Instantâneo no nível do banco de dados. As transações não podem especificar o nível de isolamento da transação SNAPSHOT.  
  
Ao definir ALLOW_SNAPSHOT_ISOLATION para um novo estado (de ON para OFF, ou de OFF, para ON), ALTER DATABASE não retorna o controle para o chamador até que todas as transações existentes no banco de dados sejam confirmadas. Se o banco de dados já estiver no estado especificado na instrução ALTER DATABASE, o controle será retornado ao chamador imediatamente. Se a instrução ALTER DATABASE não for retornada rapidamente, use [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) para determinar se há transações de longa duração. Se a instrução ALTER DATABASE for cancelada, o banco de dados permanecerá no estado que estava quando ALTER DATABASE foi iniciada. A exibição do catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) indica o estado de transações de isolamento de instantâneo no banco de dados. Se **snapshot_isolation_state_desc** = IN_TRANSITION_TO_ON, ALTER DATABASE ALLOW_SNAPSHOT_ISOLATION OFF fará uma pausa de seis segundos e tentará novamente executar a operação.  
  
Não é possível alterar o estado de ALLOW_SNAPSHOT_ISOLATION se o banco de dados for OFFLINE.  
  
Se você definir ALLOW_SNAPSHOT_ISOLATION em um banco de dados READ_ONLY, a configuração será retida se o banco de dados for definido mais tarde como READ_WRITE.  
  
É possível alterar as configurações ALLOW_SNAPSHOT_ISOLATION para os bancos de dados mestre, modelo, msdb e tempdb. Se você alterar a configuração para tempdb, ela será retida sempre que a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] for interrompida e reiniciada. Ao alterar a configuração para modelo, ela se tornará o padrão para qualquer novo banco de dados que for criado, exceto para tempdb.  
  
A opção é ON, por padrão, para os bancos de dados mestre e msdb.  
  
A configuração atual dessa opção pode ser determinada examinando-se a coluna snapshot_isolation_state na exibição do catálogo sys.databases.  
  
READ_COMMITTED_SNAPSHOT { ON | OFF }  
ON  
Habilita a opção de Instantâneo de Leitura Confirmada no nível do banco de dados. Quando habilitada, as instruções DML começam a gerar versões de linha mesmo quando nenhuma transação usar Isolamento de Instantâneo. Quando essa opção está habilitada, as transações que especificam o nível de isolamento de leitura confirmada usam o controle de versão de linha, em vez de bloqueio. Quando uma transação é executada no nível de isolamento de leitura confirmada, todas as instruções consultam um instantâneo de dados, se houver um no início da instrução.  
  
OFF  
Desabilita a opção de Instantâneo de Leitura Confirmada no nível do banco de dados. As transações que especificam o nível de isolamento READ COMMITTED usam bloqueio.  
  
Para definir READ_COMMITTED_SNAPSHOT como ON ou OFF, não deve haver nenhuma conexão ativa com o banco de dados exceto para a que está executando o comando ALTER DATABASE. Entretanto, o banco de dados não precisa estar no modo de usuário único. Não é possível alterar o estado dessa opção quando o banco de dados for OFFLINE.  
  
Se você definir READ_COMMITTED_SNAPSHOT em um banco de dados READ_ONLY, a configuração será retida quando o banco de dados for definido mais tarde como READ_WRITE.  
  
READ_COMMITTED_SNAPSHOT não pode ser ativado como ON para os bancos de dados do sistema mestre, tempdb ou msdb. Se você alterar a configuração para modelo, ela se tornará o padrão para qualquer novo banco de dados que for criado, exceto para tempdb.  
  
A configuração atual dessa opção pode ser determinada examinando-se a coluna is_read_committed_snapshot_on na exibição do catálogo sys.databases.  
  
> [!WARNING]  
>  Quando uma tabela for criada com **DURABILITY = SCHEMA_ONLY**, e **READ_COMMITTED_SNAPSHOT** depois forem alterado usando **ALTER DATABASE**, os dados na tabela serão perdidos.  
  
MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT { ON | OFF }  
**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
ON  
Quando o nível de isolamento da transação estiver configurado para qualquer nível de isolamento inferior ao SNAPSHOT (por exemplo, READ COMMITTED ou READ UNCOMMITTED), todas as operações interpretadas de [!INCLUDE[tsql](../../includes/tsql-md.md)] em tabelas com otimização de memória serão executadas em isolamento SNAPSHOT. Isso é feito mesmo que o nível de isolamento da transação seja definido explicitamente no nível de sessão ou se a opção for usada implicitamente.  
  
OFF  
Não eleva o nível de isolamento da transação para operações interpretadas do [!INCLUDE[tsql](../../includes/tsql-md.md)] em tabelas com otimização de memória.  
  
Não é possível alterar o estado de MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT se o banco de dados for OFFLINE.  
  
A opção é OFF, por padrão.  
  
A configuração atual dessa opção pode ser determinada, examinando a coluna **is_memory_optimized_elevate_to_snapshot_on** na exibição de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
**\<sql_option> ::=**  
  
Controla as opções de conformidade ANSI no nível de banco de dados.  
  
ANSI_NULL_DEFAULT { ON | OFF }  
Determina o valor padrão, NULL ou NOT NULL, de um [tipo definido pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) CLR ou coluna para o qual a nulidade não é definida explicitamente nas instruções CREATE TABLE ou ALTER TABLE. As colunas definidas com restrições seguem as regras de restrição apesar dessa configuração.  
  
ON  
O valor padrão é NULL.  
  
OFF  
O valor padrão é NOT NULL.  
  
As configurações no nível de conexão que são definidas com o uso de uma instrução SET substituem a configuração no nível de banco de dados padrão para ANSI_NULL_DEFAULT. Por padrão, clientes ODBC e OLE DB emitem uma configuração ANSI_NULL_DEFAULT de instrução SET no nível de conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET ANSI_NULL_DFLT_ON](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md).  
  
Para compatibilidade ANSI, definir a opção de banco de dados ANSI_NULL_DEFAULT como ON altera o banco de dados padrão para NULL.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_ansi_null_default_on na exibição do catálogo sys.databases ou a propriedade IsAnsiNullDefault da função DATABASEPROPERTYEX.  
  
ANSI_NULLS { ON | OFF }  
ON  
Todas as comparações com um valor nulo são avaliadas como UNKNOWN.  
  
OFF  
As comparações de valores não UNICODE com um valor nulo são avaliadas como TRUE se ambos os valores forem NULL.  
  
> [!IMPORTANT]  
>  Em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ANSI_NULLS sempre estará ON e quaisquer aplicativos que definam explicitamente a opção como OFF produzirão um erro. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
As configurações no nível de conexão que são definidas com o uso de uma instrução SET substituem a configuração no nível de banco de dados padrão para ANSI_NULLS. Por padrão, clientes ODBC e OLE DB emitem uma configuração ANSI_NULLS de instrução SET no nível de conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET ANSI_NULLS](../../t-sql/statements/set-ansi-nulls-transact-sql.md).  
  
SET ANSI_NULLS também deve ser definido como ON ao criar ou fazer alterações em índices em colunas computadas ou exibições indexadas.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_ansi_nulls_on na exibição do catálogo sys.databases ou a propriedade IsAnsiNullsEnabled da função DATABASEPROPERTYEX.  
  
ANSI_PADDING { ON | OFF }  
ON  
As cadeias de caracteres são preenchidas com o mesmo comprimento antes da conversão ou inserção em um tipo de dados **varchar** ou **nvarchar**.  
  
Espaços em branco à direita nos valores de caracteres inseridos nas colunas **varchar** ou **nvarchar** e os zeros à direita nos valores binários inseridos nas colunas **varbinary** não serão cortados. Os valores não são preenchidos com o tamanho da coluna.  
  
OFF  
Espaços em branco à direita para **varchar** ou **nvarchar** e zeros para **varbinary** são cortados.  
  
Quando OFF é especificado, essa configuração afeta apenas a definição de novas colunas.  
  
> [!IMPORTANT]  
>  Em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ANSI_PADDING sempre será ON e quaisquer aplicativos que definam explicitamente a opção como OFF produzirão um erro. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. É recomendável sempre definir ANSI_PADDING como ON. ANSI_PADDING deve ser ON ao criar ou manipular índices em colunas computadas ou exibições indexadas.  
  
As colunas **char(*n*)** e **binary(*n*)** que permitem valores nulos são preenchidas até o tamanho da coluna quando ANSI_PADDING está definido como ON, mas os brancos à direita e os zeros são cortados quando ANSI_PADDING está definido como OFF. As colunas **char(*n*)** e **binary(*n*)** que não permitem valores nulos sempre são preenchidas até o tamanho da coluna.  
  
As configurações no nível de conexão que são definidas com o uso de uma instrução SET substituem a configuração no nível de banco de dados padrão para ANSI_PADDING. Por padrão, clientes ODBC e OLE DB emitem uma configuração ANSI_PADDING da instrução SET no nível da conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET ANSI_PADDING](../../t-sql/statements/set-ansi-padding-transact-sql.md).  
  
O status dessa opção pode ser determinado examinando-se a coluna is_ansi_padding_on na exibição do catálogo sys.databases ou a propriedade IsAnsiPaddingEnabled da função DATABASEPROPERTYEX.  
  
ANSI_WARNINGS { ON | OFF }  
ON  
Erros ou avisos são emitidos quando condições como “divisão por zero” ou “valores nulos” aparecerem em funções de agregação.  
  
OFF  
Nenhum aviso é emitido e os valores nulos são retornados quando condições como “dividir por zero” ocorrem.  
  
SET ANSI_WARNINGS também deve ser definido como ON ao criar ou fazer alterações em índices em colunas computadas ou exibições indexadas.  
  
As configurações no nível de conexão que são definidas usando uma instrução SET substituem a configuração no nível de banco de dados padrão para ANSI_WARNINGS. Por padrão, clientes ODBC e OLE DB emitem uma configuração ANSI_WARNINGS de instrução SET no nível de conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET ANSI_PADDING](../../t-sql/statements/set-ansi-warnings-transact-sql.md).  
  
O status dessa opção pode ser determinado examinando-se a coluna is_ansi_warnings_on na exibição do catálogo sys.databases ou a propriedade IsAnsiWarningsEnabled da função DATABASEPROPERTYEX.  
  
ARITHABORT { ON | OFF }  
ON  
Uma consulta é encerrada quando ocorre um estouro ou erro de divisão por zero durante a execução da consulta.  
  
OFF  
Uma mensagem de aviso é exibida quando um desses erros ocorre, mas a consulta, o lote ou a transação continuam a ser processados como se nenhum erro tivesse ocorrido.  
  
SET ARITHABORT também deve ser definido como ON ao criar ou fazer alterações em índices em colunas computadas ou exibições indexadas.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_arithabort_on na exibição do catálogo sys.databases ou a propriedade IsArithmeticAbortEnabled da função DATABASEPROPERTYEX.  
  
COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 | 90 }   
Para saber mais, confira [ALTER DATABASE Compatibility Level](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
CONCAT_NULL_YIELDS_NULL { ON | OFF }  
ON  
O resultado de uma operação de concatenação será NULL quando qualquer operando for NULL. Por exemplo, concatenar a cadeia de caracteres "This is" e NULL gera o valor NULL, em vez do valor "This is".  
  
OFF  
O valor nulo é tratado como uma cadeia de caracteres vazia.  
  
CONCAT_NULL_YIELDS_NULL deve ser definido como ON ao criar ou fazer alterações em índices em colunas computadas ou exibições indexadas.  
  
> [!IMPORTANT]  
>  Em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], CONCAT_NULL_YIELDS_NULL sempre estará ON e quaisquer aplicativos que definam explicitamente a opção como OFF produzirão um erro. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
As configurações no nível de conexão que são definidas usando uma instrução SET substituem a configuração no nível de banco de dados padrão para CONCAT_NULL_YIELDS_NULL. Por padrão, clientes ODBC e OLE DB emitem uma configuração CONCAT_NULL_YIELDS_NULL de instrução SET no nível de conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET CONCAT_NULL_YIELDS_NULL](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).  
  
O status dessa opção pode ser determinado examinando-se a coluna is_concat_null_yields_null_on na exibição do catálogo sys.databases ou a propriedade IsNullConcat da função DATABASEPROPERTYEX.  
  
QUOTED_IDENTIFIER { ON | OFF }  
ON  
As aspas duplas podem ser utilizadas para conter identificadores delimitados.  
  
Todas as cadeias de caracteres delimitadas por aspas duplas são interpretadas como identificadores de objeto. Os identificadores entre aspas não precisam seguir as regras [!INCLUDE[tsql](../../includes/tsql-md.md)] para identificadores. Eles podem ser palavras-chave e incluir caracteres geralmente não permitidos nos identificadores [!INCLUDE[tsql](../../includes/tsql-md.md)]. Se o sinal de aspas simples (') fizer parte da cadeia de caracteres literal, ele poderá ser representado por aspas duplas (").  
  
OFF  
Os identificadores não podem estar entre aspas e devem seguir todas as regras de identificadores [!INCLUDE[tsql](../../includes/tsql-md.md)]. Literais podem ser delimitados por aspas simples ou duplas.  
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também permite que os identificadores sejam delimitados por colchetes ([ ]). Os identificadores entre colchetes podem sempre ser usados, seja qual for a configuração de QUOTED_IDENTIFIER. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
Quando uma tabela é criada, a opção QUOTED IDENTIFIER sempre é armazenada como ON nos metadados da tabela, mesmo que a opção esteja definida como OFF quando a tabela é criada.  
  
As configurações no nível de conexão que são definidas com o uso de uma instrução SET substituem a configuração no nível de banco de dados padrão para QUOTED_IDENTIFIER. Por padrão, clientes ODBC e OLE DB emitem uma configuração QUOTED_IDENTIFIER de instrução SET no nível de conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
O status dessa opção pode ser determinado examinando-se a coluna is_quoted_identifier_on na exibição do catálogo sys.databases ou a propriedade IsQuotedIdentifiersEnabled da função DATABASEPROPERTYEX.  
  
NUMERIC_ROUNDABORT { ON | OFF }  
ON  
Um erro é gerado quando ocorre perda de precisão em uma expressão.  
  
OFF  
As perdas de precisão não geram mensagens de erro e o resultado é arredondado de acordo com a precisão da coluna ou variável que armazena o resultado.  
  
NUMERIC_ROUNDABORT deve ser definido como OFF ao criar ou fazer alterações em índices em colunas computadas ou exibições indexadas.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_numeric_roundabort_on na exibição do catálogo sys.databases ou a propriedade IsNumericRoundAbortEnabled da função DATABASEPROPERTYEX.  
  
RECURSIVE_TRIGGERS { ON | OFF }  
ON  
O disparo recursivo de gatilhos AFTER é permitido.  
  
OFF  
Apenas o disparo recursivo direto de gatilhos AFTER não é permitido. Para desabilitar também a recursão indireta de gatilhos AFTER, defina a opção do servidor de gatilhos aninhados como **0** usando **sp_configure**.  
  
> [!NOTE]  
>  Somente a recursão direta será evitada quando RECURSIVE_TRIGGERS estiver definido como OFF. Para desabilitar a recursão indireta, é necessário definir também a opção do servidor nested triggers como 0.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_recursive_triggers_on na exibição do catálogo sys.databases ou a propriedade IsRecursiveTriggersEnabled da função DATABASEPROPERTYEX.  
  
**\<target_recovery_time_option> ::=**  
  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Especifica a frequência de pontos de verificação indiretos por banco de dados. Começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o valor padrão para novos bancos de dados é de 1 minuto, o que indica que o banco de dados usará pontos de verificação indiretos. Para versões mais antigas, o padrão é 0, o que indica que o banco de dados usará pontos de verificação automáticos cuja frequência depende da configuração do intervalo de recuperação da instância de servidor. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda 1 minuto para a maioria dos sistemas.  
  
TARGET_RECOVERY_TIME **=***target_recovery_time* { SECONDS | MINUTES }  
*target_recovery_time*  
Especifica o salto máximo no tempo para recuperar o banco de dados especificado no caso de uma falha.  
  
SECONDS  
Indica que *target_recovery_time* é expresso como o número de segundos.  
  
MINUTES  
Indica que *target_recovery_time* é expresso como o número de minutos.  
  
Para saber mais sobre pontos de verificação indiretos, confira [Pontos de verificação de banco de dados](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
**WITH \<termination> ::=**  
  
Especifica quando reverter transações incompletas quando há transição do banco de dados de um estado para outro. Se a cláusula de término for omitida, a instrução ALTER DATABASE aguardará indefinidamente se houver algum bloqueio no banco de dados. Somente uma cláusula de término pode ser especificada e ela sucede as cláusulas SET.  
  
> [!NOTE]  
>  Nem todas as opções de banco de dados usam a cláusula WITH \<termination>. Para saber mais, confira a tabela em[Opções de configuração](#SettingOptions) na seção Comentários deste artigo.  
  
ROLLBACK AFTER *integer* [SECONDS] | ROLLBACK IMMEDIATE  
Especifica se a reversão deve ser feita após o número de segundos especificado ou imediatamente.  
  
NO_WAIT  
Especifica que, se a alteração de estado do banco de dados ou da opção solicitada não puder ser concluída imediatamente sem esperar que as transações sejam confirmadas ou revertidas por si mesmas, a solicitação falhará.  
  
##  <a name="SettingOptions"></a> Opções de configuração  
Para recuperar as configurações atuais das opções de banco de dados, use a exibição do catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) ou [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)  
  
Depois de definir uma opção de banco de dados, a modificação entra em vigor imediatamente.  
  
Para alterar os valores padrão de qualquer uma das opções de banco de dados para todos os bancos de dados criados recentemente, altere a opção de banco de dados apropriada no banco de dados modelo.  
  
Nem todas as opções de banco de dados usam a cláusula WITH \<termination> ou podem ser especificadas em combinação com outras opções. A tabela a seguir lista essas opções e seu status de opção e término.  
  
|Categoria de opções|Pode ser especificado com outras opções|Pode usar a cláusula WITH \<termination>|  
|----------------------|-----------------------------------------|---------------------------------------------|  
|\<db_state_option>|Sim|Sim|  
|\<db_user_access_option>|Sim|Sim|  
|\<db_update_option>|Sim|Sim|  
|\<delayed_durability_option>|Sim|Sim|  
|\<external_access_option>|Sim|não|  
|\<cursor_option>|Sim|não|  
|\<auto_option>|Sim|não|  
|\<sql_option>|Sim|não|  
|\<recovery_option>|Sim|não|  
|\<target_recovery_time_option>|não|Sim|  
|\<database_mirroring_option>|não|não|  
|ALLOW_SNAPSHOT_ISOLATION|não|não|  
|READ_COMMITTED_SNAPSHOT|não|Sim|  
|MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT|Sim|Sim|  
|\<service_broker_option>|Sim|não|  
|DATE_CORRELATION_OPTIMIZATION|Sim|Sim|  
|\<parameterization_option>|Sim|Sim|  
|\<change_tracking_option>|Sim|Sim|  
|\<db_encryption_option>|Sim|não|  
  
O cache de planos da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é limpo com a definição de uma das seguintes opções:  
  
|||  
|-|-|  
|OFFLINE|READ_WRITE|  
|ONLINE|MODIFY FILEGROUP DEFAULT|  
|MODIFY_NAME|MODIFY FILEGROUP READ_WRITE|  
|COLLATE|MODIFY FILEGROUP READ_ONLY|  
|READ_ONLY||  
  
O cache de procedimento também é liberado nos seguintes cenários.  
  
- Um banco de dados tem a opção de banco de dados AUTO_CLOSE definida como ON. Quando nenhuma conexão de usuário fizer referência ou usar o banco de dados, a tarefa de banco de dados tentará fechar e encerrar o banco de dados automaticamente.  
- Execute diversas consultas em um banco de dados que tem opções padrão. O banco de dados é removido.  
- Um instantâneo de banco de dados para um banco de dados de origem é removido.  
- Você recria com sucesso o log de transação para um banco de dados.  
- Você restaura um backup de banco de dados.  
-   Você desanexa um banco de dados.  
  
A limpeza do cache de planos gera uma recompilação de todos os planos de execução subsequentes e pode provocar uma redução repentina e temporária do desempenho de consultas. Para cada armazenamento em cache limpo no cache de planos, o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém a seguinte mensagem informativa: "O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou %d ocorrência(s) de liberação de armazenamento em cache '% s' (parte do cache de planos) devido à manutenção do banco de dados ou operações de reconfiguração". Essa mensagem é registrada a cada cinco minutos, contanto que o cache seja liberado dentro desse intervalo de tempo.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-setting-options-on-a-database"></a>A. Configurando opções em um banco de dados  
O exemplo a seguir define o modelo de recuperação e as opções de verificação de página de dados para o banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY FULL PAGE_VERIFY CHECKSUM;  
GO  
  
```  
  
### <a name="b-setting-the-database-to-readonly"></a>B. Configurando o banco de dados como READ_ONLY  
Alterar o estado de um banco de dados ou grupo de arquivos para READ_ONLY ou READ_WRITE requer acesso exclusivo ao banco de dados. O exemplo a seguir define o banco de dados como o modo `SINGLE_USER` para obter acesso exclusivo. Em seguida, o exemplo define o estado do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] como `READ_ONLY` e retorna o acesso ao banco de dados para todos os usuários.  
  
> [!NOTE]  
>  Este exemplo usa a opção de término `WITH ROLLBACK IMMEDIATE` na primeira instrução `ALTER DATABASE` . Todas as transações incompletas serão revertidas e qualquer outra conexão com o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] será desconectada imediatamente.  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET SINGLE_USER  
WITH ROLLBACK IMMEDIATE;  
GO  
ALTER DATABASE AdventureWorks2012  
SET READ_ONLY  
GO  
ALTER DATABASE AdventureWorks2012  
SET MULTI_USER;  
GO  
  
```  
  
### <a name="c-enabling-snapshot-isolation-on-a-database"></a>C. Habilitando o isolamento de instantâneo em um banco de dados  
O exemplo a seguir habilita a opção de estrutura de isolamento de instantâneo para o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
USE AdventureWorks2012;  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET ALLOW_SNAPSHOT_ISOLATION ON;  
GO  
-- Check the state of the snapshot_isolation_framework  
-- in the database.  
SELECT name, snapshot_isolation_state,   
    snapshot_isolation_state_desc AS description  
FROM sys.databases  
WHERE name = N'AdventureWorks2012';  
GO  
  
```  
  
O conjunto de resultados mostra que a estrutura de isolamento de instantâneo está habilitada.  
  
|NAME |snapshot_isolation_state |descrição|  
|-------------------- |------------------------  |----------|  
|AdventureWorks2012   |1                        | ON |  
  
### <a name="d-enabling-modifying-and-disabling-change-tracking"></a>D. Habilitando, modificando e desabilitando o controle de alterações  
O exemplo a seguir habilita o controle de alterações no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e define o período de retenção para `2` dias.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = ON  
(AUTO_CLEANUP = ON, CHANGE_RETENTION = 2 DAYS);  
```  
  
O exemplo a seguir mostra como alterar o período de retenção para `3` dias.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING (CHANGE_RETENTION = 3 DAYS);  
```  
  
O exemplo a seguir mostra como desabilitar o controle de alterações no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = OFF;  
```  
  
### <a name="e-enabling-the-query-store"></a>E. Habilitando o repositório de consultas  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
O exemplo a seguir habilita o repositório de consultas e configura os parâmetros do repositório de consultas.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET QUERY_STORE = ON   
    (  
      OPERATION_MODE = READ_WRITE   
    , CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 )  
    , DATA_FLUSH_INTERVAL_SECONDS = 900   
    , MAX_STORAGE_SIZE_MB = 1024   
    , INTERVAL_LENGTH_MINUTES = 60   
    );  
```  
  
## <a name="see-also"></a>Consulte Também  
[Nível de compatibilidade de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
[Espelhamento de banco de dados de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
[ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
[Estatística](../../relational-databases/statistics/statistics.md)   
[CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqlserver)   
[Habilitar e desabilitar o controle de alterações](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)   
[DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)   
[DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)   
[SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
[sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
[Melhor prática com o Repositório de Consultas](../../relational-databases/performance/best-practice-with-the-query-store.md) 
  
::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> <table>
> <tr>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
> </tr>
> <tr>
>   <th><a href="alter-database-transact-sql.md?view=sql-server-2016">SQL Server</a></th>
>   <th><strong><em>* SQL Server *<br />&nbsp;</em></strong></th>
>   <th><a href="alter-database-transact-sql-set-options.md?view=azuresqldb-current">Banco de Dados SQL<br />Banco de Dados SQL</a></th>
>   <th><a href="alter-database-transact-sql-set-options.md?view=azuresqldb-mi-current">Banco de Dados SQL<br />Banco de Dados SQL</a></th>
> </tr>
> </table>

&nbsp;

# <a name="azure-sql-database-logical-server"></a>Servidor lógico do Banco de Dados SQL do Azure
Níveis de compatibilidade são opções `SET`, mas são descritas em [Nível de Compatibilidade de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
> [!NOTE]  
> Muitas opções de definição de banco de dados podem ser configuradas para a sessão atual usando [Instruções SET](../../t-sql/statements/set-statements-transact-sql.md) e são configuradas com frequência por aplicativos quando eles são conectados. As opções definidas no nível de sessão substituem os valores de **ALTER DATABASE SET** . As opções de banco de dados descritas abaixo são os valores que podem ser definidos para as sessões que não fornecem explicitamente outros valores de definição de conjunto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ALTER DATABASE { database_name | Current }  
SET   
{  
    <option_spec> [ ,...n ] [ WITH <termination> ]   
}  
;  

<option_spec> ::=
{  
    <auto_option>
  | <automatic_tuning_option>
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
;  
<auto_option> ::= 
{  
    AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] } 
  | AUTO_SHRINK { ON | OFF } 
  | AUTO_UPDATE_STATISTICS { ON | OFF } 
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
}

<automatic_tuning_option> ::=  
{   AUTOMATIC_TUNING = { AUTO | INHERIT | CUSTOM } 
  | AUTOMATIC_TUNING ( CREATE_INDEX = { DEFAULT | ON | OFF } )
  | AUTOMATIC_TUNING ( DROP_INDEX = { DEFAULT | ON | OFF } )
  | AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = { DEFAULT | ON | OFF } )
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
  | COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 }   
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

## <a name="arguments"></a>Argumentos  
*database_name*  
É o nome do banco de dados a ser modificado.  
  
CURRENT  
`CURRENT` executa a ação no banco de dados atual. `CURRENT` não é compatível com todas as opções em todos os contextos. Se `CURRENT` falhar, forneça o nome do banco de dados. 
  
**\<auto_option> ::=**
  
Controla opções automáticas.  
<a name="auto_create_statistics"></a> AUTO_CREATE_STATISTICS { ON | OFF }  
ON  
O otimizador de consulta cria estatísticas em colunas únicas em predicados de consulta, conforme necessário, para melhorar planos e desempenho de consulta. Estas estatísticas de coluna única são criadas quando o otimizador de consulta compila consultas. As estatísticas de coluna única só são criadas em colunas que ainda não são a primeira de um objeto de estatísticas existente.  
  
O padrão é ON. Nós recomendamos que você use a configuração padrão para a maioria dos bancos de dados.  
  
OFF  
O otimizador de consulta não cria estatísticas em colunas únicas em predicados de consulta quando estiver compilando consultas. Definir essa opção como OFF pode acarretar planos de consulta de qualidade inferior e menor desempenho de consulta.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_create_stats_on na exibição do catálogo sys.databases ou a propriedade IsAutoCreateStatistics da função DATABASEPROPERTYEX.  
  
Para obter mais informações, veja a seção “Usando as opções de estatísticas em todo o banco de dados” em [Estatística](../../relational-databases/statistics/statistics.md).  
  
INCREMENTAL = ON | OFF  
Quando AUTO_CREATE_STATISTICS estiver ON e INCREMENTAL estiver definido como ON, as estatísticas criadas automaticamente são criadas como incrementais sempre que as estatísticas incrementais tiverem suporte. O valor padrão é OFF. Para saber mais, veja [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md).  
  
<a name="auto_shrink"></a> AUTO_SHRINK { ON | OFF }  
ON  
Os arquivos de banco de dados são candidatos à redução periódica.  
  
Arquivos de dados e arquivos de log podem ser reduzidos automaticamente. AUTO_SHRINK reduzirá o tamanho do log de transações somente se o banco de dados estiver definido como modelo de recuperação SIMPLE ou se foi feito backup do log. Quando definido como OFF, os arquivos de banco de dados não são reduzidos automaticamente durante as verificações periódicas de espaço não utilizado.  
  
A opção AUTO_SHRINK faz com que os arquivos sejam reduzidos quando mais que 25% do arquivo contém espaço não utilizado. O arquivo é reduzido de forma que 25% de seu tamanho seja de espaço não utilizado ou ele tenha o mesmo tamanho de quando foi criado, o que for maior.  
  
Não é possível reduzir um banco de dados somente leitura.  
  
OFF  
Os arquivos de banco de dados não são reduzidos automaticamente durante as verificações periódicas de espaço não utilizado.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_auto_shrink_on na exibição do catálogo sys.databases ou a propriedade IsAutoShrink da função DATABASEPROPERTYEX.  
  
> [!NOTE]  
> A opção AUTO_SHRINK não está disponível em um banco de dados independente.  

<a name="auto_update_statistics"></a> AUTO_UPDATE_STATISTICS { ON | OFF }  
ON  
Especifica que o otimizador de consultas atualiza estatísticas quando são usadas por uma consulta e quando podem estar desatualizadas. As estatísticas ficam desatualizadas depois que operações de inserção, atualização, exclusão ou mesclagem alteram a distribuição de dados na tabela ou na exibição indexada. O otimizador de consulta determina quando estatísticas podem estar desatualizadas contando o número de modificações de dados desde a última atualização das estatísticas e comparando o número de modificações a um limite. O limite se baseia no número de linhas na tabela ou na exibição indexada.  
  
O otimizador de consulta procura estatísticas desatualizadas antes de compilar uma consulta e antes de executar um plano de consulta em cache. Antes de compilar uma consulta, o otimizador de consulta usa as colunas, tabelas e exibições indexadas no predicado de consulta para determinar quais estatísticas podem estar desatualizadas. Antes de executar um plano de consulta em cache, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifica se o plano de consulta faz referência a estatísticas atualizadas.  
  
A opção AUTO_UPDATE_STATISTICS se aplica a estatísticas criadas para índices, colunas únicas em predicados de consulta, além de estatísticas criadas por meio da instrução CREATE STATISTICS. Essa opção também se aplica a estatísticas filtradas.  
  
O padrão é ON. Nós recomendamos que você use a configuração padrão para a maioria dos bancos de dados.  
  
Use a opção AUTO_UPDATE_STATISTICS_ASYNC para especificar se as estatísticas são atualizadas de forma síncrona ou assíncrona.  
  
OFF  
Especifica que o otimizador de consulta não atualiza estatísticas quando elas são usadas por uma consulta e quando elas podem ficar desatualizadas. Definir essa opção como OFF pode acarretar planos de consulta de qualidade inferior e menor desempenho de consulta.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_update_stats_on na exibição do catálogo sys.databases ou a propriedade IsAutoUpdateStatistics da função DATABASEPROPERTYEX.  
  
Para obter mais informações, veja a seção “Usando as opções de estatísticas em todo o banco de dados” em [Estatística](../../relational-databases/statistics/statistics.md).  
  
<a name="auto_update_statistics_async"></a> AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
ON  
Especifica que atualizações de estatísticas para a opção AUTO_UPDATE_STATISTICS são assíncronas. O otimizador de consulta não aguarda a conclusão das atualizações de estatísticas para compilar consultas.  
  
Definir essa opção como ON não tem nenhum efeito, a menos que AUTO_UPDATE_STATISTICS seja definida como ON.  
  
Por padrão, a opção AUTO_UPDATE_STATISTICS_ASYNC é definida como OFF e o otimizador de consulta atualiza estatísticas de forma síncrona.  
  
OFF  
Especifica que atualizações de estatísticas para a opção AUTO_UPDATE_STATISTICS são síncronas. O otimizador de consulta aguarda a conclusão das atualizações de estatísticas para compilar consultas.  
  
Definir essa opção como OFF não tem nenhum efeito, a menos que AUTO_UPDATE_STATISTICS seja definida como ON.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_auto_update_stats_async_on na exibição do catálogo sys.databases.  
  
Para obter mais informações que descrevem quando usar atualizações de estatísticas síncronas ou assíncronas, veja a seção que "Usando as opções de estatísticas em todo o banco de dados" em [Estatísticas](../../relational-databases/statistics/statistics.md).  

<a name="auto_tuning"></a> **\<automatic_tuning_option> ::=**  
**Aplica-se a**: [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  
  
Controla opções automáticas para [ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md).  
  
AUTOMATIC_TUNING = { AUTO | INHERIT | CUSTOM }  
AUTO  
Configurar o valor de ajuste automático como AUTO aplicará a configuração padrão do Azure ao ajuste automático.  
    
INHERIT  
Ao usar o valor INHERIT, você herdará a configuração padrão do servidor pai. Isso será útil principalmente se você quiser personalizar a configuração de ajuste automático em um servidor pai e fazer com que todos os bancos de dados deste servidor herdem (INHERIT) essas configurações personalizadas. Observe que para a herança funcionar, as três opções de ajuste individuais, FORCE_LAST_GOOD_PLAN, CREATE_INDEX e DROP_INDEX, precisam ser configuradas como DEFAULT nos bancos de dados.  
  
CUSTOM  
Ao usar o valor CUSTOM, você precisará personalizar manualmente cada opção de configuração de ajuste automático disponível nos bancos de dados.  
  
Habilita ou desabilita a opção `CREATE_INDEX` de [ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md) do gerenciamento de índices automático.  
  
CREATE_INDEX = { DEFAULT | ON | OFF }  
DEFAULT  
Herda as configurações padrão do servidor. Nesse caso, as opções de habilitar ou desabilitar os recursos individuais de ajuste automático são definidas no nível do servidor.  
  
ON  
Quando habilitado, os índices ausentes são gerados de forma automática em um banco de dados. Após a criação do índice, os ganhos de desempenho da carga de trabalho são verificados. Quando o índice criado não oferecer mais benefícios para o desempenho da carga de trabalho, será automaticamente revertido. Os índices criados automaticamente são sinalizados como gerados pelo sistema.  
  
OFF  
Não gera índices ausentes de modo automático no banco de dados.  
  
Habilita ou desabilita a opção `DROP_INDEX` de [ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md) do gerenciamento de índices automático.  
  
DROP_INDEX = { DEFAULT | ON | OFF }  
DEFAULT  
Herda as configurações padrão do servidor. Nesse caso, as opções de habilitar ou desabilitar os recursos individuais de ajuste automático são definidas no nível do servidor.  
  
ON  
Remove automaticamente os índices duplicados ou que não são mais úteis da carga de trabalho de desempenho.   
  
OFF  
Não remove índices ausentes de modo automático no banco de dados.  
  
Habilita ou desabilita a opção `FORCE_LAST_GOOD_PLAN` de [ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md) da correção de plano automática.  
  
FORCE_LAST_GOOD_PLAN = { DEFAULT | ON | OFF }  
DEFAULT  
Herda as configurações padrão do servidor. Nesse caso, as opções de habilitar ou desabilitar os recursos individuais de ajuste automático são definidas no nível do servidor.  
  
ON  
O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] força automaticamente o último plano sabidamente válido nas consultas [!INCLUDE[tsql-md](../../includes/tsql-md.md)] em que o novo plano SQL provoca regressões de desempenho. O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] monitora continuamente o desempenho de consultas da consulta [!INCLUDE[tsql-md](../../includes/tsql-md.md)] com o plano forçado. Se não houver ganhos de desempenho, o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] continuará usando o último plano válido conhecido. Se os ganhos de desempenho não forem detectados, o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] produzirá um novo plano SQL. A instrução falhará se o repositório de consultas não estiver habilitado ou não estiver no modo de *Leitura-Gravação*.   
  
OFF  
O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] relata possíveis regressões de desempenho de consulta causadas por alterações de plano SQL na exibição [sys.dm_db_tuning_recommendations](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md). No entanto, essas recomendações não são aplicadas automaticamente. Usuário pode monitorar recomendações ativas e corrigir problemas identificados aplicando scripts [!INCLUDE[tsql-md](../../includes/tsql-md.md)] mostrados na exibição. Este é o valor padrão.  
  
**\<change_tracking_option> ::=**  
  
Controla as opções de controle de alterações. É possível habilitar o controle de alterações, definir opções, alterar opções e desabilitar o controle de alterações. Para obter exemplos, confira a seção Exemplos mais adiante neste artigo.  
  
ON  
Habilita o controle de alterações no banco de dados. Quando você habilita o controle de alterações, também pode definir as opções AUTO CLEANUP e CHANGE RETENTION.  
  
AUTO_CLEANUP = { ON | OFF }  
ON  
As informações de controle de alterações são removidas automaticamente depois do período de retenção especificado.  
  
OFF  
Os dados de controle de alterações não são removidos do banco de dados.  
  
CHANGE_RETENTION =*retention_period* { DAYS | HOURS | MINUTES }  
Especifica o período mínimo para manter as informações de controle de alterações no banco de dados. Os dados serão removidos somente quando o valor AUTO_CLEANUP for ON.  
  
*retention_period* é um inteiro que especifica o componente numérico do período de retenção.  
  
O período de retenção padrão é de 2 dias. O período de retenção mínimo é de 1 minuto. O tipo de retenção padrão é DAYS.  
  
OFF  
Desabilita o controle de alterações no banco de dados. É necessário desabilitar o controle de alterações em todas as tabelas antes de poder desabilitá-lo no banco de dados.  
  
**\<cursor_option> ::=**  
  
Controla opções de cursor.  
  
CURSOR_CLOSE_ON_COMMIT { ON | OFF }  
ON  
Qualquer cursor é aberto quando uma transação é confirmada ou quando uma transação revertida é fechada.  
  
OFF  
Os cursores permanecem abertos quando uma transação é confirmada; uma transação revertida fechará todos os cursores, exceto aqueles definidos como INSENSITIVE ou STATIC.  
  
As configurações no nível de conexão que são definidas com o uso da instrução SET substituem a configuração de banco de dados padrão por CURSOR_CLOSE_ON_COMMIT. Por padrão, clientes ODBC e OLE DB emitem uma configuração CURSOR_CLOSE_ON_COMMIT de instrução SET no nível de conexão como desativada para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET CURSOR_CLOSE_ON_COMMIT](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md).  
  
O status dessa opção pode ser determinado examinando-se a coluna is_cursor_close_on_commit_on na exibição do catálogo sys.databases ou a propriedade IsCloseCursorsOnCommitEnabled da função DATABASEPROPERTYEX. O cursor é implicitamente desalocado somente na desconexão. Para saber mais, confira [DECLARE CURSOR](../../t-sql/language-elements/declare-cursor-transact-sql.md).  
  
**\<db_encryption_option> ::=**  
  
Controla o estado de criptografia do banco de dados.  
  
ENCRYPTION {ON | OFF}  
Define o banco de dados a ser criptografado (ON) ou não criptografado (OFF). Para saber mais sobre criptografia de banco de dados, confira [Transparent Data Encryption](../../relational-databases/security/encryption/transparent-data-encryption.md) e [Transparent Data Encryption com o Banco de Dados SQL do Azure](../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md).  
  
Quando a criptografia estiver habilitada no nível de banco de dados, todos os grupos de arquivos serão criptografados. Qualquer novo grupo de arquivos herdará a propriedade criptografada. Se algum grupo de arquivos do banco de dados for definido como **READ ONLY**, haverá falha na operação de criptografia de banco de dados.  
  
É possível ver o estado da criptografia do banco de dados usando a exibição de gerenciamento dinâmico [sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md).  
  
**\<db_update_option> ::=**  
  
Controla se atualizações são permitidas no banco de dados.  
  
READ_ONLY  
Os usuários podem ler dados do banco de dados, mas não modificá-los.  
  
> [!NOTE]  
>  Para melhorar o desempenho da consulta, atualize as estatísticas antes de configurar um banco de dados como READ_ONLY. Se forem necessárias estatísticas adicionais depois de um banco de dados ser definido como READ_ONLY, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] criará estatísticas no tempdb. Para obter mais informações sobre estatísticas para um banco de dados somente leitura, veja [Estatísticas](../../relational-databases/statistics/statistics.md).  
  
READ_WRITE  
O banco de dados está disponível para operações de leitura e gravação.  
  
Para alterar esse estado, é necessário ter acesso exclusivo ao banco de dados. Para obter mais informações, consulte a cláusula SINGLE_USER.  
  
> [!NOTE]  
> Nos bancos de dados federados do [!INCLUDE[ssSDS](../../includes/sssds-md.md)], SET { READ_ONLY | READ_WRITE } é desabilitado.  
  
**\<db_user_access_option> ::=**  
  
Controla o acesso de usuários ao banco de dados.  
  
RESTRICTED_USER  
RESTRICTED_USER permite que somente os membros da função de banco de dados fixa db_owner e das funções de servidor fixas dbcreator e sysadmin conectem-se ao banco de dados, mas não limita seu número. Todas as conexões com o banco de dados são desconectadas no período especificado pela cláusula de término da instrução ALTER DATABASE. Depois que o banco de dados fizer a transição para o estado RESTRICTED_USER, as tentativas de conexão realizadas por usuários não qualificados serão recusadas.  **RESTRICTED_USER** não pode ser modificado com a instância Gerenciada do Banco de Dados de SQL.
  
MULTI_USER  
Todos os usuários com permissões apropriadas para se conectar ao banco de dados são permitidos.  
  
O status dessa opção pode ser determinado examinando-se a coluna user_access na exibição do catálogo sys.databases ou a propriedade UserAccess da função DATABASEPROPERTYEX.  
  
**\<delayed_durability_option> ::=**  
  
Controla se as transações são confirmadas completamente duráveis ou duráveis atrasadas.  
  
DISABLED  
Todas as transações após SET DISABLED são completamente duráveis. Todas as opções de durabilidade definidas em um bloco atômico ou instrução de confirmação são ignoradas.  
  
ALLOWED  
Todas as transações após SET ALLOWED são completamente duráveis ou duráveis atrasadas, dependendo da opção de durabilidade definida no bloco atômico ou instrução de confirmação.  
  
FORCED  
Todas as transações após SET FORCED são duráveis atrasadas. Todas as opções de durabilidade definidas em um bloco atômico ou instrução de confirmação são ignoradas.  
  
**\<PARAMETERIZATION_option> ::=**  
  
Controla a opção de parametrização.  
  
PARAMETERIZATION { SIMPLE | FORCED }  
SIMPLE  
As consultas são parametrizadas com base no comportamento padrão do banco de dados.  
  
FORCED  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parametriza todas as consultas feitas no banco de dados.  
  
A configuração atual dessa opção pode ser determinada examinando-se a coluna is_parameterization_forced na exibição do catálogo sys.databases.  
  
**\<query_store_options> ::=**  
  
ON | OFF | CLEAR [ ALL ]  
Controla se o repositório de consultas está habilitado neste banco de dados, além de controlar a remoção de conteúdo do repositório de consultas.  
  
ON  
Habilita o repositório de consultas.  
  
OFF  
Desabilita o repositório de consultas.  Este é o valor padrão.   
  
CLEAR  
Remove o conteúdo do repositório de consultas.  
  
OPERATION_MODE  
Descreve o modo de operação do repositório de consultas. Os valores válidos são READ_ONLY e READ_WRITE. No modo READ_WRITE, o repositório de consultas coleta e persiste as informações das estatísticas de execução do plano de consulta e do tempo de execução. No modo READ_ONLY, as informações podem ser lidas do repositório de consultas, mas novas informações não são adicionadas. Se o espaço máximo alocado do repositório de consultas tiver se esgotado, o repositório de consultas alterará o modo de operação para READ_ONLY.  
  
CLEANUP_POLICY  
Descreve a política de retenção de dados do repositório de consultas. STALE_QUERY_THRESHOLD_DAYS determina o número de dias que as informações de uma consulta são mantidas no repositório de consultas. STALE_QUERY_THRESHOLD_DAYS é do tipo **bigint**.  
  
DATA_FLUSH_INTERVAL_SECONDS  
Determina a frequência na qual os dados gravados no repositório de consultas é persistida no disco. Para otimizar o desempenho, os dados coletados pelo repositório de consultas são gravados de maneira assíncrona no disco. A frequência em que essa transferência assíncrona ocorre é configurada usando o argumento DATA_FLUSH_INTERVAL_SECONDS. DATA_FLUSH_INTERVAL_SECONDS é do tipo **bigint**.  
  
MAX_STORAGE_SIZE_MB  
Determina o espaço alocado para o repositório de consultas. MAX_STORAGE_SIZE_MB é do tipo **bigint**.  
  
INTERVAL_LENGTH_MINUTES  
Determina o intervalo de tempo em que os dados de estatísticas de execução do tempo de execução são agregados no repositório de consultas. Para otimizar o uso de espaço, as estatísticas de execução de tempo de execução no repositório de estatísticas de tempo de execução são agregadas em uma janela de tempo fixo. Essa janela de tempo fixo é configurada usando o argumento INTERVAL_LENGTH_MINUTES. INTERVAL_LENGTH_MINUTES é do tipo **bigint**.  
  
SIZE_BASED_CLEANUP_MODE  
Controla se a limpeza será ativada automaticamente quando a quantidade total de dados se aproximar do tamanho máximo:  
  
OFF  
Limpeza com base no tamanho não será ativada automaticamente. 
  
AUTO  
A limpeza com base em tamanho será ativada automaticamente quando o tamanho em disco atingir 90% do **max_storage_size_mb**. Limpeza com base no tamanho remove as consultas menos dispendiosas e mais antigas primeiro. Ele para a aproximadamente 80% do **max_storage_size_mb**.  Esse é o valor de configuração padrão.  
  
SIZE_BASED_CLEANUP_MODE é do tipo **nvarchar**.  
  
QUERY_CAPTURE_MODE  
Designa o modo de captura de consulta ativo no momento:  
  
ALL Todas as consultas são capturadas. Esse é o valor de configuração padrão.
  
AUTO Captura consultas de relevantes com base na contagem de execução e no consumo de recursos.  Esse é o valor de configuração padrão para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
NONE Parar de capturar novas consultas. O Repositório de Consultas continuará a coletar estatísticas de compilação e tempo de execução para consultas que já foram capturadas. Use essa configuração com cuidado, pois você poderá deixar de capturar consultas importantes.  
  
QUERY_CAPTURE_MODE é do tipo **nvarchar**.  
  
max_plans_per_query  
Um número inteiro que representa a quantidade máxima de planos de manutenção para cada consulta. O padrão é 200.  
  
**\<snapshot_option> ::=**  
  
Determina o nível de isolamento da transação.  
  
ALLOW_SNAPSHOT_ISOLATION { ON | OFF }  
ON  
Habilita a opção de Instantâneo no nível do banco de dados. Quando habilitada, as instruções DML começam a gerar versões de linha mesmo quando nenhuma transação usar Isolamento de Instantâneo. Quando essa opção está habilitada, as transações podem especificar o nível de isolamento da transação SNAPSHOT. Ao executar uma transação no nível de isolamento SNAPSHOT, todas as instruções consultam um instantâneo de dados, se houver um no início da instrução. Se uma transação que executa no nível de isolamento SNAPSHOT acessar dados em vários bancos de dados, ALLOW_SNAPSHOT_ISOLATION deverá ser definido como ON em todos os bancos de dados ou cada instrução na transação deverá usar dicas de bloqueio em qualquer referência em uma cláusula FROM para uma tabela em um banco de dados onde ALLOW_SNAPSHOT_ISOLATION seja OFF.  
  
OFF  
Desativa a opção de Instantâneo no nível do banco de dados. As transações não podem especificar o nível de isolamento da transação SNAPSHOT.  
  
Ao definir ALLOW_SNAPSHOT_ISOLATION para um novo estado (de ON para OFF, ou de OFF, para ON), ALTER DATABASE não retorna o controle para o chamador até que todas as transações existentes no banco de dados sejam confirmadas. Se o banco de dados já estiver no estado especificado na instrução ALTER DATABASE, o controle será retornado ao chamador imediatamente. Se a instrução ALTER DATABASE não for retornada rapidamente, use [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) para determinar se há transações de longa duração. Se a instrução ALTER DATABASE for cancelada, o banco de dados permanecerá no estado que estava quando ALTER DATABASE foi iniciada. A exibição do catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) indica o estado de transações de isolamento de instantâneo no banco de dados. Se **snapshot_isolation_state_desc** = IN_TRANSITION_TO_ON, ALTER DATABASE ALLOW_SNAPSHOT_ISOLATION OFF fará uma pausa de seis segundos e tentará novamente executar a operação.  
  
Não é possível alterar o estado de ALLOW_SNAPSHOT_ISOLATION se o banco de dados for OFFLINE.  
  
Se você definir ALLOW_SNAPSHOT_ISOLATION em um banco de dados READ_ONLY, a configuração será retida se o banco de dados for definido mais tarde como READ_WRITE.  
  
É possível alterar as configurações ALLOW_SNAPSHOT_ISOLATION para os bancos de dados mestre, modelo, msdb e tempdb. Se você alterar a configuração para tempdb, ela será retida sempre que a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] for interrompida e reiniciada. Ao alterar a configuração para modelo, ela se tornará o padrão para qualquer novo banco de dados que for criado, exceto para tempdb.  
  
A opção é ON, por padrão, para os bancos de dados mestre e msdb.  
  
A configuração atual dessa opção pode ser determinada examinando-se a coluna snapshot_isolation_state na exibição do catálogo sys.databases.  
  
READ_COMMITTED_SNAPSHOT { ON | OFF }  
ON  
Habilita a opção de Instantâneo de Leitura Confirmada no nível do banco de dados. Quando habilitada, as instruções DML começam a gerar versões de linha mesmo quando nenhuma transação usar Isolamento de Instantâneo. Quando essa opção está habilitada, as transações que especificam o nível de isolamento de leitura confirmada usam o controle de versão de linha, em vez de bloqueio. Quando uma transação é executada no nível de isolamento de leitura confirmada, todas as instruções consultam um instantâneo de dados, se houver um no início da instrução.  
  
OFF  
Desabilita a opção de Instantâneo de Leitura Confirmada no nível do banco de dados. As transações que especificam o nível de isolamento READ COMMITTED usam bloqueio.  
  
Para definir READ_COMMITTED_SNAPSHOT como ON ou OFF, não deve haver nenhuma conexão ativa com o banco de dados exceto para a que está executando o comando ALTER DATABASE. Entretanto, o banco de dados não precisa estar no modo de usuário único. Não é possível alterar o estado dessa opção quando o banco de dados for OFFLINE.  
  
Se você definir READ_COMMITTED_SNAPSHOT em um banco de dados READ_ONLY, a configuração será retida quando o banco de dados for definido mais tarde como READ_WRITE.  
  
READ_COMMITTED_SNAPSHOT não pode ser ativado como ON para os bancos de dados do sistema mestre, tempdb ou msdb. Se você alterar a configuração para modelo, ela se tornará o padrão para qualquer novo banco de dados que for criado, exceto para tempdb.  
  
A configuração atual dessa opção pode ser determinada examinando-se a coluna is_read_committed_snapshot_on na exibição do catálogo sys.databases.  
  
> [!WARNING]  
>  Quando uma tabela for criada com **DURABILITY = SCHEMA_ONLY**, e **READ_COMMITTED_SNAPSHOT** depois forem alterado usando **ALTER DATABASE**, os dados na tabela serão perdidos.  
  
MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT { ON | OFF }  
  
ON  
Quando o nível de isolamento da transação estiver configurado para qualquer nível de isolamento inferior ao SNAPSHOT (por exemplo, READ COMMITTED ou READ UNCOMMITTED), todas as operações interpretadas de [!INCLUDE[tsql](../../includes/tsql-md.md)] em tabelas com otimização de memória serão executadas em isolamento SNAPSHOT. Isso é feito mesmo que o nível de isolamento da transação seja definido explicitamente no nível de sessão ou se a opção for usada implicitamente.  
  
OFF  
Não eleva o nível de isolamento da transação para operações interpretadas do [!INCLUDE[tsql](../../includes/tsql-md.md)] em tabelas com otimização de memória.  
  
Não é possível alterar o estado de MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT se o banco de dados for OFFLINE.  
  
A opção é OFF, por padrão.  
  
A configuração atual dessa opção pode ser determinada, examinando a coluna **is_memory_optimized_elevate_to_snapshot_on** na exibição de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
**\<sql_option> ::=**  
  
Controla as opções de conformidade ANSI no nível de banco de dados.  
  
ANSI_NULL_DEFAULT { ON | OFF }  
Determina o valor padrão, NULL ou NOT NULL, de um [tipo definido pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) CLR ou coluna para o qual a nulidade não é definida explicitamente nas instruções CREATE TABLE ou ALTER TABLE. As colunas definidas com restrições seguem as regras de restrição apesar dessa configuração.  
  
ON  
O valor padrão é NULL.  
  
OFF  
O valor padrão é NOT NULL.  
  
As configurações no nível de conexão que são definidas com o uso de uma instrução SET substituem a configuração no nível de banco de dados padrão para ANSI_NULL_DEFAULT. Por padrão, clientes ODBC e OLE DB emitem uma configuração ANSI_NULL_DEFAULT de instrução SET no nível de conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET ANSI_NULL_DFLT_ON](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md).  
  
Para compatibilidade ANSI, definir a opção de banco de dados ANSI_NULL_DEFAULT como ON altera o banco de dados padrão para NULL.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_ansi_null_default_on na exibição do catálogo sys.databases ou a propriedade IsAnsiNullDefault da função DATABASEPROPERTYEX.  
  
ANSI_NULLS { ON | OFF }  
ON  
Todas as comparações com um valor nulo são avaliadas como UNKNOWN.  
  
OFF  
As comparações de valores não UNICODE com um valor nulo são avaliadas como TRUE se ambos os valores forem NULL.  
  
> [!IMPORTANT]  
>  Em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ANSI_NULLS sempre estará ON e quaisquer aplicativos que definam explicitamente a opção como OFF produzirão um erro. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
As configurações no nível de conexão que são definidas com o uso de uma instrução SET substituem a configuração no nível de banco de dados padrão para ANSI_NULLS. Por padrão, clientes ODBC e OLE DB emitem uma configuração ANSI_NULLS de instrução SET no nível de conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET ANSI_NULLS](../../t-sql/statements/set-ansi-nulls-transact-sql.md).  
  
SET ANSI_NULLS também deve ser definido como ON ao criar ou fazer alterações em índices em colunas computadas ou exibições indexadas.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_ansi_nulls_on na exibição do catálogo sys.databases ou a propriedade IsAnsiNullsEnabled da função DATABASEPROPERTYEX.  
  
ANSI_PADDING { ON | OFF }  
ON  
As cadeias de caracteres são preenchidas com o mesmo comprimento antes da conversão ou inserção em um tipo de dados **varchar** ou **nvarchar**.  
  
Espaços em branco à direita nos valores de caracteres inseridos nas colunas **varchar** ou **nvarchar** e os zeros à direita nos valores binários inseridos nas colunas **varbinary** não serão cortados. Os valores não são preenchidos com o tamanho da coluna.  
  
OFF  
Espaços em branco à direita para **varchar** ou **nvarchar** e zeros para **varbinary** são cortados.  
  
Quando OFF é especificado, essa configuração afeta apenas a definição de novas colunas.  
  
> [!IMPORTANT]  
>  Em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ANSI_PADDING sempre será ON e quaisquer aplicativos que definam explicitamente a opção como OFF produzirão um erro. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. É recomendável sempre definir ANSI_PADDING como ON. ANSI_PADDING deve ser ON ao criar ou manipular índices em colunas computadas ou exibições indexadas.  
  
As colunas **char(*n*)** e **binary(*n*)** que permitem valores nulos são preenchidas até o tamanho da coluna quando ANSI_PADDING está definido como ON, mas os brancos à direita e os zeros são cortados quando ANSI_PADDING está definido como OFF. As colunas **char(*n*)** e **binary(*n*)** que não permitem valores nulos sempre são preenchidas até o tamanho da coluna.  
  
As configurações no nível de conexão que são definidas com o uso de uma instrução SET substituem a configuração no nível de banco de dados padrão para ANSI_PADDING. Por padrão, clientes ODBC e OLE DB emitem uma configuração ANSI_PADDING da instrução SET no nível da conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET ANSI_PADDING](../../t-sql/statements/set-ansi-padding-transact-sql.md).  
  
O status dessa opção pode ser determinado examinando-se a coluna is_ansi_padding_on na exibição do catálogo sys.databases ou a propriedade IsAnsiPaddingEnabled da função DATABASEPROPERTYEX.  
  
ANSI_WARNINGS { ON | OFF }  
ON  
Erros ou avisos são emitidos quando condições como “divisão por zero” ou “valores nulos” aparecerem em funções de agregação.  
  
OFF  
Nenhum aviso é emitido e os valores nulos são retornados quando condições como “dividir por zero” ocorrem.  
  
SET ANSI_WARNINGS também deve ser definido como ON ao criar ou fazer alterações em índices em colunas computadas ou exibições indexadas.  
  
As configurações no nível de conexão que são definidas usando uma instrução SET substituem a configuração no nível de banco de dados padrão para ANSI_WARNINGS. Por padrão, clientes ODBC e OLE DB emitem uma configuração ANSI_WARNINGS de instrução SET no nível de conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET ANSI_PADDING](../../t-sql/statements/set-ansi-warnings-transact-sql.md).  
  
O status dessa opção pode ser determinado examinando-se a coluna is_ansi_warnings_on na exibição do catálogo sys.databases ou a propriedade IsAnsiWarningsEnabled da função DATABASEPROPERTYEX.  
  
ARITHABORT { ON | OFF }  
ON  
Uma consulta é encerrada quando ocorre um estouro ou erro de divisão por zero durante a execução da consulta.  
  
OFF  
Uma mensagem de aviso é exibida quando um desses erros ocorre, mas a consulta, o lote ou a transação continuam a ser processados como se nenhum erro tivesse ocorrido.  
  
SET ARITHABORT também deve ser definido como ON ao criar ou fazer alterações em índices em colunas computadas ou exibições indexadas.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_arithabort_on na exibição do catálogo sys.databases ou a propriedade IsArithmeticAbortEnabled da função DATABASEPROPERTYEX.  
  
COMPATIBILITY_LEVEL { 140 | 130 | 120 | 110 | 100 | 90 | 80 }   
Para saber mais, confira [ALTER DATABASE Compatibility Level](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
CONCAT_NULL_YIELDS_NULL { ON | OFF }  
ON  
O resultado de uma operação de concatenação será NULL quando qualquer operando for NULL. Por exemplo, concatenar a cadeia de caracteres "This is" e NULL gera o valor NULL, em vez do valor "This is".  
  
OFF  
O valor nulo é tratado como uma cadeia de caracteres vazia.  
  
CONCAT_NULL_YIELDS_NULL deve ser definido como ON ao criar ou fazer alterações em índices em colunas computadas ou exibições indexadas.  
  
> [!IMPORTANT]  
>  Em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], CONCAT_NULL_YIELDS_NULL sempre estará ON e quaisquer aplicativos que definam explicitamente a opção como OFF produzirão um erro. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
As configurações no nível de conexão que são definidas usando uma instrução SET substituem a configuração no nível de banco de dados padrão para CONCAT_NULL_YIELDS_NULL. Por padrão, clientes ODBC e OLE DB emitem uma configuração CONCAT_NULL_YIELDS_NULL de instrução SET no nível de conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET CONCAT_NULL_YIELDS_NULL](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).  
  
O status dessa opção pode ser determinado examinando-se a coluna is_concat_null_yields_null_on na exibição do catálogo sys.databases ou a propriedade IsNullConcat da função DATABASEPROPERTYEX.  
  
QUOTED_IDENTIFIER { ON | OFF }  
ON  
As aspas duplas podem ser utilizadas para conter identificadores delimitados.  
  
Todas as cadeias de caracteres delimitadas por aspas duplas são interpretadas como identificadores de objeto. Os identificadores entre aspas não precisam seguir as regras [!INCLUDE[tsql](../../includes/tsql-md.md)] para identificadores. Eles podem ser palavras-chave e incluir caracteres geralmente não permitidos nos identificadores [!INCLUDE[tsql](../../includes/tsql-md.md)]. Se o sinal de aspas simples (') fizer parte da cadeia de caracteres literal, ele poderá ser representado por aspas duplas (").  
  
OFF  
Os identificadores não podem estar entre aspas e devem seguir todas as regras de identificadores [!INCLUDE[tsql](../../includes/tsql-md.md)]. Literais podem ser delimitados por aspas simples ou duplas.  
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também permite que os identificadores sejam delimitados por colchetes ([ ]). Os identificadores entre colchetes podem sempre ser usados, seja qual for a configuração de QUOTED_IDENTIFIER. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
Quando uma tabela é criada, a opção QUOTED IDENTIFIER sempre é armazenada como ON nos metadados da tabela, mesmo que a opção esteja definida como OFF quando a tabela é criada.  
  
As configurações no nível de conexão que são definidas com o uso de uma instrução SET substituem a configuração no nível de banco de dados padrão para QUOTED_IDENTIFIER. Por padrão, clientes ODBC e OLE DB emitem uma configuração QUOTED_IDENTIFIER de instrução SET no nível de conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
O status dessa opção pode ser determinado examinando-se a coluna is_quoted_identifier_on na exibição do catálogo sys.databases ou a propriedade IsQuotedIdentifiersEnabled da função DATABASEPROPERTYEX.  
  
NUMERIC_ROUNDABORT { ON | OFF }  
ON  
Um erro é gerado quando ocorre perda de precisão em uma expressão.  
  
OFF  
As perdas de precisão não geram mensagens de erro e o resultado é arredondado de acordo com a precisão da coluna ou variável que armazena o resultado.  
  
NUMERIC_ROUNDABORT deve ser definido como OFF ao criar ou fazer alterações em índices em colunas computadas ou exibições indexadas.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_numeric_roundabort_on na exibição do catálogo sys.databases ou a propriedade IsNumericRoundAbortEnabled da função DATABASEPROPERTYEX.  
  
RECURSIVE_TRIGGERS { ON | OFF }  
ON  
O disparo recursivo de gatilhos AFTER é permitido.  
  
OFF  
Apenas o disparo recursivo direto de gatilhos AFTER não é permitido. Para desabilitar também a recursão indireta de gatilhos AFTER, defina a opção do servidor de gatilhos aninhados como **0** usando **sp_configure**.  
  
> [!NOTE]  
>  Somente a recursão direta será evitada quando RECURSIVE_TRIGGERS estiver definido como OFF. Para desabilitar a recursão indireta, é necessário definir também a opção do servidor nested triggers como 0.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_recursive_triggers_on na exibição do catálogo sys.databases ou a propriedade IsRecursiveTriggersEnabled da função DATABASEPROPERTYEX.  

**\<target_recovery_time_option> ::=**  
  
Especifica a frequência de pontos de verificação indiretos por banco de dados. Começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o valor padrão para novos bancos de dados é de 1 minuto, o que indica que o banco de dados usará pontos de verificação indiretos. Para versões mais antigas, o padrão é 0, o que indica que o banco de dados usará pontos de verificação automáticos cuja frequência depende da configuração do intervalo de recuperação da instância de servidor. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda 1 minuto para a maioria dos sistemas.  
  
TARGET_RECOVERY_TIME **=***target_recovery_time* { SECONDS | MINUTES }  
*target_recovery_time*  
Especifica o salto máximo no tempo para recuperar o banco de dados especificado no caso de uma falha.  
  
SECONDS  
Indica que *target_recovery_time* é expresso como o número de segundos.  
  
MINUTES  
Indica que *target_recovery_time* é expresso como o número de minutos.  
  
Para saber mais sobre pontos de verificação indiretos, confira [Pontos de verificação de banco de dados](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
**WITH \<termination> ::=**  
  
Especifica quando reverter transações incompletas quando há transição do banco de dados de um estado para outro. Se a cláusula de término for omitida, a instrução ALTER DATABASE aguardará indefinidamente se houver algum bloqueio no banco de dados. Somente uma cláusula de término pode ser especificada e ela sucede as cláusulas SET.  
  
> [!NOTE]  
>  Nem todas as opções de banco de dados usam a cláusula WITH \<termination>. Para saber mais, confira a tabela em[Opções de configuração](#SettingOptions) na seção Comentários deste artigo.  
  
ROLLBACK AFTER *integer* [SECONDS] | ROLLBACK IMMEDIATE  
Especifica se a reversão deve ser feita após o número de segundos especificado ou imediatamente.  
  
NO_WAIT  
Especifica que, se a alteração de estado do banco de dados ou da opção solicitada não puder ser concluída imediatamente sem esperar que as transações sejam confirmadas ou revertidas por si mesmas, a solicitação falhará.  
  
##  <a name="SettingOptions"></a> Opções de configuração  
Para recuperar as configurações atuais das opções de banco de dados, use a exibição do catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) ou [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)  
  
Depois de definir uma opção de banco de dados, a modificação entra em vigor imediatamente.  
  
Para alterar os valores padrão de qualquer uma das opções de banco de dados para todos os bancos de dados criados recentemente, altere a opção de banco de dados apropriada no banco de dados modelo.  
  
Nem todas as opções de banco de dados usam a cláusula WITH \<termination> ou podem ser especificadas em combinação com outras opções. A tabela a seguir lista essas opções e seu status de opção e término.  
  
|Categoria de opções|Pode ser especificado com outras opções|Pode usar a cláusula WITH \<termination>|  
|----------------------|-----------------------------------------|---------------------------------------------|  
|\<auto_option>|Sim|não|  
|\<change_tracking_option>|Sim|Sim|  
|\<cursor_option>|Sim|não|  
|\<db_encryption_option>|Sim|não|  
|\<db_update_option>|Sim|Sim|  
|\<db_user_access_option>|Sim|Sim|  
|\<delayed_durability_option>|Sim|Sim|  
|\<parameterization_option>|Sim|Sim|  
|ALLOW_SNAPSHOT_ISOLATION|não|não|  
|READ_COMMITTED_SNAPSHOT|não|Sim|  
|MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT|Sim|Sim|  
|DATE_CORRELATION_OPTIMIZATION|Sim|Sim|  
|\<sql_option>|Sim|não|  
|\<target_recovery_time_option>|não|Sim|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-setting-the-database-to-readonly"></a>A. Configurando o banco de dados como READ_ONLY  
Alterar o estado de um banco de dados ou grupo de arquivos para READ_ONLY ou READ_WRITE requer acesso exclusivo ao banco de dados. O exemplo a seguir define o banco de dados como o modo `RESTRICTED_USER` para limitar o acesso. Em seguida, o exemplo define o estado do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] como `READ_ONLY` e retorna o acesso ao banco de dados para todos os usuários.  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET RESTRICTED_USER;  
GO  
ALTER DATABASE AdventureWorks2012  
SET READ_ONLY  
GO  
ALTER DATABASE AdventureWorks2012  
SET MULTI_USER;  
GO  
  
```  
  
### <a name="b-enabling-snapshot-isolation-on-a-database"></a>B. Habilitando o isolamento de instantâneo em um banco de dados  
O exemplo a seguir habilita a opção de estrutura de isolamento de instantâneo para o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
USE AdventureWorks2012;  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET ALLOW_SNAPSHOT_ISOLATION ON;  
GO  
-- Check the state of the snapshot_isolation_framework  
-- in the database.  
SELECT name, snapshot_isolation_state,   
    snapshot_isolation_state_desc AS description  
FROM sys.databases  
WHERE name = N'AdventureWorks2012';  
GO  
  
```  
  
O conjunto de resultados mostra que a estrutura de isolamento de instantâneo está habilitada.  
  
|NAME |snapshot_isolation_state |descrição|  
|-------------------- |------------------------  |----------|  
|AdventureWorks2012   |1                        | ON |  
  
### <a name="c-enabling-modifying-and-disabling-change-tracking"></a>C. Habilitando, modificando e desabilitando o controle de alterações  
O exemplo a seguir habilita o controle de alterações no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e define o período de retenção para `2` dias.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = ON  
(AUTO_CLEANUP = ON, CHANGE_RETENTION = 2 DAYS);  
```  
  
O exemplo a seguir mostra como alterar o período de retenção para `3` dias.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING (CHANGE_RETENTION = 3 DAYS);  
```  
  
O exemplo a seguir mostra como desabilitar o controle de alterações no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = OFF;  
```  
  
### <a name="d-enabling-the-query-store"></a>D. Habilitando o repositório de consultas  
  
O exemplo a seguir habilita o repositório de consultas e configura os parâmetros do repositório de consultas.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET QUERY_STORE = ON   
    (  
      OPERATION_MODE = READ_WRITE   
    , CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 )  
    , DATA_FLUSH_INTERVAL_SECONDS = 900   
    , MAX_STORAGE_SIZE_MB = 1024   
    , INTERVAL_LENGTH_MINUTES = 60   
    );  
```  
  
## <a name="see-also"></a>Consulte Também  
[Nível de compatibilidade de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
[Espelhamento de banco de dados de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
[Estatística](../../relational-databases/statistics/statistics.md)   
[CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqldbls)   
[Habilitar e desabilitar o controle de alterações](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)   
[DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)   
[DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)   
[SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
[sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
[Melhor prática com o Repositório de Consultas](../../relational-databases/performance/best-practice-with-the-query-store.md) 
  
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> <table>
> <tr>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
> </tr>
> <tr>
>   <th><a href="alter-database-transact-sql-set-options.md?view=sql-server-2016">SQL Server</a></th>
>   <th><a href="alter-database-transact-sql-set-options.md?view=azuresqldb-current">Banco de Dados SQL<br />Banco de Dados SQL</a></th>
>   <th><strong><em>* Banco de Dados SQL<br />Instância Gerenciada *</em></strong></th>
> </tr>
> </table>

&nbsp;

# <a name="azure-sql-database-managed-instance"></a>Instância Gerenciada do Banco de Dados SQL do Azure

Níveis de compatibilidade são opções `SET`, mas são descritas em [Nível de Compatibilidade de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
> [!NOTE]  
> Muitas opções de definição de banco de dados podem ser configuradas para a sessão atual usando [Instruções SET](../../t-sql/statements/set-statements-transact-sql.md) e são configuradas com frequência por aplicativos quando eles são conectados. As opções definidas no nível de sessão substituem os valores de **ALTER DATABASE SET** . As opções de banco de dados descritas abaixo são os valores que podem ser definidos para as sessões que não fornecem explicitamente outros valores de definição de conjunto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ALTER DATABASE { database_name | Current }  
SET   
{  
    <optionspec> [ ,...n ] 
}  
;  

<optionspec> ::=
{  
    <auto_option>   
  | <change_tracking_option>   
  | <cursor_option>   
  | <db_encryption_option>    
  | <delayed_durability_option>  
  | <parameterization_option>  
  | <query_store_options>  
  | <snapshot_option>  
  | <sql_option>   
  | <target_recovery_time_option>   
  | <termination>  
  | <temporal_history_retention>
}  
;  
<auto_option> ::= 
{  
    AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] } 
  | AUTO_SHRINK { ON | OFF } 
  | AUTO_UPDATE_STATISTICS { ON | OFF } 
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
}  

<automatic_tuning_option> ::=  
{  
  AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = { ON | OFF } )
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
  | COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 }   
  | CONCAT_NULL_YIELDS_NULL { ON | OFF }   
  | NUMERIC_ROUNDABORT { ON | OFF }   
  | QUOTED_IDENTIFIER { ON | OFF }   
  | RECURSIVE_TRIGGERS { ON | OFF }   
}

<temporal_history_retention>  ::=  TEMPORAL_HISTORY_RETENTION { ON | OFF }
```  

## <a name="arguments"></a>Argumentos  
*database_name*  
É o nome do banco de dados a ser modificado.  
  
CURRENT  
`CURRENT` executa a ação no banco de dados atual. `CURRENT` não é compatível com todas as opções em todos os contextos. Se `CURRENT` falhar, forneça o nome do banco de dados. 
  
**\<auto_option> ::=**
  
Controla opções automáticas.  
<a name="auto_create_statistics"></a> AUTO_CREATE_STATISTICS { ON | OFF }  
ON  
O otimizador de consulta cria estatísticas em colunas únicas em predicados de consulta, conforme necessário, para melhorar planos e desempenho de consulta. Estas estatísticas de coluna única são criadas quando o otimizador de consulta compila consultas. As estatísticas de coluna única só são criadas em colunas que ainda não são a primeira de um objeto de estatísticas existente.  
  
O padrão é ON. Nós recomendamos que você use a configuração padrão para a maioria dos bancos de dados.  
  
OFF  
O otimizador de consulta não cria estatísticas em colunas únicas em predicados de consulta quando estiver compilando consultas. Definir essa opção como OFF pode acarretar planos de consulta de qualidade inferior e menor desempenho de consulta.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_create_stats_on na exibição do catálogo sys.databases ou a propriedade IsAutoCreateStatistics da função DATABASEPROPERTYEX.  
  
Para obter mais informações, veja a seção “Usando as opções de estatísticas em todo o banco de dados” em [Estatística](../../relational-databases/statistics/statistics.md).  
  
INCREMENTAL = ON | OFF  
Quando AUTO_CREATE_STATISTICS estiver ON e INCREMENTAL estiver definido como ON, as estatísticas criadas automaticamente são criadas como incrementais sempre que as estatísticas incrementais tiverem suporte. O valor padrão é OFF. Para saber mais, veja [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md).  
  
<a name="auto_shrink"></a> AUTO_SHRINK { ON | OFF }  
ON  
Os arquivos de banco de dados são candidatos à redução periódica.  
  
Arquivos de dados e arquivos de log podem ser reduzidos automaticamente. AUTO_SHRINK reduzirá o tamanho do log de transações somente se o banco de dados estiver definido como modelo de recuperação SIMPLE ou se foi feito backup do log. Quando definido como OFF, os arquivos de banco de dados não são reduzidos automaticamente durante as verificações periódicas de espaço não utilizado.  
  
A opção AUTO_SHRINK faz com que os arquivos sejam reduzidos quando mais que 25% do arquivo contém espaço não utilizado. O arquivo é reduzido de forma que 25% de seu tamanho seja de espaço não utilizado ou ele tenha o mesmo tamanho de quando foi criado, o que for maior.  
  
Não é possível reduzir um banco de dados somente leitura.  
  
OFF  
Os arquivos de banco de dados não são reduzidos automaticamente durante as verificações periódicas de espaço não utilizado.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_auto_shrink_on na exibição do catálogo sys.databases ou a propriedade IsAutoShrink da função DATABASEPROPERTYEX.  
  
> [!NOTE]  
> A opção AUTO_SHRINK não está disponível em um banco de dados independente.  
  
<a name="auto_update_statistics"></a> AUTO_UPDATE_STATISTICS { ON | OFF }  
ON  
Especifica que o otimizador de consultas atualiza estatísticas quando são usadas por uma consulta e quando podem estar desatualizadas. As estatísticas ficam desatualizadas depois que operações de inserção, atualização, exclusão ou mesclagem alteram a distribuição de dados na tabela ou na exibição indexada. O otimizador de consulta determina quando estatísticas podem estar desatualizadas contando o número de modificações de dados desde a última atualização das estatísticas e comparando o número de modificações a um limite. O limite se baseia no número de linhas na tabela ou na exibição indexada.  
  
O otimizador de consulta procura estatísticas desatualizadas antes de compilar uma consulta e antes de executar um plano de consulta em cache. Antes de compilar uma consulta, o otimizador de consulta usa as colunas, tabelas e exibições indexadas no predicado de consulta para determinar quais estatísticas podem estar desatualizadas. Antes de executar um plano de consulta em cache, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifica se o plano de consulta faz referência a estatísticas atualizadas.  
  
A opção AUTO_UPDATE_STATISTICS se aplica a estatísticas criadas para índices, colunas únicas em predicados de consulta, além de estatísticas criadas por meio da instrução CREATE STATISTICS. Essa opção também se aplica a estatísticas filtradas.  
  
O padrão é ON. Nós recomendamos que você use a configuração padrão para a maioria dos bancos de dados.  
  
Use a opção AUTO_UPDATE_STATISTICS_ASYNC para especificar se as estatísticas são atualizadas de forma síncrona ou assíncrona.  
  
OFF  
Especifica que o otimizador de consulta não atualiza estatísticas quando elas são usadas por uma consulta e quando elas podem ficar desatualizadas. Definir essa opção como OFF pode acarretar planos de consulta de qualidade inferior e menor desempenho de consulta.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_update_stats_on na exibição do catálogo sys.databases ou a propriedade IsAutoUpdateStatistics da função DATABASEPROPERTYEX.  
  
Para obter mais informações, veja a seção “Usando as opções de estatísticas em todo o banco de dados” em [Estatística](../../relational-databases/statistics/statistics.md).  
  
<a name="auto_update_statistics_async"></a> AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
ON  
Especifica que atualizações de estatísticas para a opção AUTO_UPDATE_STATISTICS são assíncronas. O otimizador de consulta não aguarda a conclusão das atualizações de estatísticas para compilar consultas.  
  
Definir essa opção como ON não tem nenhum efeito, a menos que AUTO_UPDATE_STATISTICS seja definida como ON.  
  
Por padrão, a opção AUTO_UPDATE_STATISTICS_ASYNC é definida como OFF e o otimizador de consulta atualiza estatísticas de forma síncrona.  
  
OFF  
Especifica que atualizações de estatísticas para a opção AUTO_UPDATE_STATISTICS são síncronas. O otimizador de consulta aguarda a conclusão das atualizações de estatísticas para compilar consultas.  
  
Definir essa opção como OFF não tem nenhum efeito, a menos que AUTO_UPDATE_STATISTICS seja definida como ON.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_auto_update_stats_async_on na exibição do catálogo sys.databases.  
  
Para obter mais informações que descrevem quando usar atualizações de estatísticas síncronas ou assíncronas, veja a seção que "Usando as opções de estatísticas em todo o banco de dados" em [Estatísticas](../../relational-databases/statistics/statistics.md).  
  
<a name="auto_tuning"></a> **\<automatic_tuning_option> ::=**  
**Aplica-se a**: [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  

Habilita ou desabilita a opção de `FORCE_LAST_GOOD_PLAN` [ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md).  
  
FORCE_LAST_GOOD_PLAN = { ON | OFF }  
ON  
O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] força automaticamente o último plano sabidamente válido nas consultas [!INCLUDE[tsql-md](../../includes/tsql-md.md)] em que o novo plano SQL provoca regressões de desempenho. O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] monitora continuamente o desempenho de consultas da consulta [!INCLUDE[tsql-md](../../includes/tsql-md.md)] com o plano forçado. Se não houver ganhos de desempenho, o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] continuará usando o último plano válido conhecido. Se os ganhos de desempenho não forem detectados, o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] produzirá um novo plano SQL. A instrução falhará se o repositório de consultas não estiver habilitado ou não estiver no modo de *Leitura-Gravação*.   
OFF  
O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] relata possíveis regressões de desempenho de consulta causadas por alterações de plano SQL na exibição [sys.dm_db_tuning_recommendations](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md). No entanto, essas recomendações não são aplicadas automaticamente. Usuário pode monitorar recomendações ativas e corrigir problemas identificados aplicando scripts [!INCLUDE[tsql-md](../../includes/tsql-md.md)] mostrados na exibição. Este é o valor padrão.

**\<change_tracking_option> ::=**  
  
Controla as opções de controle de alterações. É possível habilitar o controle de alterações, definir opções, alterar opções e desabilitar o controle de alterações. Para obter exemplos, confira a seção Exemplos mais adiante neste artigo.  
  
ON  
Habilita o controle de alterações no banco de dados. Quando você habilita o controle de alterações, também pode definir as opções AUTO CLEANUP e CHANGE RETENTION.  
  
AUTO_CLEANUP = { ON | OFF }  
ON  
As informações de controle de alterações são removidas automaticamente depois do período de retenção especificado.  
  
OFF  
Os dados de controle de alterações não são removidos do banco de dados.  
  
CHANGE_RETENTION =*retention_period* { DAYS | HOURS | MINUTES }  
Especifica o período mínimo para manter as informações de controle de alterações no banco de dados. Os dados serão removidos somente quando o valor AUTO_CLEANUP for ON.  
  
*retention_period* é um inteiro que especifica o componente numérico do período de retenção.  
  
O período de retenção padrão é de 2 dias. O período de retenção mínimo é de 1 minuto. O tipo de retenção padrão é DAYS.  
  
OFF  
Desabilita o controle de alterações no banco de dados. É necessário desabilitar o controle de alterações em todas as tabelas antes de poder desabilitá-lo no banco de dados.  
  
**\<cursor_option> ::=**  
  
Controla opções de cursor.  
  
CURSOR_CLOSE_ON_COMMIT { ON | OFF }  
ON  
Qualquer cursor é aberto quando uma transação é confirmada ou quando uma transação revertida é fechada.  
  
OFF  
Os cursores permanecem abertos quando uma transação é confirmada; uma transação revertida fechará todos os cursores, exceto aqueles definidos como INSENSITIVE ou STATIC.  
  
As configurações no nível de conexão que são definidas com o uso da instrução SET substituem a configuração de banco de dados padrão por CURSOR_CLOSE_ON_COMMIT. Por padrão, clientes ODBC e OLE DB emitem uma configuração CURSOR_CLOSE_ON_COMMIT de instrução SET no nível de conexão como desativada para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET CURSOR_CLOSE_ON_COMMIT](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md).  
  
O status dessa opção pode ser determinado examinando-se a coluna is_cursor_close_on_commit_on na exibição do catálogo sys.databases ou a propriedade IsCloseCursorsOnCommitEnabled da função DATABASEPROPERTYEX. O cursor é implicitamente desalocado somente na desconexão. Para saber mais, confira [DECLARE CURSOR](../../t-sql/language-elements/declare-cursor-transact-sql.md).  
  
**\<db_encryption_option> ::=**  
  
Controla o estado de criptografia do banco de dados.  
  
ENCRYPTION {ON | OFF}  
Define o banco de dados a ser criptografado (ON) ou não criptografado (OFF). Para saber mais sobre criptografia de banco de dados, confira [Transparent Data Encryption](../../relational-databases/security/encryption/transparent-data-encryption.md) e [Transparent Data Encryption com o Banco de Dados SQL do Azure](../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md).  
  
Quando a criptografia estiver habilitada no nível de banco de dados, todos os grupos de arquivos serão criptografados. Qualquer novo grupo de arquivos herdará a propriedade criptografada. Se algum grupo de arquivos do banco de dados for definido como **READ ONLY**, haverá falha na operação de criptografia de banco de dados.  
  
É possível ver o estado da criptografia do banco de dados usando a exibição de gerenciamento dinâmico [sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md).  
  
**\<db_update_option> ::=**  
  
Controla se atualizações são permitidas no banco de dados.  
  
READ_ONLY  
Os usuários podem ler dados do banco de dados, mas não modificá-los.  
  
> [!NOTE]  
>  Para melhorar o desempenho da consulta, atualize as estatísticas antes de configurar um banco de dados como READ_ONLY. Se forem necessárias estatísticas adicionais depois de um banco de dados ser definido como READ_ONLY, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] criará estatísticas no tempdb. Para obter mais informações sobre estatísticas para um banco de dados somente leitura, veja [Estatísticas](../../relational-databases/statistics/statistics.md).  
  
READ_WRITE  
O banco de dados está disponível para operações de leitura e gravação.  
  
Para alterar esse estado, é necessário ter acesso exclusivo ao banco de dados.   
  
**\<db_user_access_option> ::=**  
  
Controla o acesso de usuários ao banco de dados.  
  
RESTRICTED_USER  
RESTRICTED_USER permite que somente os membros da função de banco de dados fixa db_owner e das funções de servidor fixas dbcreator e sysadmin conectem-se ao banco de dados, mas não limita seu número. Todas as conexões com o banco de dados são desconectadas no período especificado pela cláusula de término da instrução ALTER DATABASE. Depois que o banco de dados fizer a transição para o estado RESTRICTED_USER, as tentativas de conexão realizadas por usuários não qualificados serão recusadas.  **RESTRICTED_USER** não pode ser modificado com a instância Gerenciada do Banco de Dados de SQL.
  
MULTI_USER  
Todos os usuários com permissões apropriadas para se conectar ao banco de dados são permitidos.  
  
O status dessa opção pode ser determinado examinando-se a coluna user_access na exibição do catálogo sys.databases ou a propriedade UserAccess da função DATABASEPROPERTYEX.  
  
**\<delayed_durability_option> ::=**  
  
Controla se as transações são confirmadas completamente duráveis ou duráveis atrasadas.  
  
DISABLED  
Todas as transações após SET DISABLED são completamente duráveis. Todas as opções de durabilidade definidas em um bloco atômico ou instrução de confirmação são ignoradas.  
  
ALLOWED  
Todas as transações após SET ALLOWED são completamente duráveis ou duráveis atrasadas, dependendo da opção de durabilidade definida no bloco atômico ou instrução de confirmação.  
  
FORCED  
Todas as transações após SET FORCED são duráveis atrasadas. Todas as opções de durabilidade definidas em um bloco atômico ou instrução de confirmação são ignoradas.  
  
**\<PARAMETERIZATION_option> ::=**  
  
Controla a opção de parametrização.  
  
PARAMETERIZATION { SIMPLE | FORCED }  
SIMPLE  
As consultas são parametrizadas com base no comportamento padrão do banco de dados.  
  
FORCED  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parametriza todas as consultas feitas no banco de dados.  
  
A configuração atual dessa opção pode ser determinada examinando-se a coluna is_parameterization_forced na exibição do catálogo sys.databases.  
  
**\<query_store_options> ::=**  
  
ON | OFF | CLEAR [ ALL ]  
Controla se o repositório de consultas está habilitado neste banco de dados, além de controlar a remoção de conteúdo do repositório de consultas.  
  
ON  
Habilita o repositório de consultas.  
  
OFF  
Desabilita o repositório de consultas.  Este é o valor padrão.   
  
CLEAR  
Remove o conteúdo do repositório de consultas.  
  
OPERATION_MODE  
Descreve o modo de operação do repositório de consultas. Os valores válidos são READ_ONLY e READ_WRITE. No modo READ_WRITE, o repositório de consultas coleta e persiste as informações das estatísticas de execução do plano de consulta e do tempo de execução. No modo READ_ONLY, as informações podem ser lidas do repositório de consultas, mas novas informações não são adicionadas. Se o espaço máximo alocado do repositório de consultas tiver se esgotado, o repositório de consultas alterará o modo de operação para READ_ONLY.  
  
CLEANUP_POLICY  
Descreve a política de retenção de dados do repositório de consultas. STALE_QUERY_THRESHOLD_DAYS determina o número de dias que as informações de uma consulta são mantidas no repositório de consultas. STALE_QUERY_THRESHOLD_DAYS é do tipo **bigint**.  
  
DATA_FLUSH_INTERVAL_SECONDS  
Determina a frequência na qual os dados gravados no repositório de consultas é persistida no disco. Para otimizar o desempenho, os dados coletados pelo repositório de consultas são gravados de maneira assíncrona no disco. A frequência em que essa transferência assíncrona ocorre é configurada usando o argumento DATA_FLUSH_INTERVAL_SECONDS. DATA_FLUSH_INTERVAL_SECONDS é do tipo **bigint**.  
  
MAX_STORAGE_SIZE_MB  
Determina o espaço alocado para o repositório de consultas. MAX_STORAGE_SIZE_MB é do tipo **bigint**.  
  
INTERVAL_LENGTH_MINUTES  
Determina o intervalo de tempo em que os dados de estatísticas de execução do tempo de execução são agregados no repositório de consultas. Para otimizar o uso de espaço, as estatísticas de execução de tempo de execução no repositório de estatísticas de tempo de execução são agregadas em uma janela de tempo fixo. Essa janela de tempo fixo é configurada usando o argumento INTERVAL_LENGTH_MINUTES. INTERVAL_LENGTH_MINUTES é do tipo **bigint**.  
  
SIZE_BASED_CLEANUP_MODE  
Controla se a limpeza será ativada automaticamente quando a quantidade total de dados se aproximar do tamanho máximo:  
  
OFF  
Limpeza com base no tamanho não será ativada automaticamente. 
  
AUTO  
A limpeza com base em tamanho será ativada automaticamente quando o tamanho em disco atingir 90% do **max_storage_size_mb**. Limpeza com base no tamanho remove as consultas menos dispendiosas e mais antigas primeiro. Ele para a aproximadamente 80% do **max_storage_size_mb**.  Esse é o valor de configuração padrão.  
  
SIZE_BASED_CLEANUP_MODE é do tipo **nvarchar**.  
  
QUERY_CAPTURE_MODE  
Designa o modo de captura de consulta ativo no momento:  
  
ALL Todas as consultas são capturadas. Esse é o valor de configuração padrão.
  
AUTO Captura consultas de relevantes com base na contagem de execução e no consumo de recursos.  Esse é o valor de configuração padrão para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
NONE Parar de capturar novas consultas. O Repositório de Consultas continuará a coletar estatísticas de compilação e tempo de execução para consultas que já foram capturadas. Use essa configuração com cuidado, pois você poderá deixar de capturar consultas importantes.  
  
QUERY_CAPTURE_MODE é do tipo **nvarchar**.  
  
max_plans_per_query  
Um número inteiro que representa a quantidade máxima de planos de manutenção para cada consulta. O padrão é 200.  
  
**\<snapshot_option> ::=**  
  
Determina o nível de isolamento da transação.  
  
ALLOW_SNAPSHOT_ISOLATION { ON | OFF }  
ON  
Habilita a opção de Instantâneo no nível do banco de dados. Quando habilitada, as instruções DML começam a gerar versões de linha mesmo quando nenhuma transação usar Isolamento de Instantâneo. Quando essa opção está habilitada, as transações podem especificar o nível de isolamento da transação SNAPSHOT. Ao executar uma transação no nível de isolamento SNAPSHOT, todas as instruções consultam um instantâneo de dados, se houver um no início da instrução. Se uma transação que executa no nível de isolamento SNAPSHOT acessar dados em vários bancos de dados, ALLOW_SNAPSHOT_ISOLATION deverá ser definido como ON em todos os bancos de dados ou cada instrução na transação deverá usar dicas de bloqueio em qualquer referência em uma cláusula FROM para uma tabela em um banco de dados onde ALLOW_SNAPSHOT_ISOLATION seja OFF.  
  
OFF  
Desativa a opção de Instantâneo no nível do banco de dados. As transações não podem especificar o nível de isolamento da transação SNAPSHOT.  
  
Ao definir ALLOW_SNAPSHOT_ISOLATION para um novo estado (de ON para OFF, ou de OFF, para ON), ALTER DATABASE não retorna o controle para o chamador até que todas as transações existentes no banco de dados sejam confirmadas. Se o banco de dados já estiver no estado especificado na instrução ALTER DATABASE, o controle será retornado ao chamador imediatamente. Se a instrução ALTER DATABASE não for retornada rapidamente, use [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) para determinar se há transações de longa duração. Se a instrução ALTER DATABASE for cancelada, o banco de dados permanecerá no estado que estava quando ALTER DATABASE foi iniciada. A exibição do catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) indica o estado de transações de isolamento de instantâneo no banco de dados. Se **snapshot_isolation_state_desc** = IN_TRANSITION_TO_ON, ALTER DATABASE ALLOW_SNAPSHOT_ISOLATION OFF fará uma pausa de seis segundos e tentará novamente executar a operação.  
  
Não é possível alterar o estado de ALLOW_SNAPSHOT_ISOLATION se o banco de dados for OFFLINE.  
  
Se você definir ALLOW_SNAPSHOT_ISOLATION em um banco de dados READ_ONLY, a configuração será retida se o banco de dados for definido mais tarde como READ_WRITE.  
  
É possível alterar as configurações ALLOW_SNAPSHOT_ISOLATION para os bancos de dados mestre, modelo, msdb e tempdb. Se você alterar a configuração para tempdb, ela será retida sempre que a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] for interrompida e reiniciada. Ao alterar a configuração para modelo, ela se tornará o padrão para qualquer novo banco de dados que for criado, exceto para tempdb.  
  
A opção é ON, por padrão, para os bancos de dados mestre e msdb.  
  
A configuração atual dessa opção pode ser determinada examinando-se a coluna snapshot_isolation_state na exibição do catálogo sys.databases.  
  
READ_COMMITTED_SNAPSHOT { ON | OFF }  
ON  
Habilita a opção de Instantâneo de Leitura Confirmada no nível do banco de dados. Quando habilitada, as instruções DML começam a gerar versões de linha mesmo quando nenhuma transação usar Isolamento de Instantâneo. Quando essa opção está habilitada, as transações que especificam o nível de isolamento de leitura confirmada usam o controle de versão de linha, em vez de bloqueio. Quando uma transação é executada no nível de isolamento de leitura confirmada, todas as instruções consultam um instantâneo de dados, se houver um no início da instrução.  
  
OFF  
Desabilita a opção de Instantâneo de Leitura Confirmada no nível do banco de dados. As transações que especificam o nível de isolamento READ COMMITTED usam bloqueio.  
  
Para definir READ_COMMITTED_SNAPSHOT como ON ou OFF, não deve haver nenhuma conexão ativa com o banco de dados exceto para a que está executando o comando ALTER DATABASE. Entretanto, o banco de dados não precisa estar no modo de usuário único. Não é possível alterar o estado dessa opção quando o banco de dados for OFFLINE.  
  
Se você definir READ_COMMITTED_SNAPSHOT em um banco de dados READ_ONLY, a configuração será retida quando o banco de dados for definido mais tarde como READ_WRITE.  
  
READ_COMMITTED_SNAPSHOT não pode ser ativado como ON para os bancos de dados do sistema mestre, tempdb ou msdb. Se você alterar a configuração para modelo, ela se tornará o padrão para qualquer novo banco de dados que for criado, exceto para tempdb.  
  
A configuração atual dessa opção pode ser determinada examinando-se a coluna is_read_committed_snapshot_on na exibição do catálogo sys.databases.  
  
> [!WARNING]  
>  Quando uma tabela for criada com **DURABILITY = SCHEMA_ONLY**, e **READ_COMMITTED_SNAPSHOT** depois forem alterado usando **ALTER DATABASE**, os dados na tabela serão perdidos.  
  
MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT { ON | OFF }  
  
ON  
Quando o nível de isolamento da transação estiver configurado para qualquer nível de isolamento inferior ao SNAPSHOT (por exemplo, READ COMMITTED ou READ UNCOMMITTED), todas as operações interpretadas de [!INCLUDE[tsql](../../includes/tsql-md.md)] em tabelas com otimização de memória serão executadas em isolamento SNAPSHOT. Isso é feito mesmo que o nível de isolamento da transação seja definido explicitamente no nível de sessão ou se a opção for usada implicitamente.  
  
OFF  
Não eleva o nível de isolamento da transação para operações interpretadas do [!INCLUDE[tsql](../../includes/tsql-md.md)] em tabelas com otimização de memória.  
  
Não é possível alterar o estado de MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT se o banco de dados for OFFLINE.  
  
A opção é OFF, por padrão.  
  
A configuração atual dessa opção pode ser determinada, examinando a coluna **is_memory_optimized_elevate_to_snapshot_on** na exibição de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
**\<sql_option> ::=**  
  
Controla as opções de conformidade ANSI no nível de banco de dados.  
  
ANSI_NULL_DEFAULT { ON | OFF }  
Determina o valor padrão, NULL ou NOT NULL, de um [tipo definido pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) CLR ou coluna para o qual a nulidade não é definida explicitamente nas instruções CREATE TABLE ou ALTER TABLE. As colunas definidas com restrições seguem as regras de restrição apesar dessa configuração.  
  
ON  
O valor padrão é NULL.  
  
OFF  
O valor padrão é NOT NULL.  
  
As configurações no nível de conexão que são definidas com o uso de uma instrução SET substituem a configuração no nível de banco de dados padrão para ANSI_NULL_DEFAULT. Por padrão, clientes ODBC e OLE DB emitem uma configuração ANSI_NULL_DEFAULT de instrução SET no nível de conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET ANSI_NULL_DFLT_ON](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md).  
  
Para compatibilidade ANSI, definir a opção de banco de dados ANSI_NULL_DEFAULT como ON altera o banco de dados padrão para NULL.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_ansi_null_default_on na exibição do catálogo sys.databases ou a propriedade IsAnsiNullDefault da função DATABASEPROPERTYEX.  
  
ANSI_NULLS { ON | OFF }  
ON  
Todas as comparações com um valor nulo são avaliadas como UNKNOWN.  
  
OFF  
As comparações de valores não UNICODE com um valor nulo são avaliadas como TRUE se ambos os valores forem NULL.  
  
> [!IMPORTANT]  
>  Em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ANSI_NULLS sempre estará ON e quaisquer aplicativos que definam explicitamente a opção como OFF produzirão um erro. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
As configurações no nível de conexão que são definidas com o uso de uma instrução SET substituem a configuração no nível de banco de dados padrão para ANSI_NULLS. Por padrão, clientes ODBC e OLE DB emitem uma configuração ANSI_NULLS de instrução SET no nível de conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET ANSI_NULLS](../../t-sql/statements/set-ansi-nulls-transact-sql.md).  
  
SET ANSI_NULLS também deve ser definido como ON ao criar ou fazer alterações em índices em colunas computadas ou exibições indexadas.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_ansi_nulls_on na exibição do catálogo sys.databases ou a propriedade IsAnsiNullsEnabled da função DATABASEPROPERTYEX.  
  
ANSI_PADDING { ON | OFF }  
ON  
As cadeias de caracteres são preenchidas com o mesmo comprimento antes da conversão ou inserção em um tipo de dados **varchar** ou **nvarchar**.  
  
Espaços em branco à direita nos valores de caracteres inseridos nas colunas **varchar** ou **nvarchar** e os zeros à direita nos valores binários inseridos nas colunas **varbinary** não serão cortados. Os valores não são preenchidos com o tamanho da coluna.  
  
OFF  
Espaços em branco à direita para **varchar** ou **nvarchar** e zeros para **varbinary** são cortados.  
  
Quando OFF é especificado, essa configuração afeta apenas a definição de novas colunas.  
  
> [!IMPORTANT]  
>  Em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ANSI_PADDING sempre será ON e quaisquer aplicativos que definam explicitamente a opção como OFF produzirão um erro. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. É recomendável sempre definir ANSI_PADDING como ON. ANSI_PADDING deve ser ON ao criar ou manipular índices em colunas computadas ou exibições indexadas.  
  
As colunas **char(*n*)** e **binary(*n*)** que permitem valores nulos são preenchidas até o tamanho da coluna quando ANSI_PADDING está definido como ON, mas os brancos à direita e os zeros são cortados quando ANSI_PADDING está definido como OFF. As colunas **char(*n*)** e **binary(*n*)** que não permitem valores nulos sempre são preenchidas até o tamanho da coluna.  
  
As configurações no nível de conexão que são definidas com o uso de uma instrução SET substituem a configuração no nível de banco de dados padrão para ANSI_PADDING. Por padrão, clientes ODBC e OLE DB emitem uma configuração ANSI_PADDING da instrução SET no nível da conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET ANSI_PADDING](../../t-sql/statements/set-ansi-padding-transact-sql.md).  
  
O status dessa opção pode ser determinado examinando-se a coluna is_ansi_padding_on na exibição do catálogo sys.databases ou a propriedade IsAnsiPaddingEnabled da função DATABASEPROPERTYEX.  
  
ANSI_WARNINGS { ON | OFF }  
ON  
Erros ou avisos são emitidos quando condições como “divisão por zero” ou “valores nulos” aparecerem em funções de agregação.  
  
OFF  
Nenhum aviso é emitido e os valores nulos são retornados quando condições como “dividir por zero” ocorrem.  
  
SET ANSI_WARNINGS também deve ser definido como ON ao criar ou fazer alterações em índices em colunas computadas ou exibições indexadas.  
  
As configurações no nível de conexão que são definidas usando uma instrução SET substituem a configuração no nível de banco de dados padrão para ANSI_WARNINGS. Por padrão, clientes ODBC e OLE DB emitem uma configuração ANSI_WARNINGS de instrução SET no nível de conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET ANSI_PADDING](../../t-sql/statements/set-ansi-warnings-transact-sql.md).  
  
O status dessa opção pode ser determinado examinando-se a coluna is_ansi_warnings_on na exibição do catálogo sys.databases ou a propriedade IsAnsiWarningsEnabled da função DATABASEPROPERTYEX.  
  
ARITHABORT { ON | OFF }  
ON  
Uma consulta é encerrada quando ocorre um estouro ou erro de divisão por zero durante a execução da consulta.  
  
OFF  
Uma mensagem de aviso é exibida quando um desses erros ocorre, mas a consulta, o lote ou a transação continuam a ser processados como se nenhum erro tivesse ocorrido.  
  
SET ARITHABORT também deve ser definido como ON ao criar ou fazer alterações em índices em colunas computadas ou exibições indexadas.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_arithabort_on na exibição do catálogo sys.databases ou a propriedade IsArithmeticAbortEnabled da função DATABASEPROPERTYEX.  
  
COMPATIBILITY_LEVEL { 140 | 130 | 120 | 110 | 100 | 90 | 80 }   
Para saber mais, confira [ALTER DATABASE Compatibility Level](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
CONCAT_NULL_YIELDS_NULL { ON | OFF }  
ON  
O resultado de uma operação de concatenação será NULL quando qualquer operando for NULL. Por exemplo, concatenar a cadeia de caracteres "This is" e NULL gera o valor NULL, em vez do valor "This is".  
  
OFF  
O valor nulo é tratado como uma cadeia de caracteres vazia.  
  
CONCAT_NULL_YIELDS_NULL deve ser definido como ON ao criar ou fazer alterações em índices em colunas computadas ou exibições indexadas.  
  
> [!IMPORTANT]  
>  Em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], CONCAT_NULL_YIELDS_NULL sempre estará ON e quaisquer aplicativos que definam explicitamente a opção como OFF produzirão um erro. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
As configurações no nível de conexão que são definidas usando uma instrução SET substituem a configuração no nível de banco de dados padrão para CONCAT_NULL_YIELDS_NULL. Por padrão, clientes ODBC e OLE DB emitem uma configuração CONCAT_NULL_YIELDS_NULL de instrução SET no nível de conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET CONCAT_NULL_YIELDS_NULL](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).  
  
O status dessa opção pode ser determinado examinando-se a coluna is_concat_null_yields_null_on na exibição do catálogo sys.databases ou a propriedade IsNullConcat da função DATABASEPROPERTYEX.  
  
QUOTED_IDENTIFIER { ON | OFF }  
ON  
As aspas duplas podem ser utilizadas para conter identificadores delimitados.  
  
Todas as cadeias de caracteres delimitadas por aspas duplas são interpretadas como identificadores de objeto. Os identificadores entre aspas não precisam seguir as regras [!INCLUDE[tsql](../../includes/tsql-md.md)] para identificadores. Eles podem ser palavras-chave e incluir caracteres geralmente não permitidos nos identificadores [!INCLUDE[tsql](../../includes/tsql-md.md)]. Se o sinal de aspas simples (') fizer parte da cadeia de caracteres literal, ele poderá ser representado por aspas duplas (").  
  
OFF  
Os identificadores não podem estar entre aspas e devem seguir todas as regras de identificadores [!INCLUDE[tsql](../../includes/tsql-md.md)]. Literais podem ser delimitados por aspas simples ou duplas.  
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também permite que os identificadores sejam delimitados por colchetes ([ ]). Os identificadores entre colchetes podem sempre ser usados, seja qual for a configuração de QUOTED_IDENTIFIER. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
Quando uma tabela é criada, a opção QUOTED IDENTIFIER sempre é armazenada como ON nos metadados da tabela, mesmo que a opção esteja definida como OFF quando a tabela é criada.  
  
As configurações no nível de conexão que são definidas com o uso de uma instrução SET substituem a configuração no nível de banco de dados padrão para QUOTED_IDENTIFIER. Por padrão, clientes ODBC e OLE DB emitem uma configuração QUOTED_IDENTIFIER de instrução SET no nível de conexão como ON para a sessão ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber mais, confira [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
O status dessa opção pode ser determinado examinando-se a coluna is_quoted_identifier_on na exibição do catálogo sys.databases ou a propriedade IsQuotedIdentifiersEnabled da função DATABASEPROPERTYEX.  
  
NUMERIC_ROUNDABORT { ON | OFF }  
ON  
Um erro é gerado quando ocorre perda de precisão em uma expressão.  
  
OFF  
As perdas de precisão não geram mensagens de erro e o resultado é arredondado de acordo com a precisão da coluna ou variável que armazena o resultado.  
  
NUMERIC_ROUNDABORT deve ser definido como OFF ao criar ou fazer alterações em índices em colunas computadas ou exibições indexadas.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_numeric_roundabort_on na exibição do catálogo sys.databases ou a propriedade IsNumericRoundAbortEnabled da função DATABASEPROPERTYEX.  
  
RECURSIVE_TRIGGERS { ON | OFF }  
ON  
O disparo recursivo de gatilhos AFTER é permitido.  
  
OFF  
Apenas o disparo recursivo direto de gatilhos AFTER não é permitido. Para desabilitar também a recursão indireta de gatilhos AFTER, defina a opção do servidor de gatilhos aninhados como **0** usando **sp_configure**.  
  
> [!NOTE]  
>  Somente a recursão direta será evitada quando RECURSIVE_TRIGGERS estiver definido como OFF. Para desabilitar a recursão indireta, é necessário definir também a opção do servidor nested triggers como 0.  
  
O status dessa opção pode ser determinado examinando-se a coluna is_recursive_triggers_on na exibição do catálogo sys.databases ou a propriedade IsRecursiveTriggersEnabled da função DATABASEPROPERTYEX.  

**\<target_recovery_time_option> ::=**  
  
Especifica a frequência de pontos de verificação indiretos por banco de dados. Começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o valor padrão para novos bancos de dados é de 1 minuto, o que indica que o banco de dados usará pontos de verificação indiretos. Para versões mais antigas, o padrão é 0, o que indica que o banco de dados usará pontos de verificação automáticos cuja frequência depende da configuração do intervalo de recuperação da instância de servidor. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda 1 minuto para a maioria dos sistemas.  
  
TARGET_RECOVERY_TIME **=***target_recovery_time* { SECONDS | MINUTES }  
*target_recovery_time*  
Especifica o salto máximo no tempo para recuperar o banco de dados especificado no caso de uma falha.  
  
SECONDS  
Indica que *target_recovery_time* é expresso como o número de segundos.  
  
MINUTES  
Indica que *target_recovery_time* é expresso como o número de minutos.  
  
Para saber mais sobre pontos de verificação indiretos, confira [Pontos de verificação de banco de dados](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
ROLLBACK AFTER *integer* [SECONDS] | ROLLBACK IMMEDIATE  
Especifica se a reversão deve ser feita após o número de segundos especificado ou imediatamente.  
  
NO_WAIT  
Especifica que, se a alteração de estado do banco de dados ou da opção solicitada não puder ser concluída imediatamente sem esperar que as transações sejam confirmadas ou revertidas por si mesmas, a solicitação falhará.  
  
##  <a name="SettingOptions"></a> Opções de configuração  
Para recuperar as configurações atuais das opções de banco de dados, use a exibição do catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) ou [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)  
  
Depois de definir uma opção de banco de dados, a modificação entra em vigor imediatamente.  
  
Para alterar os valores padrão de qualquer uma das opções de banco de dados para todos os bancos de dados criados recentemente, altere a opção de banco de dados apropriada no banco de dados modelo.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-setting-the-database-to-readonly"></a>A. Configurando o banco de dados como READ_ONLY  
Alterar o estado de um banco de dados ou grupo de arquivos para READ_ONLY ou READ_WRITE requer acesso exclusivo ao banco de dados. O exemplo a seguir define o banco de dados como o modo `RESTRICTED_USER` para acesso restrito. Em seguida, o exemplo define o estado do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] como `READ_ONLY` e retorna o acesso ao banco de dados para todos os usuários.  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET RESTRICTED_USER;  
GO  
ALTER DATABASE AdventureWorks2012  
SET READ_ONLY  
GO  
ALTER DATABASE AdventureWorks2012  
SET MULTI_USER;  
GO  
  
```  
  
### <a name="b-enabling-snapshot-isolation-on-a-database"></a>B. Habilitando o isolamento de instantâneo em um banco de dados  
O exemplo a seguir habilita a opção de estrutura de isolamento de instantâneo para o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
USE AdventureWorks2012;  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET ALLOW_SNAPSHOT_ISOLATION ON;  
GO  
-- Check the state of the snapshot_isolation_framework  
-- in the database.  
SELECT name, snapshot_isolation_state,   
    snapshot_isolation_state_desc AS description  
FROM sys.databases  
WHERE name = N'AdventureWorks2012';  
GO  
  
```  
  
O conjunto de resultados mostra que a estrutura de isolamento de instantâneo está habilitada.  
  
|NAME |snapshot_isolation_state |descrição|  
|-------------------- |------------------------  |----------|  
|AdventureWorks2012   |1                        | ON |  
  
### <a name="c-enabling-modifying-and-disabling-change-tracking"></a>C. Habilitando, modificando e desabilitando o controle de alterações  
O exemplo a seguir habilita o controle de alterações no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e define o período de retenção para `2` dias.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = ON  
(AUTO_CLEANUP = ON, CHANGE_RETENTION = 2 DAYS);  
```  
  
O exemplo a seguir mostra como alterar o período de retenção para `3` dias.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING (CHANGE_RETENTION = 3 DAYS);  
```  
  
O exemplo a seguir mostra como desabilitar o controle de alterações no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = OFF;  
```  
  
### <a name="d-enabling-the-query-store"></a>D. Habilitando o repositório de consultas  
  
O exemplo a seguir habilita o repositório de consultas e configura os parâmetros do repositório de consultas.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET QUERY_STORE = ON   
    (  
      OPERATION_MODE = READ_WRITE   
    , CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 )  
    , DATA_FLUSH_INTERVAL_SECONDS = 900   
    , MAX_STORAGE_SIZE_MB = 1024   
    , INTERVAL_LENGTH_MINUTES = 60   
    );  
```  
  
## <a name="see-also"></a>Consulte Também  
[Nível de compatibilidade de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
[Espelhamento de banco de dados de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
[Estatística](../../relational-databases/statistics/statistics.md)   
[CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqldbmi)   
[Habilitar e desabilitar o controle de alterações](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)   
[DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)   
[DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)   
[SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
[sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
[Melhor prática com o Repositório de Consultas](../../relational-databases/performance/best-practice-with-the-query-store.md) 
  
::: moniker-end
