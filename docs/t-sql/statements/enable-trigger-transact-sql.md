---
title: ENABLE TRIGGER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ENABLE TRIGGER
- ENABLE_TSQL
- ENABLE_TRIGGER_TSQL
- ENABLE
dev_langs:
- TSQL
helpviewer_keywords:
- DDL triggers, enabling
- triggers [SQL Server], enabling
- DML triggers, enabling
- ENABLE TRIGGER statement
ms.assetid: 6e21f0ad-68d0-432f-9c7c-a119dd2d3fc9
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fb2fba080ea3c51e5c29456b2166eeea6274f8a3
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="enable-trigger-transact-sql"></a>ENABLE TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Habilita um disparador DML, DDL ou de logon.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ENABLE TRIGGER { [ schema_name . ] trigger_name [ ,...n ] | ALL }  
ON { object_name | DATABASE | ALL SERVER } [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 É o nome do esquema ao qual o gatilho pertence. *schema_name* não pode ser especificado para gatilhos DDL ou de logon.  
  
 *trigger_name*  
 É o nome do disparador a ser habilitado.  
  
 ALL  
 Indica que todos os disparadores definidos no escopo da cláusula ON estão habilitados.  
  
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
 A habilitação de um disparador não recria o mesmo. Um disparador desabilitado ainda existe como um objeto no banco de dados atual, mas não é acionado. A habilitação de um disparador faz com que ele seja acionado quando forem executadas quaisquer instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] nas quais ele foi originalmente programado. Os gatilhos são desabilitados usando [DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md). Gatilhos DML definidos nas tabelas podem ser também ser habilitado ou desabilitado usando [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Para habilitar um disparador DML, no mínimo, um usuário deve ter a permissão ALTER na tabela ou exibição na qual o disparador foi criado.  
  
 Para habilitar um disparador DDL definido com escopo no servidor (ON ALL SERVER) ou um disparador de logon, um usuário deve ter permissão CONTROL SERVER no servidor. Para habilitar um disparador DDL definido com escopo no banco de dados (ON DATABASE), no mínimo, um usuário deve ter a permissão ALTER ANY DATABASE DDL TRIGGER no banco de dados atual.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-enabling-a-dml-trigger-on-a-table"></a>A. Habilitando um gatilho DML em uma tabela  
 O exemplo a seguir desabilita o gatilho `uAddress` que foi criado na tabela `Address` no banco de dados AdventureWorks e, em seguida, habilita a ele.  
  
```  
DISABLE TRIGGER Person.uAddress ON Person.Address;  
GO  
ENABLE Trigger Person.uAddress ON Person.Address;  
GO  
```  
  
### <a name="b-enabling-a-ddl-trigger"></a>B. Habilitando um gatilho DDL  
 O exemplo a seguir cria um gatilho DDL `safety` com escopo de banco de dados e, em seguida, desabilitar e permite que ele.  
  
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
ENABLE TRIGGER safety ON DATABASE;  
GO  
```  
  
### <a name="c-enabling-all-triggers-that-were-defined-with-the-same-scope"></a>C. Habilitando todos os gatilhos que foram definidos com o mesmo escopo  
 O exemplo a seguir habilita todos os disparadores DDL que foram criados no escopo do servidor.  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
ENABLE Trigger ALL ON ALL SERVER;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
  

