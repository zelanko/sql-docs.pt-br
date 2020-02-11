---
title: Um conjunto de resultados foi criado? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], determining if created
ms.assetid: 4a83b8cb-2d57-4e64-b497-80bd587ee1f9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f748e75f4e1579446b72b519356f2f649889fe0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68078971"
---
# <a name="was-a-result-set-created"></a>Um conjunto de resultados foi criado?
Na maioria das situações, os programadores de aplicativos sabem se as instruções que seu aplicativo executa criarão um conjunto de resultados. Esse é o caso se o aplicativo usar instruções SQL embutidas em código gravadas pelo programador. Normalmente, é o caso quando o aplicativo constrói instruções SQL em tempo de execução: o programador pode facilmente incluir um código que sinalize se uma instrução **Select** ou uma instrução **Insert** está sendo construída. Em algumas situações, o programador não pode, possivelmente, saber se uma instrução criará um conjunto de resultados. Isso será verdadeiro se o aplicativo fornecer uma maneira para o usuário inserir e executar uma instrução SQL. Também é verdadeiro quando o aplicativo constrói uma instrução em tempo de execução para executar um procedimento.  
  
 Nesses casos, o aplicativo chama **SQLNumResultCols** para determinar o número de colunas no conjunto de resultados. Se for 0, a instrução não criou um conjunto de resultados; Se for qualquer outro número, a instrução criará um conjunto de resultados.  
  
 O aplicativo pode chamar **SQLNumResultCols** a qualquer momento depois que a instrução é preparada ou executada. No entanto, como algumas fontes de dados não podem facilmente descrever os conjuntos de resultados que serão criados por instruções preparadas, o desempenho será afetado se **SQLNumResultCols** for chamado depois que uma instrução for preparada, mas antes de ser executada.  
  
 Algumas fontes de dados também dão suporte à determinação do número de linhas que uma instrução SQL retorna em um conjunto de resultados. Para fazer isso, o aplicativo chama **SQLRowCount**. Exatamente o que a contagem de linhas representa é indicado pela configuração da SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 ou opção SQL_STATIC_CURSOR_ATTRIBUTES2 (dependendo do tipo do cursor) retornado por uma chamada para **SQLGetInfo**. Esse bitmask indica para cada tipo de cursor se a contagem de linhas retornada é exata, aproximada ou não está disponível. Se as contagens de linhas para cursores estáticos ou controlados por conjunto de chaves são afetadas por alterações feitas por meio de **SQLBulkOperations** ou **SQLSetPos**, ou por instruções de atualização ou exclusão posicionadas, depende de outros bits retornados pelos mesmos argumentos de opção listados anteriormente. Para obter mais informações, consulte a descrição da função [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .
