---
title: CREATE WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2019
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
ms.assetid: d949e540-9517-4bca-8117-ad8358848baa
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e78ab71081c991b5e42726ed4dd594e016f324f0
ms.sourcegitcommit: aece9f7db367098fcc0c508209ba243e05547fe1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2019
ms.locfileid: "72260324"
---
# <a name="create-workload-group-transact-sql"></a>CREATE WORKLOAD GROUP (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Cria um grupo de carga de trabalho do Administrador de recursos e o associa a um pool de recursos do Administrador de recursos. O Resource Governor não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintaxe

```
CREATE WORKLOAD GROUP group_name
[ WITH
    ( [ IMPORTANCE = { LOW | MEDIUM | HIGH } ]
      [ [ , ] REQUEST_MAX_MEMORY_GRANT_PERCENT = value ]
      [ [ , ] REQUEST_MAX_CPU_TIME_SEC = value ]
      [ [ , ] REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value ]
      [ [ , ] MAX_DOP = value ]
      [ [ , ] GROUP_MAX_REQUESTS = value ] )
 ]
[ USING {
    [ pool_name | "default" ]
    [ [ , ] EXTERNAL external_pool_name | "default" ] ]
    } ]
[ ; ]
```

## <a name="arguments"></a>Argumentos

*group_name*     
É o nome definido pelo usuário do grupo de carga de trabalho. *group_name* é alfanumérico, pode ter até 128 caracteres, precisa ser exclusivo em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e precisa estar em conformidade com as regras para [identificadores](../../relational-databases/databases/database-identifiers.md).

IMPORTANCE = { LOW | **MEDIUM** | HIGH }     
Especifica a importância relativa de uma solicitação no grupo de carga de trabalho. A importância é uma das seguintes, com MEDIUM sendo o padrão:

- LOW
- MEDIUM (padrão)
- HIGH

> [!NOTE]
> Internamente, cada configuração de importância é armazenada como um número usado para cálculos.

IMPORTANCE é local para o pool de recursos; grupos de cargas de trabalho de importâncias diferentes no mesmo pool de recursos afetam uns aos outros, mas não afetam grupos de cargas de trabalho em outro pool de recursos.

REQUEST_MAX_MEMORY_GRANT_PERCENT = *value*     
Especifica o máximo de memória que uma única solicitação pode usar do pool. *valor* é um percentual relativo ao tamanho do pool de recursos especificado por MAX_MEMORY_PERCENT. 

*value* é um inteiro até [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e um flutuante que começa com [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]. O valor padrão é 25. O intervalo permitido para *value* é de 1 a 100.

> [!NOTE]  
> A quantidade especificada se refere apenas à memória de concessão de execução da consulta.  
  
> [!IMPORTANT]
> A configuração de *value* como 0 impede a execução de consultas com as operações SORT e HASH JOIN em grupos de cargas de trabalho definidos pelo usuário.     
>
> Não é recomendável definir *value* com um valor maior que 70, pois o servidor poderá não conseguir separar memória livre suficiente se outras consultas simultâneas estiverem sendo executadas. Isso pode eventualmente levar ao erro 8645, tempo limite da consulta excedido.      
  
> [!NOTE]  
> Se os requisitos de memória de consulta excederem o limite especificado por esse parâmetro, o servidor fará o seguinte:  
>   
> -  Para grupos de cargas de trabalho definidos pelo usuário, o servidor tenta reduzir o grau de paralelismo da consulta, até que o requisito de memória caia abaixo do limite, ou até que o grau de paralelismo seja igual a 1. Se o requisito de memória de consulta ainda for maior que o limite, ocorrerá o erro 8657.  
>   
> -  Para grupos de cargas de trabalho internos e padrão, o servidor permite que a consulta obtenha a memória necessária.  
>   
> Esteja ciente de que ambos os casos estarão sujeitos ao erro de tempo limite 8645 se a memória física do servidor for insuficiente.  

REQUEST_MAX_CPU_TIME_SEC = *value*     
Especifica o tempo máximo de CPU, em segundos, que uma solicitação pode usar. *value* precisa ser 0 ou um inteiro positivo. A configuração padrão de *value* é 0, o que significa ilimitado.

> [!NOTE]
> Por padrão, o Resource Governor não impedirá a continuação de uma solicitação se o tempo máximo for excedido. Porém, um evento será gerado. Para obter mais informações, consulte [Classe de evento CPU Threshold Exceeded](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md).     

> [!IMPORTANT]
> Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 e usando o [sinalizador de rastreamento 2422](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md), o Resource Governor anulará uma solicitação quando o tempo máximo for excedido.

REQUEST_MEMORY_GRANT_TIMEOUT_SEC = *value*     
Especifica o tempo máximo, em segundos, que uma consulta pode esperar pela disponibilização de uma concessão de memória (memória do buffer do trabalho). *value* precisa ser 0 ou um inteiro positivo. A configuração padrão de *value*, 0, usa um cálculo interno baseado no custo da consulta para determinar o tempo máximo.

> [!NOTE]
> Nem sempre uma consulta falha quando o tempo limite de concessão de memória é atingido. A consulta falhará somente se houver muitas consultas simultâneas em execução. Caso contrário, a consulta poderá obter apenas a concessão de memória mínima, resultando em uma queda no desempenho de consulta.

MAX_DOP = *value*     
Especifica o **grau máximo de paralelismo (MAXDOP)** para execução de consulta paralela. *value* precisa ser 0 ou um inteiro positivo. O intervalo permitido para *value* é de 0 a 64. A configuração padrão para *value*, 0, usa a configuração global. MAX_DOP é tratado como segue:

> [!NOTE]
> O grupo de cargas de trabalho do MAX_DOP substitui a [configuração de servidor para o grau máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) e a [configuração no escopo do banco de dados](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) do **MAXDOP**.

> [!TIP]
> Para fazer isso no nível da consulta, use a [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md) do **MAXDOP**. Definir o grau máximo de paralelismo como uma dica de consulta funciona, desde que não exceda o grupo de carga de trabalho do MAX_DOP. Se o valor de dica de consulta do MAXDOP ultrapassar o valor configurado no Resource Governor, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usará o valor `MAX_DOP` do Resource Governor. A [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md) do MAXDOP sempre substitui a [configuração de servidor para o grau máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).      
>   
> Para fazer isso no nível do banco de dados, use a [configuração com escopo no banco de dados](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) do **MAXDOP**.      
>   
> Para fazer isso no nível do servidor, use o **MAXDOP (grau máximo de paralelismo)** na [opção de configuração do servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).     

GROUP_MAX_REQUESTS = *value*     
Especifica o número máximo de solicitações simultâneas permitido para execução no grupo de carga de trabalho. *value* precisa ser 0 ou um inteiro positivo. A configuração padrão de *valor* é 0 e permite solicitações ilimitadas. Quando as solicitações simultâneas máximas são alcançadas, um usuário nesse grupo pode fazer logon, mas é colocado em um estado de espera até que as solicitações simultâneas sejam ignoradas abaixo do valor especificado.

USING { *pool_name* |  **"default"** }     
Associa o grupo de carga de trabalho ao pool de recursos definido pelo usuário, identificado por *pool_name*. Na realidade, isso coloca o grupo de carga de trabalho no pool de recursos. Se *pool_name* não for fornecido ou se o argumento USING não for usado, o grupo de carga de trabalho será colocado no pool padrão predefinido do Resource Governor.

"default" é uma palavra reservada e, quando usada com USING, deve ficar entre aspas ("") ou colchetes ([]).

> [!NOTE]
> Grupos de cargas de trabalho e pools de recursos predefinidos usam nomes em letras minúsculas, como "default". Isso deve ser levado em consideração nos servidores que usam ordenação com diferenciação de maiúsculas e minúsculas. Os servidores com ordenação sem diferenciação de maiúsculas e minúsculas, como SQL_Latin1_General_CP1_CI_AS, tratarão "default" e "Default" da mesma maneira.

EXTERNAL external_pool_name | "padrão"     
**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).

