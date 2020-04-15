---
title: Execução Direta ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], direct execution
- direct execution [ODBC]
- SQL statements [ODBC], executing
ms.assetid: dd00a535-b136-494f-913b-410838e3de7e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc5d942ac0c2af54168248d8e416ca233b2c69e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305157"
---
# <a name="direct-execution-odbc"></a>Execução direta ODBC
A execução direta é a maneira mais simples de executar uma declaração. Quando a declaração é submetida à execução, a fonte de dados compila-a em um plano de acesso e, em seguida, executa esse plano de acesso.  
  
 A execução direta é comumente usada por aplicativos genéricos que constroem e executam instruções em tempo de execução. Por exemplo, o código a seguir constrói uma declaração SQL e executa-a uma única vez:  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 A execução direta funciona melhor para declarações que serão executadas uma única vez. Sua maior desvantagem é que a declaração SQL é analisado toda vez que é executada. Além disso, o aplicativo não pode recuperar informações sobre o conjunto de resultados criado pela declaração (se houver) até depois que a declaração for executada; isso é possível se a declaração for preparada e executada em duas etapas separadas.  
  
 Para executar uma declaração diretamente, o aplicativo executa as seguintes ações:  
  
1.  Define os valores de quaisquer parâmetros. Para obter mais informações, consulte [Parâmetros de declaração,](../../../odbc/reference/develop-app/statement-parameters.md)mais tarde nesta seção.  
  
2.  Chama **SQLExecDirect** e passa-a uma string contendo a declaração SQL.  
  
3.  Quando **o SQLExecDirect** é chamado, o driver:  
  
    -   Modifica a declaração SQL para usar a gramática SQL da fonte de dados sem analisar a declaração; isso inclui a substituição das seqüências de fuga discutidas em [Seqüências de Fuga no ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md). O aplicativo pode recuperar a forma modificada de uma declaração SQL ligando para **SQLNativeSql**. As seqüências de escape não são substituídas se o atributo de declaração SQL_ATTR_NOSCAN estiver definido.  
  
    -   Recupera os valores atuais do parâmetro e converte-os conforme necessário. Para obter mais informações, consulte [Parâmetros de declaração,](../../../odbc/reference/develop-app/statement-parameters.md)mais tarde nesta seção.  
  
    -   Envia a declaração e os valores dos parâmetros convertidos para a fonte de dados para execução.  
  
    -   Retorna qualquer erro. Estes incluem sequenciamento ou diagnósticos estaduais, como SQLSTATE 24000 (estado cursor inválido), erros sintáticos como SQLSTATE 42000 (erro de sintaxe ou violação de acesso) e erros semânticos como SQLSTATE 42S02 (tabela base ou exibição não encontrada).
