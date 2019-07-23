---
title: TRIGGER_NESTLEVEL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TRIGGER_NESTLEVEL
- TRIGGER_NESTLEVEL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- triggers [SQL Server], number executed
- number of triggers
- TRIGGER_NESTLEVEL function
ms.assetid: 6a33e74a-0cf9-4ae1-a1e4-4a137a3ea39d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6215824f230001cb9d7add20d32c85780a65ede6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098810"
---
# <a name="triggernestlevel-transact-sql"></a>TRIGGER_NESTLEVEL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o número de disparadores executados para a instrução que acionou o disparador. TRIGGER_NESTLEVEL é usado em disparadores DML e DDL para determinar o nível atual de aninhamento.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TRIGGER_NESTLEVEL ( [ object_id ] , [ 'trigger_type' ] , [ 'trigger_event_category' ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_id*  
 É o ID de objeto de um disparador. Se *object_id* for especificada, será retornado o número de vezes que o gatilho especificado foi executado para a instrução. Se *object_id* não for especificada, será retornado o número de vezes que todos os gatilhos foram executados para a instrução.  
  
 **'** *trigger_type* **'**  
 Especifica se deve ser aplicado TRIGGER_NESTLEVEL a disparadores AFTER ou disparadores INSTEAD OF. Especifique **AFTER** para gatilhos AFTER. Especifique **IOT** para gatilhos INSTEAD OF. Se *trigger_type* for especificado, *trigger_event_category* também deverá ser especificado.  
  
 **'** *trigger_event_category* **'**  
 Especifica se deve ser aplicado TRIGGER_NESTLEVEL a disparadores DML ou DDL. Especifique **DML** para gatilhos DML. Especifique **DDL** para gatilhos DDL. Se *trigger_event_category* for especificado, *trigger_type* também deverá ser especificado. Observe que apenas **AFTER** pode ser especificado com **DDL**, porque gatilhos DDL apenas podem ser gatilhos AFTER.  
  
## <a name="remarks"></a>Remarks  
 Quando nenhum parâmetro for especificado, TRIGGER_NESTLEVEL retornará o número total de disparadores na pilha de chamada. Isto inclui ele próprio. Pode ocorrer omissão de parâmetros quando um disparador executar comandos que causem o acionamento de outro disparador ou criar uma sucessão de disparadores de acionamento.  
  
 Para retornar o número total de gatilhos na pilha de chamadas para um tipo de gatilho e uma categoria de evento específicos, especifique *object_id* = 0.  
  
 TRIGGER_NESTLEVEL retornará 0 se for executado fora de um disparador e quaisquer parâmetros não forem NULL.  
  
 Quando quaisquer parâmetros forem especificados explicitamente como NULL, um valor NULL será retornado independentemente do fato de TRIGGER_NESTLEVEL ser usado interna ou externamente a um disparador.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-testing-the-nesting-level-of-a-specific-dml-trigger"></a>A. Testando o nível de aninhamento de um gatilho DML específico  
  
```  
IF ( (SELECT TRIGGER_NESTLEVEL( OBJECT_ID('xyz') , 'AFTER' , 'DML' ) ) > 5 )  
   RAISERROR('Trigger xyz nested more than 5 levels.',16,-1)  
```  
  
### <a name="b-testing-the-nesting-level-of-a-specific-ddl-trigger"></a>B. Testando o nível de aninhamento de um gatilho DDL específico  
  
```  
IF ( ( SELECT TRIGGER_NESTLEVEL ( ( SELECT object_id FROM sys.triggers  
WHERE name = 'abc' ), 'AFTER' , 'DDL' ) ) > 5 )  
   RAISERROR ('Trigger abc nested more than 5 levels.',16,-1)  
```  
  
### <a name="c-testing-the-nesting-level-of-all-triggers-executed"></a>C. Testando o nível de aninhamento de todos os gatilhos executados  
  
```  
IF ( (SELECT trigger_nestlevel() ) > 5 )  
   RAISERROR  
      ('This statement nested over 5 levels of triggers.',16,-1)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  
