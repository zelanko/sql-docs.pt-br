---
title: "ALTERAR a configuração de escopo do banco de dados (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/04/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "32"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: cc17063b8f74e296562a460677121c5ef1c85016
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="alter-database-scoped-configuration-transact-sql"></a>ALTERAR a configuração de escopo do banco de dados (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Essa instrução permite que várias definições de configuração de banco de dados no **banco de dados individual** nível. Essa instrução está disponível em [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] e no SQL Server a partir [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Essas configurações são:  
  
- Limpar o cache de procedimento.  
  
- Definir o parâmetro MAXDOP para um valor arbitrário (1,2,...) para o banco de dados primário com base no que funciona melhor para desse banco de dados e define um valor diferente (por exemplo, 0) para todos os banco de dados secundário usado (por exemplo, para consultas de relatórios).  
  
- Defina o modelo de estimativa de cardinalidade do otimizador de consulta independente do nível de compatibilidade do banco de dados.  
  
- Habilitar ou desabilitar a detecção de parâmetro no nível do banco de dados.
  
- Habilitar ou desabilitar hotfixes de otimização de consulta no nível do banco de dados.

- Habilitar ou desabilitar o cache de identidade no nível de banco de dados.

- Habilitar ou desabilitar um stub de plano compilado para ser armazenado em cache quando um lote é compilado pela primeira vez. 
  
 ![ícone de link](../../database-engine/configure-windows/media/topic-link.gif "ícone de link") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
}  
```  
  
## <a name="arguments"></a>Argumentos  
 
PARA SECUNDÁRIO  
 
Especifica as definições de bancos de dados secundários (todos os bancos de dados secundários devem ter os valores idênticos).  
  
MAXDOP  **=**  {\<valor > | PRIMÁRIO}  
**\<valor >**  
  
Especifica o padrão MAXDOP configuração deve ser usada para instruções. 0 é o valor padrão e indica que a configuração do servidor será usada. Substituições de MAXDOP no escopo do banco de dados (a menos que ele é definido como 0) a **grau máximo de paralelismo** definido no nível do servidor por sp_configure. Dicas de consulta ainda podem substituir o banco de dados no escopo MAXDOP para ajustar consultas específicas que precisam de uma configuração diferente. Todas essas configurações são limitadas pelo MAXDOP definido para o grupo de carga de trabalho.   

Você pode usar a opção max degree of parallelism para limitar o número de processadores a serem usados na execução de plano paralela. SQL Server considera os planos de execução paralela para consultas, operações do índice data definition language (DDL), inserção paralela, alteração online de coluna, coleta de estatísticas paralela e população de cursor estático e controlado por.
 
Para definir essa opção no nível de instância, consulte [configurar o grau máximo de paralelismo opção de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). 

> [!TIP] 
> Para fazer isso no nível da consulta, adicione o **MAXDOP** [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md).  
  
PRIMARY  
  
Só pode ser definida para os secundários, enquanto o banco de dados no primário e indica que a configuração será um conjunto para o primário. Se a configuração para as principais alterações, o valor em secundários alterará adequadamente sem a necessidade de definir secundários valor explicitamente. **PRIMÁRIO** é a configuração padrão para os secundários.  
  
LEGACY_CARDINALITY_ESTIMATION  **=**  {ON | **OFF** | PRIMÁRIO}  

Permite que você defina o modelo de estimativa de cardinalidade do otimizador de consulta para o SQL Server 2012 e a versão anterior independente do nível de compatibilidade do banco de dados. O padrão é **OFF**, que define o modelo de estimativa de cardinalidade de Otimizador de consulta com base no nível de compatibilidade do banco de dados. A definição para **ON** equivale a habilitar [sinalizador de rastreamento 9481](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md). 

> [!TIP] 
> Para fazer isso no nível da consulta, adicione o **QUERYTRACEON** [dica de consulta](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md). Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, para fazer isso no nível da consulta, adicione o **dica USE** [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md) em vez de usar o sinalizador de rastreamento. 
  
PRIMARY  
  
Esse valor só é válido em secundários enquanto o banco de dados no primário e especifica que a configuração de modelo de consulta optimizer cardinalidade estimativa em todos os secundários será o valor definido para o primário. Se a configuração do primário para o modelo de estimativa de cardinalidade de Otimizador de consulta for alterado, o valor em secundários mudará adequadamente. **PRIMÁRIO** é a configuração padrão para os secundários.  
  
PARAMETER_SNIFFING  **=**  { **ON** | DESATIVAR | PRIMÁRIO}  

Habilita ou desabilita [detecção de parâmetro](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing). O padrão é ON. Isso é equivalente ao [Sinalizador de Rastreamento 4136](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).   

> [!TIP] 
> Para fazer isso no nível da consulta, consulte o **OPTIMIZE FOR UNKNOWN** [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md). Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, para fazer isso no nível da consulta, o **dica USE** [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md) também está disponível. 
  
PRIMARY  
  
Esse valor só é válido em secundários enquanto o banco de dados no primário e especifica que o valor para essa configuração em todos os secundários será o valor definido para o primário. Se a configuração do primário para o uso de [detecção de parâmetro](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing) alterações, o valor em secundários mudará adequadamente sem a necessidade de definir secundários valor explicitamente. Essa é a configuração padrão para os secundários.  
  
QUERY_OPTIMIZER_HOTFIXES  **=**  {ON | **OFF** | PRIMÁRIO}  

Habilita ou desabilita os hotfixes de otimização de consulta, independentemente do nível de compatibilidade do banco de dados. O padrão é **OFF**, que desabilita os hotfixes de otimização que foram lançados após o mais alto nível de compatibilidade disponível foi introduzido para uma versão específica de consulta (post-RTM). A definição para **ON** equivale a habilitar [sinalizador de rastreamento 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).   

> [!TIP] 
> Para fazer isso no nível da consulta, adicione o **QUERYTRACEON** [dica de consulta](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md). Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, para fazer isso no nível da consulta, adicione a dica USE [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md) em vez de usar o sinalizador de rastreamento.  
  
PRIMARY  
  
Esse valor só é válido em secundários enquanto o banco de dados no primário e especifica que o valor para essa configuração em todos os secundários é o valor definido para o primário. Se a configuração para as principais alterações, o valor em secundários altera adequadamente sem a necessidade de definir secundários valor explicitamente. Essa é a configuração padrão para os secundários.  
  
LIMPAR PROCEDURE_CACHE  

Limpa o cache de procedimento (plano) para o banco de dados. Isso pode ser executado nos primários e secundários.  

IDENTITY_CACHE  **=**  { **ON** | OFF}  

**Aplica-se a**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

Habilita ou desabilita o cache de identidade no nível de banco de dados. O padrão é **ON**. Cache de identidade é usado para melhorar o desempenho de INSERT em tabelas com colunas de identidade. Para evitar lacunas nos valores de uma coluna de identidade em casos em que o servidor reinicia inesperadamente ou o failover para um servidor secundário, desabilite a opção IDENTITY_CACHE. Essa opção é semelhante à existente [272 do sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md), exceto que ela pode ser definida no nível do banco de dados em vez de apenas no nível do servidor.   

> [!NOTE] 
> Essa opção só pode ser definida para o primário. Para obter mais informações, consulte [colunas de identidade](create-table-transact-sql-identity-property.md).  

OPTIMIZE_FOR_AD_HOC_WORKLOADS  **=**  {ON | **OFF** }  

**Aplica-se ao**: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

Habilita ou desabilita um stub de plano compilado para ser armazenado em cache quando um lote é compilado pela primeira vez. O padrão é OFF. Depois que a configuração de escopo do banco de dados que optimize_for_ad_hoc_workloads está habilitado para um banco de dados, um stub de plano compilado será armazenada em cache quando um lote é compilada pela primeira vez. Stubs de plano tem um espaço de memória menor em comparação com o tamanho do plano compilado completo.  Se um lote é compilado ou executado novamente, o stub de plano compilado será removido e substituído por um plano compilado completo.

##  <a name="Permissions"></a> Permissões  
 Requer alterar qualquer configuração de escopo do banco de dados   
no banco de dados. Essa permissão pode ser concedida por um usuário com permissão CONTROL em um banco de dados.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Embora seja possível configurar bancos de dados secundários para que as definições de configuração de escopo diferente de seu primário, todos os bancos de dados secundários usam a mesma configuração. Configurações diferentes não podem ser configuradas para secundários individuais.  
  
 Executar essa instrução limpa o cache de procedimento no banco de dados atual, que significa que todas as consultas têm a recompilação.  
  
 Para consultas de nome de parte 3, as configurações para a conexão de banco de dados atual para a consulta é cumpridas diferente para os módulos SQL (como procedimentos, funções e gatilhos) que são compilados no contexto atual do banco de dados e, portanto, usa as opções das o banco de dados no qual residem.  
  
 O evento ALTER_DATABASE_SCOPED_CONFIGURATION é adicionado como um evento DDL que pode ser usado para acionar um gatilho DDL. Este é um filho do grupo ALTER_DATABASE_EVENTS gatilho.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
**MAXDOP**  
  
 As configurações granulares podem substituir os global e o administrador de recursos pode limitar a todas as outras configurações de MAXDOP.  A lógica para a configuração de MAXDOP é o seguinte:  
  
-   Dica de consulta substitui sp_configure e o banco de dados no escopo definindo. Se o grupo de recursos MAXDOP estiver definido para o grupo de carga de trabalho:  
  
    -   Se a dica de consulta é definida como 0, ele é substituído pelo administrador de recursos de configuração.  
  
    -   Se a dica de consulta é não 0, ele é limitado pelo administrador de recursos de configuração.  
  
-   O banco de dados no escopo definindo (a menos que ele é 0) substitui a configuração de sp_configure, a menos que haja uma dica de consulta e é controlada pelo administrador de recursos de configuração.  
  
-   A configuração sp_configure é substituída pelo administrador de recursos de configuração.  
  
**QUERY_OPTIMIZER_HOTFIXES**  
  
 Quando a dica QUERYTRACEON é usada para permitir que o otimizador de consulta herdados ou hotfixes do otimizador de consulta, ele seria uma condição OR entre a dica de consulta e a configuração de escopo do banco de dados, configuração, o que significa que se o estiver habilitada, as opções se aplicam.  
  
**GeoDR**  
  
 Legíveis bancos de dados secundários, por exemplo, grupos de disponibilidade AlwaysOn e GeoReplication, usam o valor secundário, verificando o estado do banco de dados. Embora recompilação não ocorrerá failover e tecnicamente o novo primário tem consultas que estão usando as configurações do secundárias, a ideia é que a configuração entre o primário e secundário variar apenas quando a carga de trabalho é diferente e, portanto, as consultas armazenadas em cache usando as configurações ideais, enquanto a novas consultas escolher as novas configurações que são apropriadas para eles.  
  
**DacFx**  
  
 Como ALTER DATABASE SCOPED CONFIGURATION é um novo recurso do SQL Server 2016 que afeta o esquema de banco de dados, exportações do esquema (com ou sem dados) não são poderá ser importado para uma versão mais antiga do SQL Server a partir do banco de dados do SQL Azure e SQL Server Por exemplo, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou [!INCLUDE[ssSQLv14](../../includes/sssqlv14-md.md)]. Por exemplo, uma exportação para um [DACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3) ou um [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) de um [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ou [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] banco de dados usado esse novo recurso não poderá ser importado para um servidor de nível inferior.  
  
## <a name="metadata"></a>Metadados  

O [sys. database_scoped_configurations &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) exibição do sistema fornece informações sobre as configurações no escopo em um banco de dados. Opções de configuração no escopo do banco de dados só aparecem em sys. database_scoped_configurations conforme eles são substituições para as configurações padrão de todo o servidor. O [Configurations &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) exibição do sistema mostra apenas as configurações de todo o servidor.  
  
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
  
Este exemplo define MAXDOP para um banco de dados secundário para ser o mesmo é definida para seu banco de dados primário em um cenário de replicação geográfica.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=PRIMARY ;
```  
  
### <a name="c-set-legacycardinalityestimation"></a>C. Definir LEGACY_CARDINALITY_ESTIMATION  

Este exemplo define LEGACY_CARDINALITY_ESTIMATION como ON para um banco de dados secundário em um cenário de replicação geográfica.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=ON ;  
```  
  
Este exemplo define LEGACY_CARDINALITY_ESTIMATION para um banco de dados secundário, assim como para seu banco de dados primário em um cenário de replicação geográfica.  
  
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
  
Este exemplo define PARAMETER_SNIFFING banco de dados secundário, pois ela está no banco de dados primário em um cenário de replicação geográfica.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=PRIMARY ;  
```  
  
### <a name="e-set-queryoptimizerhotfixes"></a>E. Definir QUERY_OPTIMIZER_HOTFIXES  

Defina QUERY_OPTIMIZER_HOTFIXES como ON para um banco de dados primário em um cenário de replicação geográfica.  

```sql  
ALTER DATABASE SCOPED CONFIGURATION SET QUERY_OPTIMIZER_HOTFIXES=ON ;  
```  
  
### <a name="f-clear-procedure-cache"></a>F. Limpar o Cache de procedimento  

Este exemplo limpa o cache de procedimento (é possível somente para um banco de dados primário).  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE ;  
```  

### <a name="g-set-identitycache"></a>G. Definir IDENTITY_CACHE

**Aplica-se a**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)] (o recurso está em visualização pública) 

Este exemplo desabilita o cache de identidade.

```sql 
ALTER DATABASE SCOPED CONFIGURATION SET IDENTITY_CACHE=OFF ; 
```

### <a name="h-set-optimizeforadhocworkloads"></a>H. Definir OPTIMIZE_FOR_AD_HOC_WORKLOADS

**Aplica-se ao**: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

Este exemplo habilita um stub de plano compilado ser armazenado em cache quando um lote é compilado pela primeira vez.

```sql 
ALTER DATABASE SCOPED CONFIGURATION SET OPTIMIZE_FOR_AD_HOC_WORKLOADS = ON;
```

## <a name="additional-resources"></a>Recursos adicionais

### <a name="maxdop-resources"></a>Recursos MAXDOP 
* [Grau de paralelismo](../../relational-databases/query-processing-architecture-guide.md#DOP)
* [Recomendações e diretrizes para a opção de configuração "grau máximo de paralelismo" no SQL Server](https://support.microsoft.com/en-us/kb/2806535) 

### <a name="legacycardinalityestimation-resources"></a>Recursos LEGACY_CARDINALITY_ESTIMATION    
* [Estimativa de cardinalidade (SQL Server)](../../relational-databases/performance/cardinality-estimation-sql-server.md)
* [Otimizar os planos de consulta com o avaliador de cardinalidade do SQL Server 2014](https://msdn.microsoft.com/library/dn673537.aspx)

### <a name="parametersniffing-resources"></a>Recursos PARAMETER_SNIFFING    
* [Detecção de parâmetros](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)
* ["Eu sentir um parâmetro!"](https://blogs.msdn.microsoft.com/queryoptteam/2006/03/31/i-smell-a-parameter/)

### <a name="queryoptimizerhotfixes-resources"></a>Recursos QUERY_OPTIMIZER_HOTFIXES    
* [Sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
* [SQL Server query optimizer hotfix rastreamento sinalizador 4199 modelo de serviço](https://support.microsoft.com/en-us/kb/974006)

## <a name="more-information"></a>Mais informações  
 [sys. database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)   
 [Configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [Exibições de catálogo de arquivos e bancos de dados](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [Opções de configuração de servidor](../../database-engine/configure-windows/server-configuration-options-sql-server.md) [Configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)  
 
