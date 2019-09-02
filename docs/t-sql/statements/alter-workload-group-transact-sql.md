---
title: ALTER WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2019
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
ms.openlocfilehash: 47b924754f221b93e8f9e661a1b12afb5f07fcd4
ms.sourcegitcommit: 8c1c6232a4f592f6bf81910a49375f7488f069c4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/26/2019
ms.locfileid: "70026227"
---
# <a name="alter-workload-group-transact-sql"></a>ALTER WORKLOAD GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera uma configuração existente de grupo de cargas de trabalho do Resource Governor e a atribui opcionalmente a um pool de recursos do Resource Governor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ALTER WORKLOAD GROUP { group_name | "default" }  
[ WITH  
    ([ IMPORTANCE = { LOW | MEDIUM | HIGH } ]  
      [ [ , ] REQUEST_MAX_MEMORY_GRANT_PERCENT = value ]  
      [ [ , ] REQUEST_MAX_CPU_TIME_SEC = value ]  
      [ [ , ] REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value ]   
      [ [ , ] MAX_DOP = value ]  
      [ [ , ] GROUP_MAX_REQUESTS = value ] )  
 ]  
[ USING { pool_name | "default" } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *group_name* | "**default**"       
 É o nome de um grupo de cargas de trabalho existente, definido pelo usuário, ou o grupo de cargas de trabalho padrão do Administrador de Recursos.  
  
> [!NOTE]  
> O Administrador de Recursos cria os grupos internos e padrão quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é instalado.  
  
 A opção "default" deve estar entre aspas ("") ou colchetes ([]) quando usado com ALTER WORKLOAD GROUP para evitar conflito com DEFAULT, que é uma palavra reservada do sistema. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
> [!NOTE]  
> Os grupos de carga de trabalho predefinidos e os pools de recursos usam nomes de letras minúsculas, como "padrão". Isso deve ser levado em consideração nos servidores que usam ordenação com diferenciação de maiúsculas e minúsculas. Os servidores com ordenação sem diferenciação de maiúsculas e minúsculas, como SQL_Latin1_General_CP1_CI_AS, tratarão "default" e "Default" da mesma maneira.  
  
 IMPORTANCE = { LOW | **MEDIUM** | HIGH }       
 Especifica a importância relativa de uma solicitação no grupo de carga de trabalho. A importância é uma das seguintes:  
  
-   LOW  
-   MEDIUM (padrão)  
-   HIGH  
  
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
  
 REQUEST_MEMORY_GRANT_TIMEOUT_SEC =*value*  
 Especifica o tempo máximo, em segundos, que uma consulta pode aguardar pela concessão de memória (memória do buffer de trabalho).  
  
> [!NOTE]  
> Nem sempre uma consulta falha quando o tempo limite de concessão de memória é atingido. A consulta falhará somente se houver muitas consultas simultâneas em execução. Caso contrário, a consulta poderá obter apenas a concessão de memória mínima, resultando em uma queda no desempenho de consulta.  
  
 *value* deve ser um inteiro positivo. A configuração padrão de *value*, 0, usa um cálculo interno baseado no custo da consulta para determinar o tempo máximo.  
  
 MAX_DOP =*value*       
 Especifica o DOP (grau máximo de paralelismo) para solicitações paralelas. *value* deve ser 0 ou um inteiro positivo, de 1 a 255. Quando *value* for 0, o servidor escolherá o grau máximo de paralelismo. Essa é a configuração padrão e recomendada.  
  
> [!NOTE]  
> O valor real que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] define para MAX_DOP poderia ser menos que o valor especificado. O valor final é determinado pela fórmula min(255, *número de CPUs)* .  
  
> [!CAUTION]  
> Alterar MAX_DOP pode comprometer o desempenho de um servidor. Se você precisar alterar MAX_DOP, nós recomendaremos que seja definido um valor menor que ou igual ao número máximo de agendadores de hardware que existem em um único nó NUMA. Nós recomendamos que você não defina MAX_DOP como um valor maior que 8.  
  
 MAX_DOP é tratado como segue:  
  
-   MAX_DOP como dica de consulta será cumprido, contanto que não exceda o grupo de cargas de trabalho MAX_DOP.  
  
-   MAX_DOP como uma dica de consulta sempre substitui o 'grau máximo de paralelismo' sp_configure.  
  
-   O grupo de carga de trabalho MAX_DOP substitui o 'grau máximo de paralelismo' sp_configure.  
  