O grupo de carga de trabalho pode especificar um pool de recursos externo. Você pode definir um grupo de carga de trabalho e associá-lo a dois pools:

- Um pool de recursos para cargas de trabalho e consultas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
- Um pool de recursos externo para processos externos. Para obter mais informações, confira [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

## <a name="remarks"></a>Remarks
Quando `REQUEST_MEMORY_GRANT_PERCENT` é usado, a criação de índice tem permissão para usar mais memória do workspace do que a concedida inicialmente, para melhorar o desempenho. Esse tratamento especial tem o suporte do Administrador de Recursos no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Porém, a concessão inicial e qualquer concessão de memória adicional estão limitadas pelas configurações de pool de recursos e de grupo de carga de trabalho.

O limite de `MAX_DOP` é definido por [tarefa](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md). Não é um limite por [solicitação](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) ou por consulta. Isso significa que, durante uma execução de consulta paralela, uma solicitação única pode gerar várias tarefas que são atribuídas a um [agendador](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md). Para saber mais, confira o [Guia de arquitetura de threads e tarefas](../../relational-databases/thread-and-task-architecture-guide.md).

Quando `MAX_DOP` for usado e uma consulta for marcada como serial em tempo de compilação, ela não poderá ser revertida a paralela em tempo de execução, independentemente do grupo de carga de trabalho ou da definição de configuração do servidor. Depois de configurar o `MAX_DOP`, ele só poderá ser reduzido devido à pressão de memória. A reconfiguração do grupo de carga de trabalho não é visível durante a espera na fila de concessão de memória.

### <a name="index-creation-on-a-partitioned-table"></a>Criação de índice em uma tabela particionada

A memória consumida pela criação de índice na tabela particionada não alinhada é proporcional ao número de partições envolvidas. Se a memória total necessária exceder o limite por consulta `REQUEST_MAX_MEMORY_GRANT_PERCENT` imposto pela configuração de grupo de cargas de trabalho do Resource Governor, poderá ocorrer uma falha na criação do índice. Como o grupo de carga de trabalho *"padrão"* permite que uma consulta exceda o limite por consulta com o mínimo de memória necessária, o usuário talvez possa executar a mesma criação de índice no grupo de carga de trabalho *"padrão"* caso o pool de recursos *"padrão"* tenha memória total suficiente configurada para executar tal consulta.

## <a name="permissions"></a>Permissões
Requer a permissão `CONTROL SERVER`.

## <a name="example"></a>Exemplo

Crie um grupo de carga de trabalho chamado `newReports`, que usa as configurações padrão do Resource Governor e está no pool padrão desse Resource Governor. O exemplo especifica o pool `default`, mas isso não é necessário.

```sql
CREATE WORKLOAD GROUP newReports
    USING "default" ;
GO
```

## <a name="see-also"></a>Consulte Também

- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)
- [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)
- [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)
