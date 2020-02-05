---
title: Especificar o primeiro e o último gatilho | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- first triggers [SQL Server]
- last triggers
- DML triggers, first or last triggers
- INSTEAD OF triggers
- AFTER triggers
ms.assetid: 9e6c7684-3dd3-46bb-b7be-523b33fae4d5
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1020bb9dff821471f33ba3af9285249a93980133
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68055993"
---
# <a name="specify-first-and-last-triggers"></a>Especificar o primeiro e o último gatilhos
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  É possível especificar que um dos gatilhos AFTER associados a uma tabela seja tanto o primeiro gatilho AFTER quanto o último gatilho AFTER, acionado para cada uma das ações de gatilho - INSERT, DELETE e UPDATE. Os disparadores AFTER que são acionados entre o primeiro e o último disparador são executados em ordem indefinida.  
  
 Para especificar a ordem para um gatilho AFTER, use o procedimento armazenado **sp_settriggerorder** . **sp_settriggerorder** tem as opções a seguir.  
  
|Opção|DESCRIÇÃO|  
|------------|-----------------|  
|**First**|Especifica que o gatilho DML é o primeiro gatilho AFTER acionado para uma ação de gatilho.|  
|**Last**|Especifica que o gatilho DML é o último gatilho AFTER acionado para uma ação de gatilho.|  
|**Nenhuma**|Especifica que não há nenhuma ordem específica na qual o gatilho DML deva ser acionado. Usado, principalmente, para redefinir um gatilho a ser o primeiro ou o último.|  
  
 O seguinte exemplo mostra o uso de **sp_settriggerorder**:  
  
```  
sp_settriggerorder @triggername = 'MyTrigger', @order = 'first', @stmttype = 'UPDATE'  
```  
  
> [!IMPORTANT]  
>  O primeiro e o último gatilho devem ser dois gatilhos DML diferentes.  
  
 Uma tabela pode definir os gatilhos INSERT, UPDATE, e DELETE para serem acionados ao mesmo tempo. Cada instrução pode ter seus próprios primeiros e últimos gatilhos, mas os gatilhos não podem ser os mesmos.  
  
 Caso o primeiro ou o último gatilho definido para uma tabela não abranja uma ação de gatilho, por exemplo, INSERT, DELETE e UPDATE, não haverá primeiro ou último gatilho para ações perdidas.  
  
 Gatilhos INSTEAD OF não podem ser especificados como primeiro ou último. Os gatilhos INSTEAD OF são acionados antes que as atualizações das tabelas subjacentes sejam feitas. Se as atualizações forem feitas pelo gatilho INSTEAD OF às tabelas subjacentes, as atualizações ocorrerão antes que qualquer gatilho AFTER, definido na tabela, seja acionado. Por exemplo, se um gatilho INSTEAD OF INSERT em uma exibição, inserir dados em uma tabela base e a tabela base tiver um gatilho INSTEAD OF INSERT e três gatilhos AFTER INSERT, o gatilho INSTEAD OF INSERT na tabela base, será acionado em vez da ação de inserção e os gatilhos AFTER na tabela base, serão acionados após qualquer ação de inserção na tabela base. Para obter mais informações, consulte [DML Triggers](../../relational-databases/triggers/dml-triggers.md).  
  
 Se uma instrução ALTER TRIGGER alterar o primeiro ou o último gatilho, os atributos **First** ou **Last** serão removidos e o valor do pedido será definido como **None**. O pedido deve ser redefinido com **sp_settriggerorder**.  
  
 A função OBJECTPROPERTY relata se um gatilho é um primeiro ou último gatilho usando as seguintes propriedades: **ExecIsFirstInsertTrigger**, **ExecIsFirstUpdateTrigger**, **ExecIsFirstDeleteTrigger**, **ExecIsLastInsertTrigger**, **ExecIsLastUpdateTrigger** e **ExecIsLastDeleteTrigger**.  
  
 A replicação gera automaticamente um primeiro disparador para qualquer tabela que esteja incluída em uma atualização imediata ou uma assinatura de atualização em fila. A replicação requer que seu disparador seja o primeiro disparador. A replicação gerará um erro se você tentar incluir uma tabela com um primeiro disparador em uma atualização imediata ou uma assinatura de atualização em fila. Se você tentar fazer com que um gatilho seja o primeiro depois que uma tabela for incluída em uma assinatura, **sp_settriggerorder** retornará um erro. Se você usar ALTER no gatilho de replicação ou usar **sp_settriggerorder** para alterar o gatilho de replicação para o último ou nenhum gatilho, a assinatura não funcionará corretamente.  
  
## <a name="see-also"></a>Consulte Também  
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_settriggerorder &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql.md)  
  
  
