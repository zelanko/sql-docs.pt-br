---
title: Criar grupo de cargas de trabalho (Transact-SQL) | Microsoft Docs
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
- WORKLOAD GROUP
- WORKLOAD_GROUP_TSQL
- CREATE WORKLOAD GROUP
- CREATE_WORKLOAD_GROUP_TSQL
dev_langs: TSQL
helpviewer_keywords: CREATE WORKLOAD GROUP statement
ms.assetid: d949e540-9517-4bca-8117-ad8358848baa
caps.latest.revision: "47"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cec1360259d78679fab31a45a074d5fbbf3779b5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="create-workload-group-transact-sql"></a>CREATE WORKLOAD GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um grupo de carga de trabalho do Administrador de recursos e o associa a um pool de recursos do Administrador de recursos. Administrador de recursos não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
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
 É o nome definido pelo usuário do grupo de carga de trabalho. *group_name* é alfanumérico, pode ter até 128 caracteres, deve ser exclusivo dentro de uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e deve estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 IMPORTÂNCIA = {BAIXO | **MÉDIO** | ALTA}  
 Especifica a importância relativa de uma solicitação no grupo de carga de trabalho. A importância é uma das seguintes, com MEDIUM sendo o padrão:  
  
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
 Especifica o tempo máximo, em segundos, que uma consulta pode esperar pela disponibilização de uma concessão de memória (memória do buffer do trabalho).  
  
> [!NOTE]  
>  Nem sempre uma consulta falha quando o tempo limite de concessão de memória é atingido. A consulta falhará somente se houver muitas consultas simultâneas em execução. Caso contrário, a consulta poderá obter apenas a concessão de memória mínima, resultando em uma queda no desempenho de consulta.  
  
 *valor* deve ser 0 ou um número inteiro positivo. A configuração padrão para *valor*, 0, usa um cálculo interno baseado no custo da consulta para determinar o tempo máximo.  
  
 MAX_DOP =*value*  
 Especifica o DOP (grau máximo de paralelismo) para solicitações paralelas. *valor* deve ser 0 ou um número inteiro positivo. O intervalo permitido para *valor* é de 0 a 64. A configuração padrão para *valor*, 0, usa a configuração global. MAX_DOP é tratado como segue:  
  
-   MAX_DOP como dica de consulta é válido, contanto que não exceda o grupo de carga de trabalho MAX_DOP. Se o valor de dica de consulta MAXDOP exceder o valor que está configurado usando o Administrador de Recursos, o Mecanismo de Banco de Dados usará o valor MAXDOP do Administrador de Recursos.  
  
-   MAX_DOP como uma dica de consulta sempre substitui o 'grau máximo de paralelismo' sp_configure.  
  
-   O grupo de carga de trabalho MAX_DOP substitui o 'grau máximo de paralelismo' sp_configure.  
  
-   Se a consulta for marcada como serial em tempo de compilação, ela não poderá ser revertida a paralela em tempo de execução, independentemente do grupo de carga de trabalho ou da configuração sp_configure.  
  
-   Depois de ser configurado, o DOP só pode ser reduzido sob pressão de concessão de memória. A reconfiguração do grupo de carga de trabalho não é visível durante a espera na fila de concessão de memória.  
  
 GROUP_MAX_REQUESTS =*value*  
 Especifica o número máximo de solicitações simultâneas permitido para execução no grupo de carga de trabalho. *valor* deve ser 0 ou um número inteiro positivo. A configuração padrão para *valor*, 0, permite solicitações ilimitadas. Quando as solicitações simultâneas máximas são alcançadas, um usuário nesse grupo pode fazer logon, mas é colocado em um estado de espera até que as solicitações simultâneas sejam ignoradas abaixo do valor especificado.  
  
 USANDO { *nome_do_pool* | **"padrão"** }  
 Associa o grupo de carga de trabalho com o pool de recursos definidos pelo usuário identificado pelo *nome_do_pool*. Na realidade, isso coloca o grupo de carga de trabalho no pool de recursos. Se *nome_do_pool* não for fornecido, ou se o argumento USING não for usado, o grupo de carga de trabalho será colocado no pool padrão predefinido do administrador de recursos.  
  
 "default" é uma palavra reservada e, quando usada com USING, deve ficar entre aspas ("") ou colchetes ([]).  
  
> [!NOTE]  
>  Grupos de cargas de trabalho e pools de recursos predefinidos usam nomes em letras minúsculas, como "default". Isso deve ser levado em consideração nos servidores que usam agrupamento com diferenciação de maiúsculas e minúsculas. Os servidores com agrupamento sem diferenciação de maiúsculas e minúsculas, como SQL_Latin1_General_CP1_CI_AS, tratarão "default" e "Default" da mesma maneira.  
  
 External_pool_name externo | "padrão"  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 Grupo de carga de trabalho pode especificar um pool de recursos externos. Você pode definir um grupo de carga de trabalho e associar 2 pools:  
  
-   Um pool de recursos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cargas de trabalho e consultas  
  
-   Um pool de recursos externos para processos externos. Para obter mais informações, consulte [sp_execute_external_script &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 REQUEST_MEMORY_GRANT_PERCENT: a criação de índice pode usar mais memória de espaço de trabalho do que aquela inicialmente concedida a fim de melhorar o desempenho. Esse tratamento especial tem o suporte do Administrador de Recursos no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Porém, a concessão inicial e qualquer concessão de memória adicional estão limitadas pelas configurações de pool de recursos e de grupo de carga de trabalho.  
  
 **Criação de índice em uma tabela particionada**  
  
 A memória consumida pela criação de índice em uma tabela particionada desalinhada é proporcional ao número de partições envolvidas. Se a memória total necessária exceder o limite por consulta (REQUEST_MAX_MEMORY_GRANT_PERCENT) imposto pela configuração de grupo de cargas de trabalho do Administrador de Recursos, poderá ocorrer uma falha na criação do índice. Como o grupo de carga de trabalho "padrão" permite que uma consulta exceda o limite por consulta com o mínimo de memória necessária, o usuário talvez possa executar a mesma criação de índice no grupo de carga de trabalho "padrão" caso o pool de recursos "padrão" tenha memória total suficiente configurada para executar tal consulta.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER.  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte mostra como criar um grupo de carga de trabalho denominado `newReports`. Ele usa as configurações padrão do Administrador de Recursos e está no pool padrão desse Administrador. O exemplo especifica o pool `default`, mas isso não é necessário.  
  
```  
CREATE WORKLOAD GROUP newReports  
    USING "default" ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  

