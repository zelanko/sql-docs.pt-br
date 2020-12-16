---
description: CREATE WORKLOAD GROUP (Transact-SQL)
title: CREATE WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/27/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD GROUP
- WORKLOAD_GROUP_TSQL
- CREATE WORKLOAD GROUP
- CREATE_WORKLOAD_GROUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD GROUP statement
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: e86f0221b1acbf6cfe7b946a60e1b147dfbe7151
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489009"
---
# <a name="create-workload-group-transact-sql"></a>CREATE WORKLOAD GROUP (Transact-SQL)

[!INCLUDE[select-product](../../includes/select-product.md)]

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017"

:::row:::
    :::column:::
        **_\* SQL Server \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Instância Gerenciada de SQL](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](create-workload-group-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-server-and-sql-managed-instance"></a>SQL Server e Instância Gerenciada de SQL

[!INCLUDE [CREATE WORKLOAD GROUP](../../includes/create-workload-group.md)]
  
::: moniker-end
::: moniker range="=azuresqldb-mi-current"

:::row:::
    :::column:::
        [SQL Server](create-workload-group-transact-sql.md?view=sql-server-ver15&preserve-view=true)
    :::column-end:::
    :::column:::
        **_\* Instância Gerenciada de SQL \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](create-workload-group-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-server-and-sql-managed-instance"></a>SQL Server e Instância Gerenciada de SQL

[!INCLUDE [CREATE WORKLOAD GROUP](../../includes/create-workload-group.md)]

::: moniker-end
::: moniker range="=azure-sqldw-latest"

:::row:::
    :::column:::
        [SQL Server](create-workload-group-transact-sql.md?view=sql-server-ver15&preserve-view=true)
    :::column-end:::
    :::column:::
        [Instância Gerenciada de SQL](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        **_\* Azure Synapse<br />Analytics \*_** &nbsp;
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="azure-synapse-analytics"></a>Azure Synapse Analytics

Cria um grupo de carga de trabalho. Grupos de carga de trabalho são contêineres para um conjunto de solicitações e são a base de como o gerenciamento de cargas de trabalho é configurado em um sistema. Os grupos de cargas de trabalho fornecem a capacidade de reservar recursos para ter isolamento da cargas de trabalho, conter recursos, definir recursos por solicitação e aderir às regras de execução. Quando a instrução for concluída, as configurações estarão em vigor.

:::image type="icon" source="../../database-engine/configure-windows/media/topic-link.gif"::: [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

```syntaxsql
CREATE WORKLOAD GROUP group_name
 WITH
 (   MIN_PERCENTAGE_RESOURCE = value 
   , CAP_PERCENTAGE_RESOURCE = value 
   , REQUEST_MIN_RESOURCE_GRANT_PERCENT = value
  [ [ , ] REQUEST_MAX_RESOURCE_GRANT_PERCENT = value ]
  [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH } ]
  [ [ , ] QUERY_EXECUTION_TIMEOUT_SEC = value ] )
  [ ; ]

```

*group_name*</br>
Especifica o nome pelo qual o grupo de carga de trabalho é identificado. *group_name* é um sysname. Ele pode ter até 128 caracteres e deve ser exclusivo dentro da instância.

*MIN_PERCENTAGE_RESOURCE* = value</br>
Especifica uma alocação de recurso mínima garantida para este grupo de carga de trabalho, que não é compartilhada com outros grupos de carga de trabalho. *value* é um intervalo de inteiros de 0 a 100. A soma de min_percentage_resource em todos os grupos de carga de trabalho não pode exceder 100. O valor de min_percentage_resource não pode ser maior que cap_percentage_resource. Há valores mínimos efetivos permitidos por nível de serviço. Confira [Valores Efetivos](#effective-values) para obter mais detalhes.

*CAP_PERCENTAGE_RESOURCE* = value</br>
Especifica a utilização de recursos máxima para todas as solicitações em um grupo de carga de trabalho. O intervalo de inteiros permitido para o valor é de 1 a 100. O valor de cap_percentage_resource precisa ser maior que min_percentage_resource. O valor efetivo para cap_percentage_resource pode ser reduzido se min_percentage_resource estiver configurado como maior que zero em outros grupos de carga de trabalho.

*REQUEST_MIN_RESOURCE_GRANT_PERCENT* = value</br>
Define a quantidade mínima de recursos alocados por solicitação. *value* é um parâmetro obrigatório com um intervalo decimal entre 0,75 e 100,00. O valor de request_min_resource_grant_percent deve ser múltiplo de 0,25, deve ser um fator de min_percentage_resource e ser menor que cap_percentage_resource. Há valores mínimos efetivos permitidos por nível de serviço. Confira [Valores Efetivos](#effective-values) para obter mais detalhes.

Por exemplo:

```sql
CREATE WORKLOAD GROUP wgSample 
WITH
  ( MIN_PERCENTAGE_RESOURCE = 26                -- integer value
    , REQUEST_MIN_RESOURCE_GRANT_PERCENT = 3.25 -- factor of 26 (guaranteed a minimum of 8 concurrency)
    , CAP_PERCENTAGE_RESOURCE = 100 )
```

considere os valores que são usados para as classes de recurso como uma diretriz para request_min_resource_grant_percent.  A tabela a seguir contém alocações de recursos para Gen2.

|Classe de recurso|Porcentagem de recursos|
|---|---|
|Smallrc|3%|
|Mediumrc|10%|
|Largerc|22%|
|Xlargerc|70%|
|||

*REQUEST_MAX_RESOURCE_GRANT_PERCENT* = value</br>         
Define a quantidade máxima de recursos alocados por solicitação. *value* é um parâmetro decimal opcional com um valor padrão igual ao request_min_resource_grant_percent. *value* deve ser maior ou igual a request_min_resource_grant_percent. Quando o valor de request_max_resource_grant_percent é maior que request_min_resource_grant_percent e os recursos do sistema estão disponíveis, recursos adicionais são alocados a uma solicitação.

*IMPORTANCE* = { LOW \| BELOW_NORMAL \| NORMAL \| ABOVE_NORMAL \| HIGH }</br>        
Especifica a importância padrão de uma solicitação no grupo de carga de trabalho. A importância é uma das seguintes, com NORMAL sendo o padrão:

- LOW
- BELOW_NORMAL
- NORMAL (padrão)
- ABOVE_NORMAL
- HIGH

A importância definida no grupo de carga de trabalho é uma importância padrão para todas as solicitações no grupo de carga de trabalho. Um usuário também pode definir a importância no nível do classificador, que pode substituir a configuração de importância do grupo de carga de trabalho. Isso permite diferenciar a importância das solicitações em um grupo de carga de trabalho para ter acesso a recursos não reservados mais rapidamente. Quando a soma de min_percentage_resource entre grupos de carga de trabalho é menor que 100, há recursos não reservados que são atribuídos em uma base de importância.

*QUERY_EXECUTION_TIMEOUT_SEC* = value</br>     
Especifica o tempo máximo, em segundos, que uma consulta pode ser executada antes de ser cancelada. *value* precisa ser 0 ou um inteiro positivo. A configuração padrão para o valor é 0, em que a consulta nunca expira. QUERY_EXECUTION_TIMEOUT_SEC conta depois que a consulta está em estado de execução, não quando a consulta é enfileirada.

## <a name="remarks"></a>Comentários

Os grupos de carga de trabalho correspondentes às classes de recursos são criados automaticamente para ter compatibilidade com versões anteriores. Esses grupos de carga de trabalho definidos pelo sistema não podem ser descartados. Oito grupos de carga de trabalho adicionais definidos pelo usuário podem ser criados.

Se um grupo de cargas de trabalho for criado com `min_percentage_resource` maior que zero, a instrução `CREATE WORKLOAD GROUP` entrará na fila até que haja recursos suficientes para criar o grupo de carga de trabalho.

## <a name="effective-values"></a>Valores efetivos

Os parâmetros `min_percentage_resource`, `cap_percentage_resource`, `request_min_resource_grant_percent` e `request_max_resource_grant_percent` têm valores efetivos que são ajustados no contexto do nível de serviço atual e da configuração de outros grupos de carga de trabalho.

O parâmetro `request_min_resource_grant_percent` tem um valor efetivo porque há recursos mínimos necessários por consulta, dependendo do nível de serviço.  Por exemplo, no nível de serviço mais baixo, DW100c, são necessários pelo menos 25% dos recursos por solicitação.  Se o grupo de carga de trabalho estiver configurado com 3% em `request_min_resource_grant_percent` e `request_max_resource_grant_percent`, os valores efetivos para ambos os parâmetros serão ajustados para 25% quando a instância for iniciada.  Se a instância for expandida para DW1000c, os valores configurados e efetivos para ambos os parâmetros serão de 3%, porque esse é o valor mínimo com suporte no nível de serviço.  Se a instância for expandida para um valor maior que DW1000c, os valores configurados e efetivos para ambos os parâmetros permanecerão em 3%.  Confira a tabela abaixo para obter mais detalhes sobre os valores efetivos nos diferentes níveis de serviço.

|Nível de serviço|Valor mais baixo efetivo para REQUEST_MIN_RESOURCE_GRANT_PERCENT|Máximo de consultas simultâneas|
|---|---|---|
|DW100c|25%|4|
|DW200c|12,5%|8|
|DW300c|8%|12|
|DW400c|6,25%|16|
|DW500c|5%|20|
|DW1000c|3%|32|
|DW1500c|3%|32|
|DW2000c|2%|48|
|DW2500c|2%|48|
|DW3000c|1,5%|64|
|DW5000c|1,5%|64|
|DW6000c|0,75%|128|
|DW7500c|0,75%|128|
|DW10000c|0,75%|128|
|DW15000c|0,75%|128|
|DW30000c|0,75%|128|
||||

O parâmetro `min_percentage_resource` deve ser maior ou igual ao `request_min_resource_grant_percent` efetivo. Um grupo de carga de trabalho com um `min_percentage_resource` configurado menor do que o `min_percentage_resource` efetivo tem o valor ajustado para zero em runtime. Quando isso acontece, os recursos configurados para `min_percentage_resource` podem ser compartilhados entre todos os grupos de carga de trabalho. Por exemplo, o grupo de carga de trabalho `wgAdHoc` com um `min_percentage_resource` de 10% em execução em DW1000c teria um `min_percentage_resource` efetivo de 10% (3% é o valor mínimo com suporte em DW1000c). `wgAdhoc` em DW100c teria um min_percentage_resource efetivo de 0%. Os 10% configurados para `wgAdhoc` seriam compartilhados entre todos os grupos de carga de trabalho.

O parâmetro `cap_percentage_resource` também tem um valor efetivo. Se um grupo de carga de trabalho `wgAdhoc` estiver configurado com um `cap_percentage_resource` de 100% e outro grupo de carga de trabalho `wgDashboards` for criado com 25% `min_percentage_resource`, o `cap_percentage_resource` efetivo para `wgAdhoc` se tornará 75%.

A maneira mais fácil de entender os valores de tempo de execução para seus grupos de carga de trabalho é consultar o modo de exibição do sistema [sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md).

## <a name="permissions"></a>Permissões

Requer a permissão `CONTROL DATABASE`

## <a name="see-also"></a>Confira também

- [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](drop-workload-group-transact-sql.md)
- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](alter-workload-group-transact-sql.md)
- [sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md)
- [sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md)
- [Início Rápido: Configurar isolamento da carga de trabalho com o T-SQL](/azure/sql-data-warehouse/quickstart-configure-workload-isolation-tsql)

::: moniker-end
