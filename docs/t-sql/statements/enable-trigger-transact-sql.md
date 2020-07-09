---
title: ENABLE TRIGGER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 26ffe6c73d00056b9b15bd07f41349b367bef02d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85735688"
---
# <a name="enable-trigger-transact-sql"></a>ENABLE TRIGGER (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Habilita um disparador DML, DDL ou de logon.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
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
É o nome da tabela ou da exibição na qual o gatilho DML *trigger_name* foi criado para ser executado.  
  
DATABASE  
Para um gatilho DDL, indica que *trigger_name* foi criado ou modificado para ser executado com o escopo do banco de dados.  
  
ALL SERVER  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.  
  
Para um gatilho DDL, indica que *trigger_name* foi criado ou modificado para ser executado com o escopo do servidor. ALL SERVER também é aplicado a gatilhos de logon.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
## <a name="remarks"></a>Comentários  
A habilitação de um disparador não recria o mesmo. Um disparador desabilitado ainda existe como um objeto no banco de dados atual, mas não é acionado. A habilitação de um disparador faz com que ele seja acionado quando forem executadas quaisquer instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] nas quais ele foi originalmente programado. Os gatilhos são desabilitados usando [DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md). Os gatilhos DML definidos em tabelas também podem ser desabilitados ou habilitados usando [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
Para habilitar um disparador DML, no mínimo, um usuário precisa ter a permissão ALTER na tabela ou exibição na qual o disparador foi criado.  
  
Para habilitar um disparador DDL definido com escopo no servidor (ON ALL SERVER) ou um disparador de logon, um usuário precisa ter permissão CONTROL SERVER no servidor. Para habilitar um disparador DDL definido com escopo no banco de dados (ON DATABASE), no mínimo, um usuário precisa ter a permissão ALTER ANY DATABASE DDL TRIGGER no banco de dados atual.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-enabling-a-dml-trigger-on-a-table"></a>a. Habilitando um gatilho DML em uma tabela  
O exemplo a seguir desabilita o gatilho `uAddress` que foi criado na tabela `Address` no banco de dados AdventureWorks e, em seguida, habilita-o.  
  
```sql  
DISABLE TRIGGER Person.uAddress ON Person.Address;  
GO  
ENABLE Trigger Person.uAddress ON Person.Address;  
GO  
```  
  
### <a name="b-enabling-a-ddl-trigger"></a>B. Habilitando um gatilho DDL  
O exemplo a seguir cria um gatilho DDL `safety` com escopo definido no banco de dados e depois o desabilita e habilita.  
  
```sql  
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
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.  
  
```sql  
ENABLE Trigger ALL ON ALL SERVER;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
  
