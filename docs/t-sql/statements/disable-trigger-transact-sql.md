---
title: DISABLE TRIGGER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DISABLE_TSQL
- DISABLE
- DISABLE TRIGGER
- DISABLE_TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DML triggers, disabling
- DDL triggers, disabling
- DISABLE TRIGGER statement
- triggers [SQL Server], disabling
- disabling triggers
ms.assetid: e6529f06-e442-437e-a7bf-41790bc092c5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 69398e740c4ae5ca49c93b1f70d7c02a0d3fbf42
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="disable-trigger-transact-sql"></a>DISABLE TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Desabilita um gatilho.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DISABLE TRIGGER { [ schema_name . ] trigger_name [ ,...n ] | ALL }  
ON { object_name | DATABASE | ALL SERVER } [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 É o nome do esquema ao qual o gatilho pertence. *schema_name* não pode ser especificado para gatilhos DDL ou de logon.  
  
 *trigger_name*  
 É o nome do gatilho a ser desabilitado.  
  
 ALL  
 Indica que todos os gatilhos definidos no escopo da cláusula ON estão desabilitados.  
  
> [!CAUTION]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria gatilhos em bancos de dados que são publicados para replicação de mesclagem. Ao especificar ALL em bancos de dados publicados, esses gatilhos são desabilitados, interrompendo a replicação. Verifique se o banco de dados atual não foi publicado para replicação de mesclagem antes de especificar ALL.  
  
 *object_name*  
 É o nome da tabela ou exibição na qual o gatilho DML *trigger_name* foi criado para executar.  
  
 DATABASE  
 Para um gatilho DDL, indica que *trigger_name* foi criado ou modificado para ser executado com escopo de banco de dados.  
  
 ALL SERVER  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Para um gatilho DDL, indica que *trigger_name* foi criado ou modificado para ser executado com escopo no servidor. ALL SERVER também é aplicado a gatilhos de logon.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
## <a name="remarks"></a>Comentários  
 Os gatilhos são habilitados por padrão ao serem criados. Ao desabilitar um gatilho, você não o descarta. O gatilho ainda existe como um objeto no banco de dados atual. Porém, o gatilho não é acionado quando qualquer instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] em que ele tenha sido programado é executada. Os gatilhos podem ser reabilitados usando [ENABLE TRIGGER](../../t-sql/statements/enable-trigger-transact-sql.md). Gatilhos DML definidos nas tabelas podem ser também ser habilitado ou desabilitado usando [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
 Alterar o gatilho usando a **ALTER TRIGGER** instrução permite que o gatilho.  
  
## <a name="permissions"></a>Permissões  
 Para desabilitar um gatilho DML, no mínimo, um usuário deve ter a permissão ALTER na tabela ou exibição na qual o gatilho foi criado.  
  
 Para desabilitar um gatilho DDL definido com escopo de servidor (ON ALL SERVER) ou um gatilho de logon, um usuário deve ter a permissão CONTROL SERVER no servidor. Para desabilitar um gatilho DDL definido com escopo de banco de dados (ON DATABASE), no mínimo, um usuário deve ter a permissão ALTER ANY DATABASE DDL TRIGGER no banco de dados atual.  
  
## <a name="examples"></a>Exemplos  
Os exemplos a seguir são descritos no banco de dados AdventureWorks2012.
  
### <a name="a-disabling-a-dml-trigger-on-a-table"></a>A. Desabilitando um gatilho DML em uma tabela  
 O exemplo a seguir desabilita o gatilho `uAddress` que foi criado na tabela `Address`.  
  
```  
DISABLE TRIGGER Person.uAddress ON Person.Address;  
GO  
```  
  
### <a name="b-disabling-a-ddl-trigger"></a>B. Desabilitando um gatilho DDL  
 O exemplo a seguir cria um gatilho DDL `safety` com escopo definido no banco de dados e depois desabilita o mesmo.  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_TABLE, ALTER_TABLE   
AS   
   PRINT 'You must disable Trigger "safety" to drop or alter tables!'   
   ROLLBACK;  
GO  
DISABLE TRIGGER safety ON DATABASE;  
GO  
```  
  
### <a name="c-disabling-all-triggers-that-were-defined-with-the-same-scope"></a>C. Desabilitando todos os gatilhos que foram definidos com o mesmo escopo  
 O exemplo a seguir desabilita todos os gatilhos DDL que foram criados no escopo do servidor.  
  
```  
DISABLE Trigger ALL ON ALL SERVER;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
  
