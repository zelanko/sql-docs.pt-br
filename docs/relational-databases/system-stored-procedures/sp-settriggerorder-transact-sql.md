---
title: sp_settriggerorder (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_settriggerorder
- sp_settriggerorder_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_settriggerorder
ms.assetid: 8b75c906-7315-486c-bc59-293ef12078e8
caps.latest.revision: 54
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bef1fdf427c6bc510e77f8df55f3281d5b5db6cd
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spsettriggerorder-transact-sql"></a>sp_settriggerorder (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Especifica os disparadores AFTER que são acionados em primeiro ou último lugar. Os disparadores AFTER que são acionados entre o primeiro e o último disparador são executados em ordem indefinida.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_settriggerorder [ @triggername = ] '[ triggerschema. ] triggername'   
    , [ @order = ] 'value'   
    , [ @stmttype = ] 'statement_type'   
    [ , [ @namespace = ] { 'DATABASE' | 'SERVER' | NULL } ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@triggername=** ] **'**[ *triggerschema ***.**] *nome_do_disparador * '**  
 É o nome do gatilho e do esquema ao qual ele pertence, se aplicável, cuja ordem será definida ou alterada. [*triggerschema ***.**]* nome_do_disparador * é **sysname**. Se o nome não corresponder a um disparador ou se o nome corresponder a um disparador INSTEAD OF, o procedimento retornará um erro. *triggerschema* não pode ser especificado para gatilhos DDL ou de logon.  
  
 [ **@order=** ] **'***value***'**  
 É a configuração da nova ordem do disparador. *valor* é **varchar (10)** e pode ser qualquer um dos valores a seguir.  
  
> [!IMPORTANT]  
>  O **primeiro** e **último** gatilhos devem ser dois disparadores diferentes.  
  
|Value|Description|  
|-----------|-----------------|  
|**Primeiro**|O disparador é acionado em primeiro lugar.|  
|**Last**|O disparador é acionado em último lugar.|  
|**Nenhuma**|O disparador é acionado em ordem indefinida.|  
  
 [  **@stmttype=** ] **'***statement_type***'**  
 Especifica a instrução SQL que aciona o gatilho. *statement_type* é **varchar (50)** e pode ser INSERT, UPDATE, DELETE, LOGON ou qualquer [!INCLUDE[tsql](../../includes/tsql-md.md)] evento de instrução listado na [eventos DDL](../../relational-databases/triggers/ddl-events.md). Os grupos de eventos não podem ser especificados.  
  
 Um gatilho pode ser designado como o **primeiro** ou **último** disparador para um tipo de instrução somente depois que o disparador foi definido como um disparador para esse tipo de instrução. Por exemplo, acionar **TR1** pode ser designado como **primeiro** para inserção na tabela **T1** se **TR1** é definido como um disparador INSERT. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] retornará um erro se **TR1**, que foi definido somente como um gatilho de inserção está definido como um **primeiro**, ou **último**, gatilho de uma instrução UPDATE. Para obter mais informações, consulte a seção Comentários.  
  
 **@namespace=** { **'DATABASE'** | **'SERVER'** | NULL}  
 Quando *nome_do_disparador* é um gatilho DDL, **@namespace** Especifica se *nome_do_disparador* foi criado com escopo de banco de dados ou servidor. Se *nome_do_disparador* é um gatilho de logon, SERVER deve ser especificado. Para obter mais informações sobre o escopo do gatilho DDL, consulte [gatilhos DDL](../../relational-databases/triggers/ddl-triggers.md). Se não for especificado ou se NULL for especificado, *nome_do_disparador* é um gatilho DML.  
  
||  
|-|  
|SERVER aplica-se a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) e 1 (falha)  
  
## <a name="remarks"></a>Remarks  
  
## <a name="dml-triggers"></a>Gatilhos DML  
 Pode haver apenas um **primeiro** um **último** gatilho para cada instrução em uma única tabela.  
  
 Se um **primeiro** gatilho já está definido na tabela, banco de dados ou servidor, você não pode designar um novo disparador como **primeiro** para a mesma tabela, banco de dados ou servidor para o mesmo *statement_type* . Essa restrição se aplica também **último** gatilhos.  
  
 A replicação gera automaticamente um primeiro disparador para qualquer tabela que esteja incluída em uma atualização imediata ou uma assinatura de atualização em fila. A replicação requer que seu disparador seja o primeiro disparador. A replicação gerará um erro se você tentar incluir uma tabela com um primeiro disparador em uma atualização imediata ou uma assinatura de atualização em fila. Se você tentar fazer com que um gatilho seja o primeiro depois que uma tabela for incluída em uma assinatura, **sp_settriggerorder** retornará um erro. Se você usar ALTER TRIGGER no disparador de replicação ou use **sp_settriggerorder** para alterar o disparador de replicação para um **último** ou **nenhum** gatilho, a assinatura faz não funcione corretamente.  
  
## <a name="ddl-triggers"></a>Gatilhos DDL  
 Se um disparador DDL com escopo de banco de dados e um gatilho DDL com escopo no servidor existirem no mesmo evento, você pode especificar que ambos os disparadores podem ser um **primeiro** disparador ou uma **último** gatilho. Entretanto, disparadores com escopo no servidor sempre são acionados em primeiro lugar. Em geral, a ordem de execução de disparadores DDL que existem no mesmo evento é a seguinte:  
  
1.  O disparador do nível de servidor marcado como **primeiro**.  
  
2.  Outros disparadores do nível do servidor.  
  
3.  O disparador do nível de servidor marcado como **último**.  
  
4.  O disparador do nível de banco de dados marcado como **primeiro**.  
  
5.  Outros disparadores do nível do banco de dados.  
  
6.  O disparador do nível de banco de dados marcado como **último**.  
  
## <a name="general-trigger-considerations"></a>Considerações gerais sobre gatilhos  
 Se uma instrução ALTER TRIGGER alterar um primeiro ou último gatilho, o **primeiro** ou **último** atributo originalmente definido no disparador será descartado e o valor é substituído por **nenhum**. O valor de ordem deve ser redefinido usando **sp_settriggerorder**.  
  
 Se o mesmo disparador deve ser designado como a ordem do primeira ou última para mais de um tipo de instrução, **sp_settriggerorder** deve ser executado para cada tipo de instrução. Além disso, o gatilho deve ser primeiro definido para um tipo de instrução antes de ser designado como o **primeiro** ou **último** disparador a ser acionado para esse tipo de instrução.  
  
## <a name="permissions"></a>Permissões  
 A definição da ordem de um disparador DDL com escopo no servidor (criado ON ALL SERVER) ou um disparador de logon requer permissão CONTROL SERVER.  
  
 A definição da ordem de um disparador DDL com escopo no banco de dados (criado ON DATABASE) requer permissão ALTER ANY DATABASE DDL TRIGGER.  
  
 A definição da ordem de um disparador DML requer permissão ALTER na tabela ou exibição na qual o disparador está definido.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-setting-the-firing-order-for-a-dml-trigger"></a>A. Definindo a ordem de acionamento para um disparador DML  
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
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
  
