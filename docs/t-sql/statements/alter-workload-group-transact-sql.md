---
title: ALTER WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/04/2018
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_WORKLOAD_GROUP_TSQL
- ALTER WORKLOAD GROUP
dev_langs: TSQL
helpviewer_keywords: ALTER WORKLOAD GROUP statement
ms.assetid: 957addce-feb0-4e54-893e-5faca3cd184c
caps.latest.revision: "56"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d48a892ef00610cc0d69ff8d2a36e0fce4be7704
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="alter-workload-group-transact-sql"></a>ALTER WORKLOAD GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera uma configuração de grupo de carga de trabalho de administrador de recursos existente e, opcionalmente, atribui a um a um pool de recursos do administrador de recursos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
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
> Grupos de cargas de trabalho predefinidos e pools de recursos usam nomes de letras minúsculas, como "padrão". Isso deve ser levado em consideração nos servidores que usam agrupamento com diferenciação de maiúsculas e minúsculas. Os servidores com agrupamento sem diferenciação de maiúsculas e minúsculas, como SQL_Latin1_General_CP1_CI_AS, tratarão "default" e "Default" da mesma maneira.  
  
 IMPORTANCE = { LOW | MEDIUM | HIGH }  
 Especifica a importância relativa de uma solicitação no grupo de carga de trabalho. A importância é uma das seguintes:  
  
-   LOW  
-   MEDIUM (padrão)  
-   HIGH  
  
> [!NOTE]  
> Internamente, cada configuração de importância é armazenada como um número usado para cálculos.  
  
 IMPORTANCE é local para o pool de recursos; grupos de cargas de trabalho de importâncias diferentes no mesmo pool de recursos afetam uns aos outros, mas não afetam grupos de cargas de trabalho em outro pool de recursos.  
  
 REQUEST_MAX_MEMORY_GRANT_PERCENT =*value*  
 Especifica o máximo de memória que uma única solicitação pode usar do pool. Essa porcentagem é relativa ao tamanho do pool de recursos especificado por MAX_MEMORY_PERCENT.  
  
> [!NOTE]  
> A quantidade especificada se refere apenas à memória de concessão de execução da consulta.  
  
 *valor* deve ser 0 ou um número inteiro positivo. O intervalo permitido para *valor* é de 0 a 100. A configuração padrão para *valor* é 25.  
  
 Observe o seguinte:  
  
-   Configuração *valor* como 0 impede que consultas com operações de classificação e HASH JOIN em grupos de carga de trabalho definidos pelo usuário em execução.  
  
-   Não é recomendável definir *valor* maior que 70, porque o servidor pode estar não é possível definir separar memória livre suficiente se outras consultas simultâneas estiverem em execução. Isso pode eventualmente levar ao erro 8645, tempo limite da consulta excedido.  
  
> [!NOTE]  
>  Se os requisitos de memória de consulta excederem o limite especificado por esse parâmetro, o servidor fará o seguinte:  
>   
>  Para grupos de cargas de trabalho definidos pelo usuário, o servidor tenta reduzir o grau de paralelismo da consulta, até que o requisito de memória caia abaixo do limite, ou até que o grau de paralelismo seja igual a 1. Se o requisito de memória de consulta ainda for maior que o limite, ocorrerá o erro 8657.  
>   
>  Para grupos de cargas de trabalho internos e padrão, o servidor permite que a consulta obtenha a memória necessária.  
>   
>  Esteja ciente de que ambos os casos estarão sujeitos ao erro de tempo limite 8645 se a memória física do servidor for insuficiente.  
  
 REQUEST_MAX_CPU_TIME_SEC =*value*  
 Especifica o tempo máximo de CPU, em segundos, que uma solicitação pode usar. *valor* deve ser 0 ou um número inteiro positivo. A configuração padrão para *valor* é 0, o que significa ilimitado.  
  
> [!NOTE]  
> Por padrão, o administrador de recursos não impedirá uma solicitação de continue se o tempo máximo for excedido. Porém, um evento será gerado. Para obter mais informações, consulte [limite de CPU excedido classe de evento](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md). 

> [!IMPORTANT]
> Começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 e usando [2422 do sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md), administrador de recursos será anular uma solicitação quando o tempo máximo for excedido.
  
 REQUEST_MEMORY_GRANT_TIMEOUT_SEC =*value*  
 Especifica o tempo máximo, em segundos, que uma consulta pode aguardar pela concessão de memória (memória do buffer de trabalho).  
  
> [!NOTE]  
>  Nem sempre uma consulta falha quando o tempo limite de concessão de memória é atingido. A consulta falhará somente se houver muitas consultas simultâneas em execução. Caso contrário, a consulta poderá obter apenas a concessão de memória mínima, resultando em uma queda no desempenho de consulta.  
  
 *valor* deve ser um inteiro positivo. A configuração padrão para *valor*, 0, usa um cálculo interno baseado no custo da consulta para determinar o tempo máximo.  
  
 MAX_DOP =*value*  
 Especifica o DOP (grau máximo de paralelismo) para solicitações paralelas. *valor* deve ser 0 ou um número inteiro positivo, 1 a 255. Quando *valor* é 0, o servidor escolherá o grau máximo de paralelismo. Essa é a configuração padrão e recomendada.  
  
> [!NOTE]  
>  O valor real que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] define para MAX_DOP poderia ser menos que o valor especificado. O valor final é determinado pela fórmula min (255, *número de CPUs)*.  
  
