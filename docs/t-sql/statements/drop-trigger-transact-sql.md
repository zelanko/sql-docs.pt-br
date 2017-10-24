---
title: DROP TRIGGER (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP TRIGGER
- DROP_TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- renaming triggers
- triggers [SQL Server], removing
- DDL triggers, removing
- DROP TRIGGER statement
- deleting triggers
- dropping triggers
- removing triggers
- DML triggers, removing
ms.assetid: 092d0d71-9f1e-4e38-a1c4-2487adfa5b4e
caps.latest.revision: 53
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e3ca35b2b33a60d0af5dd31467f1381402f8f99b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="drop-trigger-transact-sql"></a>DROP TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Remove um ou mais gatilhos DML ou DDL do banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  
  
DROP TRIGGER [ IF EXISTS ] [schema_name.]trigger_name [ ,...n ] [ ; ]  
  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, REVOKE or UPDATE statement (DDL Trigger)  
  
DROP TRIGGER [ IF EXISTS ] trigger_name [ ,...n ]   
ON { DATABASE | ALL SERVER }   
[ ; ]  
  
-- Trigger on a LOGON event (Logon Trigger)  
  
DROP TRIGGER [ IF EXISTS ] trigger_name [ ,...n ]   
ON ALL SERVER  
```  

  
## <a name="arguments"></a>Argumentos  
 *SE EXISTIR*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658), [!INCLUDE[sssds](../../includes/sssds-md.md)]).  
  
 Condicionalmente descarta o gatilho apenas se ele já existe.  
  
 *schema_name*  
 É o nome do esquema ao qual o gatilho DML pertence. Os gatilhos DML são definidos no escopo do esquema da tabela ou na exibição na qual são criados. *schema_name* não pode ser especificado para gatilhos DDL ou de logon.  
  
 *trigger_name*  
 É o nome do gatilho a ser removido. Para ver uma lista dos gatilhos atualmente criados, use [server_assembly_modules](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) ou [server_triggers](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md).  
  
 DATABASE  
 Indica que o escopo do gatilho DDL é aplicado ao banco de dados atual. DATABASE deverá ser especificado se também foi especificado quando o gatilho foi criado ou modificado.  
  
 ALL SERVER  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Indica que o escopo do gatilho DDL é aplicado ao servidor atual. ALL SERVER deverá ser especificado se também foi especificado quando o gatilho foi criado ou modificado. ALL SERVER também é aplicado a gatilhos de logon.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
## <a name="remarks"></a>Comentários  
 Você pode remover um gatilho DML descartando-o ou descartando a tabela do gatilho. Quando uma tabela é descartada, todos os gatilhos associados também são descartados.  
  
 Quando um gatilho é descartado, informações sobre o gatilho são removidas o **sys. Objects**, **Triggers** e **sql_modules** exibições do catálogo.  
  
 Somente será possível descartar vários gatilhos DDL por instrução DROP TRIGGER caso todos os gatilhos foram criados usando cláusulas ON idênticas.  
  
 Para renomear um gatilho, use DROP TRIGGER e CREATE TRIGGER. Para alterar a definição de um gatilho, use ALTER TRIGGER.  
  
 Para obter mais informações sobre como determinar as dependências de um gatilho específico, consulte [sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md), [sql_referenced_entities &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md), e [sql_referencing_entities &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md).  
  
 Para obter mais informações sobre como exibir o texto do gatilho, consulte [sp_helptext &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md) e [sys. sql_modules &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md).  
  
 Para obter mais informações sobre como exibir uma lista dos gatilhos existentes, consulte [Triggers &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) e [server_triggers &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 O descarte de um gatilho DML requer permissão ALTER na tabela ou exibição na qual o gatilho está definido.  
  
 O descarte de um gatilho DDL definido com escopo no servidor (ON ALL SERVER) ou de um gatilho de logon requer permissão CONTROL SERVER no servidor. O descarte de um gatilho DDL definido com escopo no banco de dados (ON DATABASE) requer permissão ALTER ANY DATABASE DDL TRIGGER no banco de dados atual.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-dropping-a-dml-trigger"></a>A. Descartando um gatilho DML  
 O exemplo a seguir remove o gatilho `employee_insupd` do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. (Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] você pode usar a sintaxe DROP TRIGGER IF EXISTS.)  
  
```  
IF OBJECT_ID ('employee_insupd', 'TR') IS NOT NULL  
   DROP TRIGGER employee_insupd;  
```  
  
### <a name="b-dropping-a-ddl-trigger"></a>B. Descartando um gatilho DDL  
 O exemplo a seguir descarta o gatilho DDL `safety`.  
  
> [!IMPORTANT]  
>  Como gatilhos DDL não estão no escopo do esquema e, portanto não aparecem no **sys. Objects** exibição do catálogo a função OBJECT_ID não pode ser usada para consultar se eles existem no banco de dados. Os objetos que não tenham seu escopo definido para o esquema devem ser consultados usando a exibição de catálogo apropriada. Para gatilhos DDL, use **Triggers**.  
  
```  
DROP TRIGGER safety  
ON DATABASE;  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Obter informações sobre gatilhos DML](../../relational-databases/triggers/get-information-about-dml-triggers.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [sys.trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)   
 [sys.server_trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)   
 [sys.server_assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)  
  
  

