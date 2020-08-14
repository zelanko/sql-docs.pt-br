---
title: ALTER WORKLOAD GROUP (Transact-SQL)
ms.custom: ''
ms.date: 05/05/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_WORKLOAD_GROUP_TSQL
- ALTER WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER WORKLOAD GROUP statement
ms.assetid: 957addce-feb0-4e54-893e-5faca3cd184c
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: 3909a970b37b23a1767d45bdae14e29441822acb
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864457"
---
# <a name="alter-workload-group-transact-sql"></a>ALTER WORKLOAD GROUP (Transact-SQL)

[!INCLUDE[select-product](../../includes/select-product.md)]

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

:::row:::
    :::column:::
        **_\* SQL Server \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Banco de Dados SQL<br />Instância Gerenciada](alter-workload-group-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-workload-group-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-server-and-sql-managed-instance"></a>SQL Server e Instância Gerenciada de SQL

[!INCLUDE [ALTER WORKLOAD GROUP](../../includes/alter-workload-group.md)]
  
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-workload-group-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        **_\* Instância Gerenciada do<br />Banco de Dados SQL \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-workload-group-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-server-and-sql-managed-instance"></a>SQL Server e Instância Gerenciada de SQL

[!INCLUDE [ALTER WORKLOAD GROUP](../../includes/alter-workload-group.md)]

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-workload-group-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        [Banco de Dados SQL<br />Instância Gerenciada](alter-workload-group-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        **_\* Azure Synapse<br />Analytics \*_** &nbsp;
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="azure-synapse-analytics"></a>Azure Synapse Analytics

Altera um grupo de carga de trabalho existente.

Consulte a seção comportamento de `ALTER WORKLOAD GROUP` abaixo para obter mais detalhes sobre como o `ALTER WORKLOAD GROUP` se comporta em um sistema com solicitações em execução e em fila. 

As restrições em vigor para [CREATE WORKLOAD GROUP](create-workload-group-transact-sql.md) também se aplicam a `ALTER WORKLOAD GROUP`.  Antes de modificar parâmetros, consulte [sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md) para garantir que os valores estejam dentro de intervalos aceitáveis.

## <a name="syntax"></a>Sintaxe

```syntaxsql
ALTER WORKLOAD GROUP group_name
 WITH
 ([       MIN_PERCENTAGE_RESOURCE = value ]
  [ [ , ] CAP_PERCENTAGE_RESOURCE = value ]
  [ [ , ] REQUEST_MIN_RESOURCE_GRANT_PERCENT = value ]
  [ [ , ] REQUEST_MAX_RESOURCE_GRANT_PERCENT = value ] 
  [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }]
  [ [ , ] QUERY_EXECUTION_TIMEOUT_SEC = value ] )
  [ ; ]
  ```

## <a name="arguments"></a>Argumentos

group_name  
É o nome de um grupo de carga de trabalho definido pelo usuário existente que está sendo alterado.  O group_name não é alterável. 

MIN_PERCENTAGE_RESOURCE = value  
O valor é um intervalo de inteiros de 0 a 100.  Ao alterar min_percentage_resource, a soma de min_percentage_resource em todos os grupos de carga de trabalho não pode exceder 100.  A alteração de min_percentage_resource exige que todas as consultas em execução sejam concluídas no grupo de carga de trabalho antes que o comando seja concluído.  Consulte a seção Comportamento do ALTER WORKLOAD GROUP neste documento para obter mais detalhes.

CAP_PERCENTAGE_RESOURCE = value  
O valor é um intervalo de inteiros de 1 a 100.  O valor de cap_percentage_resource precisa ser maior que min_percentage_resource.  A alteração de cap_percentage_resource exige que todas as consultas em execução sejam concluídas no grupo de carga de trabalho antes que o comando seja concluído.  Consulte a seção Comportamento do ALTER WORKLOAD GROUP neste documento para obter mais detalhes. 

REQUEST_MIN_RESOURCE_GRANT_PERCENT = value  
O valor é um decimal com um intervalo entre 0,75 e 100,00.  O valor de request_min_resource_grant_percent precisa ser um fator de min_percentage_resource e ser menor que cap_percentage_resource. 
  
REQUEST_MAX_RESOURCE_GRANT_PERCENT = value  
O valor é um decimal e precisa ser maior ou igual a request_min_resource_grant_percent.

IMPORTANCE = { LOW \|  BELOW_NORMAL \| NORMAL \| ABOVE_NORMAL \| HIGH }  
Altera a importância padrão de uma solicitação no grupo de carga de trabalho.

QUERY_EXECUTION_TIMEOUT_SEC = value  
Altera o tempo máximo, em segundos, que uma consulta pode ser executada antes de ser cancelada. O valor precisa ser zero ou um inteiro positivo. A configuração padrão de value é 0, o que significa ilimitado.   

## <a name="permissions"></a>Permissões

Requer a permissão CONTROL DATABASE

## <a name="example"></a>Exemplo

O exemplo abaixo verifica os valores na exibição de catálogo para wgDataLoads e altera os valores.

```sql
SELECT *
FROM sys.workload_management_workload_groups  
WHERE [name] = 'wgDataLoads'

ALTER WORKLOAD GROUP wgDataLoads WITH
( MIN_PERCENTAGE_RESOURCE            = 40
 ,CAP_PERCENTAGE_RESOURCE            = 80
 ,REQUEST_MIN_RESOURCE_GRANT_PERCENT = 10 )
 ```

## <a name="alter-workload-group-behavior"></a>Comportamento do ALTER WORKLOAD GROUP

A qualquer momento, há três tipos de solicitações no sistema
- Solicitações que ainda não foram classificadas.
- Solicitações que estão classificadas e estão aguardando bloqueios de objeto ou recursos do sistema.
- Solicitações que estão classificadas e em execução.

Com base nas propriedades de um grupo de carga de trabalho que está sendo alterado, o tempo em que as configurações entram em vigor será diferente.

**Importance ou query_execution_timeout** Para as propriedades importance e query_execution_timeout, as solicitações não classificadas escolhem os novos valores de configuração.  As solicitações em espera e em execução são executadas com a configuração antiga.  A solicitação `ALTER WORKLOAD GROUP` é executada imediatamente, independentemente de estar executando consultas no grupo de carga de trabalho.

**Request_min_resource_grant_percent ou request_max_resource_grant_percent** Para request_min_resource_grant_percent e request_max_resource_grant_percent, as solicitações em execução são executadas com a configuração antiga.  As solicitações em espera e as solicitações não classificadas escolhem os novos valores de configuração.  A solicitação `ALTER WORKLOAD GROUP` é executada imediatamente, independentemente de estar executando consultas no grupo de carga de trabalho.

**Min_percentage_resource ou cap_percentage_resource** Para min_percentage_resource e cap_percentage_resource, as solicitações em execução são executadas com a configuração antiga.  As solicitações em espera e as solicitações não classificadas escolhem os novos valores de configuração. 

Alterar min_percentage_resource e cap_percentage_resource requer o esvaziamento de solicitações em execução no grupo de carga de trabalho que está sendo alterado.  Ao diminuir min_percentage_resource, os recursos liberados são retornados para o pool de compartilhamento, permitindo que as solicitações de outros grupos de carga de trabalho possam ser utilizadas.  Por outro lado, aumentar o min_percentage_resource aguardará até que as solicitações que utilizam apenas os recursos necessários do pool compartilhado sejam concluídas.  A operação Alter workload group terá prioridade de acesso a recursos compartilhados em relação a outras solicitações aguardando execução no pool compartilhado.  Se a soma de min_percentage_resource exceder 100%, a solicitação ALTER WORKLOAD GROUP falhará imediatamente. 

**Comportamento de bloqueio** Alterar um grupo de carga de trabalho requer um bloqueio global em todos os grupos de carga de trabalho.  Uma solicitação para alterar um grupo de carga de trabalho ficaria atrás na fila das solicitações de grupo de carga de trabalho de criação ou de remoção já enviadas.  Se um lote de instruções de alteração for enviado de uma vez, elas serão processadas na ordem em que forem enviadas.  

## <a name="see-also"></a>Confira também

- [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](create-workload-group-transact-sql.md)
- [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](drop-workload-group-transact-sql.md)
- [sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md)
- [sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md)
- [Início Rápido: Configurar isolamento da carga de trabalho com o T-SQL](/azure/sql-data-warehouse/quickstart-configure-workload-isolation-tsql)

::: moniker-end
