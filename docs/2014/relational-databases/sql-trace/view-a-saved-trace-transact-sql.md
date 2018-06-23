---
title: Exibir um rastreamento salvo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], viewing
- displaying traces
- viewing traces
ms.assetid: 3a95a816-aa89-4d5f-858c-968a9cb3ee87
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7f417eb54eff29631f4a24ebbf48de40937a50c5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008592"
---
# <a name="view-a-saved-trace-transact-sql"></a>Exibir um rastreamento salvo (Transact-SQL)
  Este tópico descreve como usar funções internas para exibir um rastreamento salvo.  
  
### <a name="to-view-a-specific-trace"></a>Exibir um rastreamento específico  
  
1.  Execute **fn_trace_getinfo** especificando a identificação do rastreamento sobre o qual informações são necessárias. Esta função retorna uma tabela que lista o rastreamento, a propriedade de rastreamento e as informações sobre a propriedade.  
  
     Invoque a função deste modo:  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(trace_id)  
    ```  
  
### <a name="to-view-all-existing-traces"></a>Exibir todos os rastreamentos existentes  
  
1.  Execute **fn_trace_getinfo** especificando `0` ou `default`. Esta função retorna uma tabela que lista todos os rastreamentos, suas propriedades e as informações sobre essas propriedades.  
  
     Chame a função como segue:  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(default)  
    ```  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
 Para executar a função interna **fn_trace_getinfo**, o usuário precisa da seguinte permissão:  
  
 ALTER TRACE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql)   
 [Exibir e analisar rastreamentos com o SQL Server Profiler](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)  
  
  
