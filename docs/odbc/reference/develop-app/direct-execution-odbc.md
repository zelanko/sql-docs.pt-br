---
title: Execução direta ODBC | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305157"
---
# <a name="direct-execution-odbc"></a>Execução direta ODBC
A execução direta é a maneira mais simples de executar uma instrução. Quando a instrução é enviada para execução, a fonte de dados a compila em um plano de acesso e, em seguida, executa esse plano de acesso.  
  
 A execução direta é normalmente usada por aplicativos genéricos que criam e executam instruções em tempo de execução. Por exemplo, o código a seguir cria uma instrução SQL e a executa uma única vez:  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 A execução direta funciona melhor para instruções que serão executadas uma única vez. Sua grande desvantagem é que a instrução SQL é analisada toda vez que é executada. Além disso, o aplicativo não pode recuperar informações sobre o conjunto de resultados criado pela instrução (se houver) até que a instrução seja executada; Isso é possível se a instrução for preparada e executada em duas etapas separadas.  
  
 Para executar uma instrução diretamente, o aplicativo executa as seguintes ações:  
  
1.  Define os valores de qualquer parâmetro. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md), mais adiante nesta seção.  
  
2.  Chama **SQLExecDirect** e passa uma cadeia de caracteres que contém a instrução SQL.  
  
3.  Quando **SQLExecDirect** é chamado, o driver:  
  
    -   Modifica a instrução SQL para usar a gramática SQL da fonte de dados sem analisar a instrução; Isso inclui substituir as sequências de escape abordadas em [sequências de escape no ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md). O aplicativo pode recuperar a forma modificada de uma instrução SQL chamando **SQLNativeSql**. As sequências de escape não serão substituídas se o atributo da instrução SQL_ATTR_NOSCAN for definido.  
  
    -   Recupera os valores de parâmetro atuais e os converte conforme necessário. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md), mais adiante nesta seção.  
  
    -   Envia a instrução e os valores de parâmetro convertidos para a fonte de dados para execução.  
  
    -   Retorna quaisquer erros. Isso inclui o controle de sequenciamento ou de estado como SQLSTATE 24000 (estado de cursor inválido), erros sintáticos como SQLSTATE 42000 (erro de sintaxe ou violação de acesso) e erros semânticos como SQLSTATE 42S02 (tabela base ou exibição não encontrada).
