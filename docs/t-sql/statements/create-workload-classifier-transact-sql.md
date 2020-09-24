---
description: Classificador CREATE WORKLOAD (Transact-SQL)
title: Classificador CREATE WORKLOAD (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/11/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD CLASSIFIER
- WORKLOAD_CLASSIFIER_TSQL
- CREATE WORKLOAD CLASSIFIER
- CREATE_WORKLOAD_CLASSIFIER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD CLASSIFIER statement
ms.assetid: ''
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 6ba3377c525a51475cd3cf567f098e27c9c12be7
ms.sourcegitcommit: c74bb5944994e34b102615b592fdaabe54713047
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90990039"
---
# <a name="create-workload-classifier-transact-sql"></a>CREATE WORKLOAD CLASSIFIER (Transact-SQL)

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Cria um objeto de classificador para uso no gerenciamento de carga de trabalho.  O classificador alinha solicitações de entrada a um grupo de carga de trabalho com base nos parâmetros especificados na definição de instrução do classificador.  Os classificadores são avaliados com o envio de cada solicitação.  Se uma solicitação não corresponde a um classificador, ela é atribuída ao grupo de carga de trabalho padrão.  O grupo de carga de trabalho padrão é a classe de recurso smallrc.

> [!NOTE]
> O classificador de carga de trabalho assume o lugar da atribuição de classe do recurso sp_addrolemember.  Depois que os classificadores de carga de trabalho são criados, execute sp_droprolemember para remover os mapeamentos de classe de recurso redundantes.

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe

```syntaxsql
CREATE WORKLOAD CLASSIFIER classifier_name  
WITH  
    (   WORKLOAD_GROUP = 'name'  
    ,   MEMBERNAME = 'security_account' 
[ [ , ] WLM_LABEL = 'label' ]  
[ [ , ] WLM_CONTEXT = 'context' ]  
[ [ , ] START_TIME = 'HH:MM' ]  
[ [ , ] END_TIME = 'HH:MM' ]  
  
[ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }]) 
[;]
```

## <a name="arguments"></a>Argumentos

 *classifier_name*  
 Especifique o nome pelo qual o classificador de carga de trabalho é identificado.  classifier_name é um sysname.  Ele pode ter até 128 caracteres e deve ser exclusivo dentro da instância.

 *WORKLOAD_GROUP* =  *'name'*    
 Quando as condições são atendidas pelas regras de classificador, o nome mapeia a solicitação para um grupo de carga de trabalho.  o nome é um sysname.  Ele pode ter até 128 caracteres e deve ser um nome de grupo de carga de trabalho válido no momento da criação do classificador.

 Os grupos de carga de trabalho disponíveis podem ser encontrados na exibição de catálogo [sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md).

 *MEMBERNAME* =  *'security_account'*     
 A conta de segurança usada para classificação.  Security_account é um sysname, sem padrão. Security_account pode ser um usuário de banco de dados, uma função de banco de dados, um logon do Azure Active Directory ou um grupo do Azure Active Directory.
 
 *WLM_LABEL*   
 Especifica o valor do rótulo com que uma solicitação pode ser classificada.  Label é um parâmetro opcional de tipo nvarchar(255).  Use [OPTION (LABEL)](/azure/sql-data-warehouse/sql-data-warehouse-develop-label) na solicitação para corresponder à configuração do classificador.

Exemplo:

```sql
CREATE WORKLOAD CLASSIFIER wcELTLoads WITH  
( WORKLOAD_GROUP = 'wgDataLoad'
 ,MEMBERNAME     = 'ELTRole'  
 ,WLM_LABEL      = 'dimension_loads' )

SELECT COUNT(*) 
  FROM DimCustomer
  OPTION (LABEL = 'dimension_loads')
```

*WLM_CONTEXT*  
Especifica o valor do contexto da sessão com que uma solicitação pode ser classificada.  context é um parâmetro opcional de tipo nvarchar(255).  Use o [sys. sp_set_session_context](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md?view=azure-sqldw-latest) com o nome da variável igual a `wlm_context` antes de enviar uma solicitação para definir o contexto da sessão.

Exemplo:

```sql
CREATE WORKLOAD CLASSIFIER wcDataLoad WITH  
( WORKLOAD_GROUP = 'wgDataLoad'
 ,MEMBERNAME     = 'ELTRole'
 ,WLM_CONTEXT    = 'dim_load' )
 
--set session context
EXEC sys.sp_set_session_context @key = 'wlm_context', @value = 'dim_load'

--run multiple statements using the wlm_context setting
SELECT COUNT(*) FROM stg.daily_customer_load
SELECT COUNT(*) FROM stg.daily_sales_load

--turn off the wlm_context session setting
EXEC sys.sp_set_session_context @key = 'wlm_context', @value = null
```

*START_TIME* e *END_TIME*  
Especifica o start_time e end_time com relação aos quais uma solicitação pode ser classificada.  Tanto start_time quanto end_time têm o formato HH: MM no fuso horário UTC.  Start_time e end_time devem ser especificados juntos.

Exemplo:

```sql
CREATE WORKLOAD CLASSIFIER wcELTLoads WITH  
( WORKLOAD_GROUP = 'wgDataLoads'
 ,MEMBERNAME     = 'ELTRole'  
 ,START_TIME     = '22:00'
 ,END_TIME       = '02:00' )
```

*IMPORTANCE* = { LOW \| BELOW_NORMAL \| NORMAL \| ABOVE_NORMAL \| HIGH }  
Especifica a importância relativa de uma solicitação.  A importância é uma das seguintes:

- LOW
- BELOW_NORMAL
- NORMAL (padrão)
- ABOVE_NORMAL
- HIGH  

Se a importância não for especificada, a configuração de importância do grupo de carga de trabalho será usada.  A importância do grupo de carga de trabalho padrão é normal.  A importância influencia a ordem na qual as solicitações são agendadas, oferecendo primeiro acesso a recursos e bloqueios.

## <a name="classification-parameter-weighting"></a>Peso do parâmetro de classificação

Uma solicitação pode corresponder a vários classificadores.  Há um peso para os parâmetros do classificador.  O classificador de correspondência com maior peso é usado para atribuir um grupo de carga de trabalho e uma importância.  O peso é o seguinte:

|Parâmetro do classificador |Peso   |
|---------------------|---------|
|USER                 |64       |
|ROLE                 |32       |
|WLM_LABEL            |16       |
|WLM_CONTEXT          |8        |
|START_TIME/END_TIME  |4        |

Considere as seguintes configurações de classificador.

```sql
CREATE WORKLOAD CLASSIFIER classifierA WITH  
( WORKLOAD_GROUP = 'wgDashboards'  
 ,MEMBERNAME     = 'userloginA'
 ,IMPORTANCE     = HIGH
 ,WLM_LABEL      = 'salereport' )

CREATE WORKLOAD CLASSIFIER classifierB WITH  
( WORKLOAD_GROUP = 'wgUserQueries'  
 ,MEMBERNAME     = 'userloginA'
 ,IMPORTANCE     = LOW
 ,START_TIME     = '18:00'
 ,END_TIME       = '07:00' )
```

O usuário `userloginA` está configurado para os dois classificadores.  Se userloginA executar uma consulta com um rótulo igual a `salesreport` entre 18h e 7h UTC, a solicitação será classificada para o grupo de carga de trabalho wgDashboards com importância HIGH.  A expectativa pode ser classificar a solicitação para wgUserQueries com importância LOW para relatórios fora do horário de trabalho, mas o peso de WLM_LABEL é maior que o de START_TIME/END_TIME.  O peso do classifierA é 80 (64 para o usuário, mais 16 para WLM_LABEL).  O peso de classifierB é 68 (64 para o usuário, 4 para START_TIME/END_TIME).  Nesse caso é possível adicionar WLM_LABEL ao classifierB.

 Para obter mais informações, confira [peso da carga de trabalho](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification#classification-weighting).

## <a name="permissions"></a>Permissões

 Requer a permissão CONTROL DATABASE.  
  
## <a name="examples"></a>Exemplos

 O exemplo seguinte mostra como criar um classificador de carga de trabalho denominado `wgcELTRole`. Ele usa o grupo de carga de trabalho staticrc20, o usuário `ELTRole` e define a importância como `above_normal`.

```sql
CREATE WORKLOAD CLASSIFIER wgcELTRole
  WITH (WORKLOAD_GROUP = 'staticrc20'
       ,MEMBERNAME = 'ELTRole'
      ,IMPORTANCE = above_normal);
```

## <a name="see-also"></a>Consulte Também

[Classificação do [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)</br>
[DROP WORKLOAD CLASSIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-classifier-transact-sql.md)</br>
[sys.workload_management_workload_classifiers](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifiers-transact-sql.md)</br>
[sys.workload_management_workload_classifier_details](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifier-details-transact-sql.md)

