---
title: Exibir os Eventos Estendidos equivalentes às classes do Rastreamento do SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Trace, extended events equivalents
- extended events [SQL Server], SQL Trace equivalents
- extended events [SQL Server], user configurable events
ms.assetid: 7f24104c-201d-4361-9759-f78a27936011
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c65894f0fa9dd7e710d150a3fbe6512687162cb9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37170747"
---
# <a name="view-the-extended-events-equivalents-to-sql-trace-event-classes"></a>Exibir os Eventos Estendidos equivalentes às classes de evento de Rastreamento do SQL
  Se você desejar usar os Eventos Estendidos para coletar dados de evento equivalentes a colunas e classes de evento do Rastreamento do SQL, será útil entender como os eventos do Rastreamento do SQL são mapeados para os eventos e as ações dos Eventos Estendidos.  
  
 Você pode usar o seguinte procedimento para exibir os eventos e as ações dos Eventos Estendidos que são equivalentes a cada evento do Rastreamento do SQL e suas colunas associadas.  
  
## <a name="to-view-the-extended-events-equivalents-to-sql-trace-events-using-query-editor"></a>Para exibir os equivalentes de Eventos Estendidos a eventos do Rastreamento do SQL usando o Editor de Consulta  
  
-   No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], execute a seguinte consulta:  
  
    ```  
    USE MASTER;  
    GO  
    SELECT DISTINCT  
       tb.trace_event_id,  
       te.name AS 'Event Class',  
       em.package_name AS 'Package',  
       em.xe_event_name AS 'XEvent Name',  
       tb.trace_column_id,  
       tc.name AS 'SQL Trace Column',  
       am.xe_action_name as 'Extended Events action'  
    FROM (sys.trace_events te LEFT OUTER JOIN sys.trace_xe_event_map em  
       ON te.trace_event_id = em.trace_event_id) LEFT OUTER JOIN sys.trace_event_bindings tb  
       ON em.trace_event_id = tb.trace_event_id LEFT OUTER JOIN sys.trace_columns tc  
       ON tb.trace_column_id = tc.trace_column_id LEFT OUTER JOIN sys.trace_xe_action_map am  
       ON tc.trace_column_id = am.trace_column_id  
    ORDER BY te.name, tc.name  
    ```  
  
 Ao exibir os resultados, observe o seguinte:  
  
-   Se todas as colunas retornarem NULL com exceção da coluna Event Class, isso indicará que a classe de evento não foi migrada do Rastreamento do SQL.  
  
-   Se apenas o valor da coluna Extended Events for NULL, isso indicará que qualquer um das seguintes condições é verdadeira:  
  
    -   A coluna Rastreamento do SQL é mapeada para um dos campos de dados associados ao evento de Eventos Estendidos.  
  
        > [!NOTE]  
        >  Cada evento dos Eventos Estendidos tem um conjunto padrão de campos de dados que são incluídos automaticamente no conjunto de resultados.  
  
    -   A coluna de ação não tem um equivalente significativo dos Eventos Estendidos. Um exemplo disso é a coluna EventClass no Rastreamento do SQL. Essa coluna não é necessária nos Eventos Estendidos porque o nome do evento atende ao mesmo objetivo.  
  
-   Para as classes de evento do Rastreamento do SQL configuráveis pelo usuário (UserConfigurable:1 a UserConfigurable:9), os Eventos Estendidos usam um único evento para substituí-las. O evento é chamado user_event. Este evento é gerado por meio de sp_trace_generateevent, o mesmo procedimento armazenado usado pelo Rastreamento do SQL. O evento user_event é retornado, independentemente de qual ID de evento é passada para o procedimento armazenado. No entanto, um campo event_id é retornado como parte dos dados do evento. Isso permite a você criar um predicado baseado na ID do evento. Por exemplo, se você usar UserConfigurable:0 (ID de evento = 82) no código, poderá adicionar o evento user_event à sessão e especificar o predicado “event_id = 82”. Portanto, você não precisa alterar o código, pois o procedimento armazenado sp_trace_generateevent gera o evento user_event dos Eventos Estendidos, e a classe de evento equivalente do Rastreamento do SQL.  
  
-   Se todas as colunas retornarem NULL com exceção da coluna Event Class, isso indicará que a classe de evento não foi migrada do Rastreamento do SQL.  
  
-   Se apenas o valor da coluna Extended Events for NULL, isso indicará que qualquer um das seguintes condições é verdadeira:  
  
    -   A coluna Rastreamento do SQL é mapeada para um dos campos de dados associados ao evento de Eventos Estendidos.  
  
        > [!NOTE]  
        >  Cada evento dos Eventos Estendidos tem um conjunto padrão de campos de dados que são incluídos automaticamente no conjunto de resultados.  
  
    -   A coluna de ação não tem um equivalente significativo dos Eventos Estendidos. Um exemplo disso é a coluna EventClass no Rastreamento do SQL. Essa coluna não é necessária nos Eventos Estendidos porque o nome do evento atende ao mesmo objetivo.  
  
-   Para as classes de evento do Rastreamento do SQL configuráveis pelo usuário (UserConfigurable:1 a UserConfigurable:9), os Eventos Estendidos usam um único evento para substituí-las. O evento é chamado user_event. Este evento é gerado por meio de sp_trace_generateevent, o mesmo procedimento armazenado usado pelo Rastreamento do SQL. O evento user_event é retornado, independentemente de qual ID de evento é passada para o procedimento armazenado. No entanto, um campo event_id é retornado como parte dos dados do evento. Isso permite a você criar um predicado baseado na ID do evento. Por exemplo, se você usar UserConfigurable:0 (ID de evento = 82) no código, poderá adicionar o evento user_event à sessão e especificar o predicado “event_id = 82”. Portanto, você não precisa alterar o código, pois o procedimento armazenado sp_trace_generateevent gera o evento user_event dos Eventos Estendidos, e a classe de evento equivalente do Rastreamento do SQL.  
  
## <a name="see-also"></a>Consulte também  
 [sp_trace_generateevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql)  
  
  
