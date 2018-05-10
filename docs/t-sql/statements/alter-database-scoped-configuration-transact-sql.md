---
title: ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- ALTER_DATABASE_SCOPED_CONFIGURATION
- ALTER_DATABASE_SCOPED_CONFIGURATION_TSQL
- DATABASE_SCOPED_CONFIGURATION_TSQL
- SCOPED_CONFIGURATION_TSQL
- SCOPED_TSQL
- ALTER_DATABASE_SCOPED_TSQL
- DATABASE_SCOPED_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CONFIGURATION statement
- configuration [SQL Server], ALTER DATABASE SCOPED CONFIGURATION statement
ms.assetid: 63373c2f-9a0b-431b-b9d2-6fa35641571a
caps.latest.revision: 32
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9d9f156deb3fa8b59de0703da2b7f1f309862c16
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="alter-database-scoped-configuration-transact-sql"></a>ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Essa instrução permite várias definições de configuração de banco de dados no nível do **banco de dados individual**. Essa instrução está disponível no [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)] e no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Essas configurações são:  
  
- Limpar o cache de procedimento.  
- Definir o parâmetro MAXDOP para um valor arbitrário (1, 2,...) para o banco de dados primário com base naquilo que funciona melhor para esse banco de dados específico e definir um valor diferente (por exemplo, 0) para todos os bancos de dados secundários usados (como para consultas de relatórios).  
- Defina o modelo de estimativa de cardinalidade do otimizador de consulta independente do nível de compatibilidade do banco de dados.  
- Habilitar ou desabilitar a detecção de parâmetro no nível do banco de dados.
- Habilitar ou desabilitar hotfixes de otimização de consulta no nível do banco de dados.
- Habilitar ou desabilitar o cache de identidade no nível do banco de dados.
- Habilitar ou desabilitar um stub de plano compilado para ser armazenado em cache quando um lote for compilado pela primeira vez.  
- Habilite ou desabilite a coleta de estatísticas de execução para módulos T-SQL compilados nativamente.
  
 ![Ícone de link](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ALTER DATABASE SCOPED CONFIGURATION  
{        
     {  [ FOR SECONDARY] SET <set_options>  }    
}  
| CLEAR PROCEDURE_CACHE  
| SET < set_options >
[;]    
  
< set_options > ::=    
{  
    MAXDOP = { <value> | PRIMARY}    
    | LEGACY_CARDINALITY_ESTIMATION = { ON | OFF | PRIMARY}    
    | PARAMETER_SNIFFING = { ON | OFF | PRIMARY}    
    | QUERY_OPTIMIZER_HOTFIXES = { ON | OFF | PRIMARY}
    | IDENTITY_CACHE = { ON | OFF }
    | OPTIMIZE_FOR_AD_HOC_WORKLOADS = { ON | OFF }
    | XTP_PROCEDURE_EXECUTION_STATISTICS = { ON | OFF } 
    | XTP_QUERY_EXECUTION_STATISTICS = { ON | OFF }     
}  
```  
  
## <a name="arguments"></a>Argumentos  
 
FOR SECONDARY  
 
Especifica as definições para bancos de dados secundários (todos os bancos de dados secundários precisam ter valores idênticos).  
  
MAXDOP **=** {\<value> | PRIMARY }  
**\<value>**  
  
Especifica a configuração MAXDOP padrão que deve ser usada para instruções. 0 é o valor padrão e indica que a configuração do servidor será usada. O MAXDOP no escopo do banco de dados (a menos que esteja definido como 0) substitui o **max degree of parallelism** definido no nível do servidor por sp_configure. As dicas de consulta ainda podem substituir o MAXDOP no escopo do BD para ajustar consultas específicas que precisam de uma configuração diferente. Todas essas configurações são limitadas pelo MAXDOP definido para o grupo de carga de trabalho.   

Você pode usar a opção max degree of parallelism para limitar o número de processadores a serem usados na execução de plano paralela. O SQL Server considera os planos de execução paralela para consultas, operações de DDL (linguagem de definição de dados) do índice, inserção paralela, alteração online de coluna, coleta de estatísticas paralela e população de cursor estático e controlado por conjunto de chaves.
 
Para definir essa opção no nível da instância, confira [Configurar a opção max degree of parallelism de configuração do servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). 

> [!TIP] 
> Para fazer isso no nível da consulta, adicione a [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md) **MAXDOP**.  
  
PRIMARY  
  
Só pode ser definida para os secundários, enquanto o banco de dados está no primário e indica que a configuração será a definida para o primário. Se a configuração do primário for alterada, o valor nos secundários será alterado da maneira apropriada sem precisar ser definido explicitamente. **PRIMARY** é a configuração padrão dos secundários.  
  
LEGACY_CARDINALITY_ESTIMATION **=** { ON | **OFF** | PRIMARY }  

Permite que você defina o modelo de estimativa de cardinalidade do otimizador de consulta para o SQL Server 2012 e versões anteriores independentemente do nível de compatibilidade do banco de dados. O padrão é **OFF**, que define o modelo de estimativa de cardinalidade do otimizador de consulta com base no nível de compatibilidade do banco de dados. Definir como **ON** equivale a habilitar o [sinalizador de rastreamento 9481](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md). 

> [!TIP] 
> Para fazer isso no nível da consulta, adicione a [dica de consulta](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) **QUERYTRACEON**. Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, para fazer isso no nível da consulta, adicione a [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md) **USE HINT** em vez de usar o sinalizador de rastreamento. 
  
PRIMARY  
  
Esse valor só é válido nos secundários enquanto o banco de dados está no primário e especifica que a configuração do modelo de estimativa de cardinalidade do otimizador de consulta em todos os secundários será o valor definido para o primário. Se a configuração no primário para o modelo de estimativa de cardinalidade do otimizador de consulta for alterado, o valor nos secundários será alterado da maneira adequada. **PRIMARY** é a configuração padrão dos secundários.  
  
PARAMETER_SNIFFING **=** { **ON** | OFF | PRIMARY}  

Habilita ou desabilita a [detecção de parâmetro](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing). O padrão é ON. Isso é equivalente ao [Sinalizador de Rastreamento 4136](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).   

> [!TIP] 
> Para fazer isso no nível da consulta, confira a [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md) **OPTIMIZE FOR UNKNOWN**. Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, para fazer isso no nível da consulta, a [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md) **USE HINT** também está disponível. 
  
PRIMARY  
  
Esse valor só é válido nos secundários enquanto o banco de dados está no primário e especifica que o valor dessa configuração em todos os secundários será o valor definido para o primário. Se a configuração do primário para o uso de [detecção de parâmetro](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing) fora alterada, o valor nos secundários será alterado da maneira apropriada sem a necessidade de definir o valor dos secundários explicitamente. Essa é a configuração padrão para os secundários.  
  
QUERY_OPTIMIZER_HOTFIXES **=** { ON | **OFF** | PRIMARY }  

Habilita ou desabilita os hotfixes de otimização de consulta, independentemente do nível de compatibilidade do banco de dados. O padrão é **OFF**, que desabilita os hotfixes de otimização de consulta que foram lançados depois que o nível de compatibilidade mais alto disponível foi introduzido para uma versão específica de (pós-RTM). Definir como **ON** equivale a habilitar o [sinalizador de rastreamento 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).   

> [!TIP] 
> Para fazer isso no nível da consulta, adicione a [dica de consulta](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) **QUERYTRACEON**. Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, para fazer isso no nível da consulta, adicione a [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md) USE HINT em vez de usar o sinalizador de rastreamento.  
  
PRIMARY  
  
Esse valor só é válido nos secundários enquanto o banco de dados está no primário e especifica que o valor dessa configuração em todos os secundários será o valor definido para o primário. Se a configuração do primário for alterada, o valor nos secundários será alterado da maneira apropriada sem precisar ser definido explicitamente. Essa é a configuração padrão para os secundários.  
  
CLEAR PROCEDURE_CACHE  

Limpa o cache de procedimento (plano) do banco de dados. Pode ser executado tanto nos primários quanto nos secundários.  

IDENTITY_CACHE **=** { **ON** | OFF }  

**Aplica-se a**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

Habilita ou desabilita o cache de identidade no nível do banco de dados. O padrão é **ON**. O cache de identidade é usado para melhorar o desempenho de INSERT em tabelas com colunas de identidade. Para evitar lacunas nos valores de uma coluna de identidade em casos em que o servidor é reiniciado inesperadamente ou efetua failover para um servidor secundário, desabilite a opção IDENTITY_CACHE. Essa opção é semelhante ao [sinalizador de rastreamento 272](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) existente, exceto que ela pode ser definida no nível do banco de dados em vez de apenas no nível do servidor.   

> [!NOTE] 
> Essa opção só pode ser definida para o primário. Para obter mais informações, confira [colunas de identidade](create-table-transact-sql-identity-property.md).  

OPTIMIZE_FOR_AD_HOC_WORKLOADS **=** { ON | **OFF** }  

**Aplica-se ao**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)] 

Habilita ou desabilita um stub de plano compilado para ser armazenado em cache quando um lote é compilado pela primeira vez. O padrão é OFF. Quando a configuração no escopo do banco de dados OPTIMIZE_FOR_AD_HOC_WORKLOADS estiver habilitada para um banco de dados, um stub de plano compilado será armazenado em cache quando um lote for compilado pela primeira vez. Os stubs de plano têm um volume de memória menor em comparação com o tamanho do plano compilado completo.  Se um lote for compilado ou executado novamente, o stub de plano compilado será removido e substituído por um plano compilado completo.

XTP_PROCEDURE_EXECUTION_STATISTICS  **=** { ON | **OFF** }  

**Aplica-se ao**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 

Habilita ou desabilita a coleta de estatísticas de execução no nível do módulo para módulos T-SQL compilados nativamente no banco de dados atual. O padrão é OFF. As estatísticas de execução são refletidas em [sys.dm_exec_procedure_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md).

As estatísticas de execução de nível de módulo para módulos T-SQL compilados nativamente serão coletadas se esta opção estiver ATIVADA ou se a coleta de estatísticas for habilitada por meio de [sp_xtp_control_proc_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md).

XTP_QUERY_EXECUTION_STATISTICS  **=** { ON | **OFF** }  

**Aplica-se ao**: [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]

Habilita ou desabilita a coleta de estatísticas de execução no nível de instrução para módulos T-SQL compilados nativamente no banco de dados atual. O padrão é OFF. As estatísticas de execução são refletidas em [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) e no [Repositório de Consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).

As estatísticas de execução de nível de instrução para módulos T-SQL compilados nativamente serão coletadas se esta opção estiver ATIVADA ou se a coleta de estatísticas for habilitada por meio de [sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md).

Para ver mais detalhes sobre monitoramento de desempenho de módulos T-SQL compilados nativamente, consulte [Monitorando o desempenho de procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/monitoring-performance-of-natively-compiled-stored-procedures.md).

##  <a name="Permissions"></a> Permissões  
 Requer ALTER ANY DATABASE SCOPE CONFIGURATION   
no banco de dados. Essa permissão pode ser concedida por um usuário com a permissão CONTROL em um banco de dados.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Embora seja possível configurar bancos de dados secundários para com definições de configuração de escopo diferentes do primário, todos os bancos de dados secundários usam a mesma configuração. As configurações diferentes não podem ser configuradas para secundários individuais.  
  
 Executar essa instrução limpa o cache de procedimento no banco de dados atual, que significa que todas as consultas precisarão ser recompiladas.  
  
 Para consultas de nome de três partes, as configurações da conexão de banco de dados atual da consulta são cumpridas, já para os módulos SQL (como procedimentos, funções e gatilhos), que são compilados no contexto atual do banco de dados, são usadas as opções do banco de dados no qual eles residem.  
  
 O evento ALTER_DATABASE_SCOPED_CONFIGURATION é adicionado como um evento DDL que pode ser usado para acionar um gatilho DDL. Este é um filho do grupo de gatilhos ALTER_DATABASE_EVENTS.  
 
 As definições de configurações no escopo do banco de dados serão transferidas para o banco de dados. Isso significa que quando um determinado banco de dados é restaurado ou anexado, as definições de configuração existentes permanecem.
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
**MAXDOP**  
  
 As configurações granulares podem substituir as globais e o Resource Governor pode limitar a todas as outras configurações de MAXDOP.  A lógica para a configuração de MAXDOP é a seguinte:  
  
-   A dica de consulta substitui sp_configure e a configuração no escopo do banco de dados. Se o grupo de recursos MAXDOP estiver definido para o grupo de carga de trabalho:  
  
    -   Se a dica de consulta for definida como 0, ela será substituído pela configuração do Resource Governor.  
  
    -   Se a dica de consulta não for 0, ela será limitada pela configuração do Resource Governor.  
  
-   A configuração no escopo do BD (a menos que seja 0) substitui a configuração de sp_configure, a menos que haja uma dica de consulta e ela seja limitada pela configuração do Resource Governor.  
  
-   A configuração de sp_configure é substituída pela configuração do Resource Governor.  
  
**QUERY_OPTIMIZER_HOTFIXES**  
  
 Quando a dica QUERYTRACEON for usada para habilitar o otimizador de consulta herdado ou hotfixes do otimizador de consulta, ele será uma condição OR entre a dica de consulta e a definição de configuração no escopo do banco de dados, significando que se uma das duas estiver habilitada, as opções serão aplicadas.  
  
**GeoDR**  
  
 Os bancos de dados secundários legíveis, por exemplo, os Grupos de Disponibilidade AlwaysOn e a Replicação Geográfica, usam o valor secundário verificando o estado do banco de dados. Embora a recompilação não ocorra no failover e tecnicamente o novo primário tenha consultas que usam as configurações do secundário, a ideia é que a configuração entre o primário e o secundário apenas varie quando a carga de trabalho for diferente e, portanto, as consultas armazenadas em cache estiverem usando as configurações ideais, enquanto as novas consultas estarão selecionando as novas configurações apropriadas para elas.  
  
**DacFx**  
  
 Como ALTER DATABASE SCOPED CONFIGURATION é um novo recurso no Banco de Dados SQL do Azure e no SQL Server, começando com o SQL Server 2016, que afeta o esquema do banco de dados, as exportações do esquema (com ou sem dados) não podem importadas para uma versão mais antiga do SQL Server, por exemplo, o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou o [!INCLUDE[ssSQLv14](../../includes/sssqlv14-md.md)]. Por exemplo, uma exportação para um [DACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3) ou um [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) de um [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ou de um banco de dados do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] que tiver usado esse novo recurso não poderá ser importada em um servidor de nível inferior.  
  
## <a name="metadata"></a>Metadados  

O Modo de Exibição do Sistema [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) fornece informações sobre as configurações no escopo em um banco de dados. As opções de configuração no escopo do banco de dados só aparecem em sys.database_scoped_configurations porque elas são substituições das configurações padrão de todo o servidor. O Modo de Exibição do Sistema [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) mostra apenas as configurações de todo o servidor.  
  
## <a name="examples"></a>Exemplos  
Esses exemplos demonstram o uso de ALTER DATABASE SCOPED CONFIGURATION  
  
### <a name="a-grant-permission"></a>A. Conceder permissão  

Este exemplo concede a permissão necessária para executar ALTER DATABASE SCOPED CONFIGURATION     
para o usuário [Joe].  
  
```sql  
GRANT ALTER ANY DATABASE SCOPED CONFIGURATION to [Joe] ;  
```  
  
### <a name="b-set-maxdop"></a>B. Definir MAXDOP  

Este exemplo define MAXDOP = 1 para um banco de dados primário e MAXDOP = 4 para um banco de dados secundário em um cenário de replicação geográfica.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION SET MAXDOP = 1 ;  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=4 ;  
```  
  
Este exemplo define MAXDOP para um banco de dados secundário como o mesmo que está definido para seu banco de dados primário em um cenário de replicação geográfica.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=PRIMARY ;
```  
  
### <a name="c-set-legacycardinalityestimation"></a>C. Definir LEGACY_CARDINALITY_ESTIMATION  

Este exemplo define LEGACY_CARDINALITY_ESTIMATION como ON para um banco de dados secundário em um cenário de replicação geográfica.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=ON ;  
```  
  
Este exemplo define LEGACY_CARDINALITY_ESTIMATION para um banco de dados secundário como o mesmo que está definido para seu banco de dados primário em um cenário de replicação geográfica.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=PRIMARY ;  
```  
  
### <a name="d-set-parametersniffing"></a>D. Definir PARAMETER_SNIFFING  

Este exemplo define PARAMETER_SNIFFING como OFF para um banco de dados primário em um cenário de replicação geográfica.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION SET PARAMETER_SNIFFING =OFF ;  
```  
  
Este exemplo define PARAMETER_SNIFFING como OFF para um banco de dados primário em um cenário de replicação geográfica.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=OFF ;  
```  
  
Este exemplo define PARAMETER_SNIFFING para um banco de dados secundário como o mesmo que está definido em seu banco de dados primário em um cenário de replicação geográfica.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=PRIMARY ;  
```  
  
### <a name="e-set-queryoptimizerhotfixes"></a>E. Definir QUERY_OPTIMIZER_HOTFIXES  

Defina QUERY_OPTIMIZER_HOTFIXES como ON para um banco de dados primário em um cenário de replicação geográfica.  

```sql  
ALTER DATABASE SCOPED CONFIGURATION SET QUERY_OPTIMIZER_HOTFIXES=ON ;  
```  
  
### <a name="f-clear-procedure-cache"></a>F. Limpar o cache de procedimento  

Este exemplo limpa o cache de procedimento (é possível somente para um banco de dados primário).  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE ;  
```  

### <a name="g-set-identitycache"></a>G. Definir IDENTITY_CACHE

**Aplica-se a**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)] (o recurso está na versão prévia pública) 

Este exemplo desabilita o cache de identidade.

```sql 
ALTER DATABASE SCOPED CONFIGURATION SET IDENTITY_CACHE=OFF ; 
```

### <a name="h-set-optimizeforadhocworkloads"></a>H. Definir OPTIMIZE_FOR_AD_HOC_WORKLOADS

**Aplica-se ao**: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

Este exemplo habilita um stub de plano compilado para ser armazenado em cache quando um lote é compilado pela primeira vez.

```sql 
ALTER DATABASE SCOPED CONFIGURATION SET OPTIMIZE_FOR_AD_HOC_WORKLOADS = ON;
```

## <a name="additional-resources"></a>Recursos adicionais

### <a name="maxdop-resources"></a>Recursos de MAXDOP 
* [Grau de paralelismo](../../relational-databases/query-processing-architecture-guide.md#DOP)
* [Recomendações e diretrizes para a opção de configuração "max degree of parallelism" do SQL Server ](https://support.microsoft.com/en-us/kb/2806535) 

### <a name="legacycardinalityestimation-resources"></a>Recursos de LEGACY_CARDINALITY_ESTIMATION    
* [Estimativa de cardinalidade (SQL Server)](../../relational-databases/performance/cardinality-estimation-sql-server.md)
* [Otimizar os planos de consulta com o avaliador de cardinalidade do SQL Server 2014](https://msdn.microsoft.com/library/dn673537.aspx)

### <a name="parametersniffing-resources"></a>Recursos de PARAMETER_SNIFFING    
* [Detecção de parâmetros](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)
* ["I smell a parameter!"](https://blogs.msdn.microsoft.com/queryoptteam/2006/03/31/i-smell-a-parameter/) (Sinto cheiro de parâmetro!)

### <a name="queryoptimizerhotfixes-resources"></a>Recursos de QUERY_OPTIMIZER_HOTFIXES    
* [Sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
* [Modelo de serviço do sinalizador de rastreamento 4199 de hotfix do otimizador de consulta do SQL Server](https://support.microsoft.com/en-us/kb/974006)

## <a name="more-information"></a>Mais informações  
 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)   
 [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [Exibições de catálogo de bancos de dados e de arquivos](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [Opções de configuração do servidor](../../database-engine/configure-windows/server-configuration-options-sql-server.md) [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)  
 
