---
description: sp_settriggerorder (Transact-SQL)
title: sp_settriggerorder (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_settriggerorder
- sp_settriggerorder_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_settriggerorder
ms.assetid: 8b75c906-7315-486c-bc59-293ef12078e8
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6d8ef1360e35d084703a4f86590ade57be6a4c24
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468297"
---
# <a name="sp_settriggerorder-transact-sql"></a>sp_settriggerorder (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Especifica os disparadores AFTER que são acionados em primeiro ou último lugar. Os disparadores AFTER que são acionados entre o primeiro e o último disparador são executados em ordem indefinida.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_settriggerorder [ @triggername = ] '[ triggerschema. ] triggername'   
    , [ @order = ] 'value'   
    , [ @stmttype = ] 'statement_type'   
    [ , [ @namespace = ] { 'DATABASE' | 'SERVER' | NULL } ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @triggername = ] '[ _triggerschema.] _triggername'` É o nome do gatilho e o esquema ao qual ele pertence, se aplicável, cuja ordem deve ser definida ou alterada. [_triggerschema_**.**] *triggername* é **sysname**. Se o nome não corresponder a um disparador ou se o nome corresponder a um disparador INSTEAD OF, o procedimento retornará um erro. *triggerschema* não pode ser especificado para gatilhos DDL ou de logon.  
  
`[ @order = ] 'value'` É a configuração para a nova ordem do gatilho. o *valor* é **varchar (10)** e pode ser qualquer um dos valores a seguir.  
  
> [!IMPORTANT]  
>  O **primeiro** e o **último** gatilho devem ser dois gatilhos diferentes.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**First**|O disparador é acionado em primeiro lugar.|  
|**Last**|O disparador é acionado em último lugar.|  
|**Nenhum**|O disparador é acionado em ordem indefinida.|  
  
`[ @stmttype = ] 'statement_type'` Especifica a instrução SQL que dispara o gatilho. *statement_type* é **varchar (50)** e pode ser inserir, atualizar, excluir, fazer logon ou qualquer [!INCLUDE[tsql](../../includes/tsql-md.md)] evento de instrução listado em [eventos DDL](../../relational-databases/triggers/ddl-events.md). Os grupos de eventos não podem ser especificados.  
  
 Um gatilho pode ser designado como o **primeiro** ou **último** gatilho para um tipo de instrução somente depois que esse gatilho tiver sido definido como um gatilho para esse tipo de instrução. Por exemplo, o disparador de **TR1** pode ser designado **primeiro** para INSERT na tabela **T1** se o **TR1** for definido como um gatilho de inserção. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] retorna um erro se o **TR1**, que foi definido somente como um gatilho de inserção, é definido como um gatilho **First** ou **Last**, para uma instrução UPDATE. Para obter mais informações, consulte a seção Comentários.  
  
 **\@ namespace =** { **' banco de dados '**'  |  **servidor** ' | NULO  
 Quando *triggername* é um gatilho DDL, **\@ namespace** especifica se *triggername* foi criado com escopo de banco de dados ou escopo de servidor. Se *triggername* for um gatilho de logon, o servidor deverá ser especificado. Para obter mais informações sobre o escopo do gatilho DDL, consulte [gatilhos DDL](../../relational-databases/triggers/ddl-triggers.md). Se não for especificado, ou se NULL for especificado, *triggername* será um gatilho DML.  
  
* O servidor aplica-se a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) e 1 (falha)  
  
## <a name="remarks"></a>Comentários  
  
## <a name="dml-triggers"></a>Gatilhos DML  
 Pode haver apenas um **primeiro** e um **último** gatilho para cada instrução em uma única tabela.  
  
 Se um **primeiro** gatilho já estiver definido na tabela, no banco de dados ou no servidor, você não poderá designar um novo gatilho como **primeiro** para a mesma tabela, banco de dados ou servidor para o mesmo *statement_type*. Essa restrição também aplica os **últimos** gatilhos.  
  
 A replicação gera automaticamente um primeiro disparador para qualquer tabela que esteja incluída em uma atualização imediata ou uma assinatura de atualização em fila. A replicação requer que seu disparador seja o primeiro disparador. A replicação gerará um erro se você tentar incluir uma tabela com um primeiro disparador em uma atualização imediata ou uma assinatura de atualização em fila. Se você tentar fazer com que um gatilho seja o primeiro depois que uma tabela for incluída em uma assinatura, **sp_settriggerorder** retornará um erro. Se você usar ALTER TRIGGER no gatilho de replicação ou usar **sp_settriggerorder** para alterar o gatilho de replicação para um gatilho **Last** ou **None** , a assinatura não funcionará corretamente.  
  
## <a name="ddl-triggers"></a>Gatilhos DDL  
 Se um gatilho DDL com escopo de banco de dados e um gatilho DDL com escopo de servidor existirem no mesmo evento, você poderá especificar que ambos os gatilhos sejam um **primeiro** gatilho ou um **último** gatilho. Entretanto, disparadores com escopo no servidor sempre são acionados em primeiro lugar. Em geral, a ordem de execução de disparadores DDL que existem no mesmo evento é a seguinte:  
  
1.  O gatilho de nível de servidor marcado **primeiro**.  
  
2.  Outros disparadores do nível do servidor.  
  
3.  O gatilho de nível de servidor marcado como **último**.  
  
4.  O gatilho de nível de banco de dados marcado **primeiro**.  
  
5.  Outros disparadores do nível do banco de dados.  
  
6.  O gatilho de nível de banco de dados marcado como **último**.  
  
## <a name="general-trigger-considerations"></a>Considerações gerais sobre gatilhos  
 Se uma instrução ALTER TRIGGER alterar um primeiro ou último gatilho, o **primeiro** ou **último** atributo originalmente definido no gatilho será descartado e o valor será substituído por **None**. O valor do pedido deve ser redefinido usando **sp_settriggerorder**.  
  
 Se o mesmo gatilho deve ser designado como a primeira ou última ordem para mais de um tipo de instrução, **sp_settriggerorder** deve ser executado para cada tipo de instrução. Além disso, o gatilho deve ser definido primeiro para um tipo de instrução antes que possa ser designado como o **primeiro** ou **último** gatilho a ser acionado para esse tipo de instrução.  
  
## <a name="permissions"></a>Permissões  
 A definição da ordem de um disparador DDL com escopo no servidor (criado ON ALL SERVER) ou um disparador de logon requer permissão CONTROL SERVER.  
  
 A definição da ordem de um disparador DDL com escopo no banco de dados (criado ON DATABASE) requer permissão ALTER ANY DATABASE DDL TRIGGER.  
  
 A definição da ordem de um disparador DML requer permissão ALTER na tabela ou exibição na qual o disparador está definido.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-setting-the-firing-order-for-a-dml-trigger"></a>a. Definindo a ordem de acionamento para um disparador DML  
 O exemplo a seguir especifica que o disparador `uSalesOrderHeader` será o primeiro disparador a ser acionado depois que uma operação `UPDATE` ocorrer na tabela `Sales.SalesOrderHeader`.  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'Sales.uSalesOrderHeader', @order='First', @stmttype = 'UPDATE';  
```  
  
### <a name="b-setting-the-firing-order-for-a-ddl-trigger"></a>B. Definindo a ordem de acionamento para um disparador DDL  
 O exemplo a seguir especifica que o disparador `ddlDatabaseTriggerLog` será o primeiro disparador a ser acionado depois que um evento `ALTER_TABLE` ocorrer no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'ddlDatabaseTriggerLog', @order='First', @stmttype = 'ALTER_TABLE', @namespace = 'DATABASE';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
  