> [!CAUTION]  
>  Alterar MAX_DOP pode comprometer o desempenho de um servidor. Se você precisar alterar MAX_DOP, nós recomendaremos que seja definido um valor menor que ou igual ao número máximo de agendadores de hardware que existem em um único nó NUMA. Nós recomendamos que você não defina MAX_DOP como um valor maior que 8.  
  
 MAX_DOP é tratado como segue:  
  
-   MAX_DOP como dica de consulta será cumprido, contanto que não exceda o grupo de cargas de trabalho MAX_DOP.  
  
-   MAX_DOP como uma dica de consulta sempre substitui o 'grau máximo de paralelismo' sp_configure.  
  
-   O grupo de carga de trabalho MAX_DOP substitui o 'grau máximo de paralelismo' sp_configure.  
  
-   Se a consulta for marcada como serial (MAX_DOP = 1 ) em tempo de compilação, não poderá ser revertida para paralela em tempo de execução, independentemente do grupo de cargas de trabalho ou da configuração sp_configure.  
  
 Depois de ser configurado, o DOP só pode ser reduzido sob pressão de concessão de memória. A reconfiguração do grupo de carga de trabalho não é visível durante a espera na fila de concessão de memória.  
  
 GROUP_MAX_REQUESTS =*value*  
 Especifica o número máximo de solicitações simultâneas permitido para execução no grupo de carga de trabalho. *valor* deve ser 0 ou um número inteiro positivo. A configuração padrão para *valor*, 0, permite solicitações ilimitadas. Quando as solicitações simultâneas máximas são alcançadas, um usuário nesse grupo pode fazer logon, mas é colocado em um estado de espera até que as solicitações simultâneas sejam ignoradas abaixo do valor especificado.  
  
 USANDO { *nome_do_pool* | "**padrão**"}  
 Associa o grupo de carga de trabalho com o pool de recursos definidos pelo usuário identificado pelo *nome_do_pool*, que, na realidade, coloca o grupo de carga de trabalho no pool de recursos. Se *nome_do_pool* não foi fornecido ou se o argumento USING não for usado, o grupo de carga de trabalho será colocado no pool padrão predefinido do administrador de recursos.  
  
 A opção "default" deve estar entre aspas ("") ou colchetes ([]) quando usado com ALTER WORKLOAD GROUP para evitar conflito com DEFAULT, que é uma palavra reservada do sistema. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
> [!NOTE]  
>  A opção "default" diferencia maiúsculas de minúsculas.  
  
## <a name="remarks"></a>Remarks  
 ALTER WORKLOAD GROUP é permitido no grupo padrão.  
  
 As alterações na configuração do grupo de cargas de trabalho não entrarão em vigor enquanto ALTER RESOURCE GOVERNOR RECONFIGURE não for executado. Ao alterar um plano que afetam a configuração, a nova configuração só terão efeito em planos em cache anteriormente após a execução de DBCC FREEPROCCACHE (*nome_do_pool*), onde *nome_do_pool* é o nome de um recurso Pool de recursos de administrador no qual o grupo de carga de trabalho está associado.  
  
-   Se você estiver alterando MAX_DOP como 1, a execução de DBCC FREEPROCCACHE não é necessária porque planos paralelos podem executar em modo serial. No entanto, não é tão eficiente quanto um plano compilado como um plano serial.  
  
-   Se você estiver alterando MAX_DOP de 1 para 0 ou um valor maior que 1, a execução de DBCC FREEPROCCACHE não é necessário. No entanto, os planos seriais não pode ser executado em paralelo, para que limpar o cache do respectivo permitirá novos planos para potencialmente ser compilado usando paralelismo.  
  
> [!CAUTION]  
>  Planos em cache de um pool de recursos que está associado a mais de um grupo de carga de trabalho de limpeza afetará todos os grupos de cargas de trabalho com o pool de recursos definidos pelo usuário identificado pelo *nome_do_pool*.  
  
 Ao executar instruções DDL, é recomendável estar familiarizado com os estados do Administrador de Recursos. Para obter mais informações, consulte [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).  
  
 REQUEST_MEMORY_GRANT_PERCENT: no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], a criação de índice pode usar mais memória do espaço de trabalho do que aquela inicialmente concedida a fim de melhorar o desempenho. Esse tratamento especial tem suporte do Administrador de Recursos em versões posteriores. No entanto, a concessão inicial e qualquer concessão de memória adicional estão limitadas pelas configurações de pool de recursos e de grupo de cargas de trabalho.  
  
 **Criação de índice em uma tabela particionada**  
  
 A memória consumida pela criação de índice em uma tabela particionada desalinhada é proporcional ao número de partições envolvidas.  Se a memória total necessária exceder o limite por consulta (REQUEST_MAX_MEMORY_GRANT_PERCENT) imposto pela configuração de grupo de cargas de trabalho do Administrador de Recursos, poderá ocorrer uma falha na criação do índice. Como o grupo de carga de trabalho "padrão" permite que uma consulta exceda o limite por consulta com o mínimo de memória requerida para iniciar, para compatibilidade com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o usuário talvez possa executar a mesma criação de índice no grupo de carga de trabalho "padrão" caso o pool de recursos "padrão" tenha memória total suficiente configurada para executar tal consulta.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como alterar a importância de solicitações no grupo padrão de `MEDIUM` para `LOW`.  
  
```  
ALTER WORKLOAD GROUP "default"  
WITH (IMPORTANCE = LOW);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
 O exemplo a seguir mostra como mover um grupo de cargas de trabalho do pool em que ele se encontra para o pool padrão.  
  
```  
ALTER WORKLOAD GROUP adHoc  
USING [default];  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