-   Se a consulta for marcada como serial (MAX_DOP = 1) em tempo de compilação, não poderá ser revertida para paralela em tempo de execução, independentemente do grupo de cargas de trabalho ou da configuração sp_configure.  
  
 Depois de ser configurado, o DOP só pode ser reduzido sob pressão de concessão de memória. A reconfiguração do grupo de carga de trabalho não é visível durante a espera na fila de concessão de memória.  
  
 GROUP_MAX_REQUESTS = *value*      
 Especifica o número máximo de solicitações simultâneas permitido para execução no grupo de carga de trabalho. *value* precisa ser 0 ou um inteiro positivo. A configuração padrão de *value*, 0, permite solicitações ilimitadas. Quando as solicitações simultâneas máximas são alcançadas, um usuário nesse grupo pode fazer logon, mas é colocado em um estado de espera até que as solicitações simultâneas sejam ignoradas abaixo do valor especificado.  
  
 USING { *pool_name* | "**default**" }      
 Associa o grupo de cargas de trabalho ao pool de recursos definido pelo usuário, identificado por *pool_name*, o que, na realidade, coloca o grupo de cargas de trabalho no pool de recursos. Se *pool_name* não for fornecido ou se o argumento USING não for usado, o grupo de carga de trabalho será colocado no pool padrão predefinido do Resource Governor.  
  
 A opção "default" deve estar entre aspas ("") ou colchetes ([]) quando usado com ALTER WORKLOAD GROUP para evitar conflito com DEFAULT, que é uma palavra reservada do sistema. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
> [!NOTE]  
> A opção "default" diferencia maiúsculas de minúsculas.  
  
## <a name="remarks"></a>Remarks  
 ALTER WORKLOAD GROUP é permitido no grupo padrão.  
  
 As alterações na configuração do grupo de cargas de trabalho não entrarão em vigor enquanto ALTER RESOURCE GOVERNOR RECONFIGURE não for executado. Ao alterar um plano que afeta a configuração, a nova configuração apenas terá efeito nos planos anteriormente armazenados em cache após a execução de DBCC FREEPROCCACHE (*pool_name*), em que *pool_name* é o nome de um pool de recursos do Resource Governor ao qual o grupo de carga de trabalho está associado.  
  
-   Se você estiver alterando MAX_DOP para 1, a execução de DBCC FREEPROCCACHE não será necessária, porque os planos paralelos podem ser executados em modo serial. No entanto, isso pode não ser tão eficiente quanto um plano compilado como um plano serial.  
  
-   Se você estiver alterando MAX_DOP de 1 para 0 ou para um valor maior que 1, a execução de DBCC FREEPROCCACHE não será necessária. No entanto, os planos seriais não podem ser executados em paralelo, portanto, limpar o respectivo cache permitirá que novos planos sejam possivelmente compilados usando paralelismo.  
  
> [!CAUTION]  
> A limpeza de planos armazenados em cache de um pool de recursos que está associado a mais de um grupo de carga de trabalho afetará todos os grupos de cargas de trabalho com o pool de recursos definido pelo usuário identificado por *pool_name*.  
  
 Ao executar instruções DDL, é recomendável estar familiarizado com os estados do Resource Governor. Para obter mais informações, consulte [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).  
  
 REQUEST_MEMORY_GRANT_PERCENT: Em [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], a criação de índice tem permissão para usar mais memória do workspace do que a concedida inicialmente para melhorar o desempenho. Esse tratamento especial tem suporte do Administrador de Recursos em versões posteriores. No entanto, a concessão inicial e qualquer concessão de memória adicional estão limitadas pelas configurações de pool de recursos e de grupo de cargas de trabalho.  
  
 **Criação de índice em uma tabela particionada**  
  
 A memória consumida pela criação de índice na tabela particionada não alinhada é proporcional ao número de partições envolvidas.  Se a memória total necessária exceder o limite por consulta (REQUEST_MAX_MEMORY_GRANT_PERCENT) imposto pela configuração de grupo de cargas de trabalho do Administrador de Recursos, poderá ocorrer uma falha na criação do índice. Como o grupo de carga de trabalho "padrão" permite que uma consulta exceda o limite por consulta com o mínimo de memória requerida para iniciar, para compatibilidade com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o usuário talvez possa executar a mesma criação de índice no grupo de carga de trabalho "padrão" caso o pool de recursos "padrão" tenha memória total suficiente configurada para executar tal consulta.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `CONTROL SERVER`.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como alterar a importância de solicitações no grupo padrão de `MEDIUM` para `LOW`.  
  
```sql  
ALTER WORKLOAD GROUP "default"  
WITH (IMPORTANCE = LOW);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
 O exemplo a seguir mostra como mover um grupo de cargas de trabalho do pool em que ele se encontra para o pool padrão.  
  
```sql  
ALTER WORKLOAD GROUP adHoc  
USING [default];  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
