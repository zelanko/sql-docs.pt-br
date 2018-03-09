---
title: Foi um conjunto criado de resultados? | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: result sets [ODBC], determining if created
ms.assetid: 4a83b8cb-2d57-4e64-b497-80bd587ee1f9
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a7222a9dcbbf7c979dd46ff554fab5988bcfada4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="was-a-result-set-created"></a>Foi um conjunto criado de resultados?
Na maioria das situações, os programadores de aplicativos saber se as instruções que executa o aplicativo criará um conjunto de resultados. Esse é o caso se o aplicativo usa instruções SQL embutidas gravadas pelo programador. Geralmente é o caso quando o aplicativo construa instruções SQL em tempo de execução: O programador facilmente pode incluir o código que indica se um **selecione** instrução ou um **inserir** instrução está sendo construído. Em algumas situações, o programador não é possível saber se uma instrução criará um conjunto de resultados. Isso é verdadeiro se o aplicativo fornece uma maneira para que o usuário insira e executar uma instrução SQL. Ele também é verdadeiro quando o aplicativo cria uma instrução em tempo de execução para executar um procedimento.  
  
 Nesses casos, o aplicativo chama **SQLNumResultCols** para determinar o número de colunas no conjunto de resultados. Se isso for 0, a instrução não criou um conjunto de resultados; Se for qualquer outro número, a instrução criar um conjunto de resultados.  
  
 O aplicativo pode chamar **SQLNumResultCols** a qualquer momento após a instrução estiver preparada ou executada. No entanto, pois algumas fontes de dados não podem descrever facilmente os conjuntos de resultados que serão criados por instruções preparadas, desempenho será afetado se **SQLNumResultCols** é chamado depois que uma instrução é preparada, mas antes de ser executado.  
  
 Algumas fontes de dados também dão suporte a determinar o número de linhas que uma instrução SQL retorna um conjunto de resultados. Para fazer isso, o aplicativo chama **SQLRowCount**. Exatamente o que a contagem de linhas representa é indicada pela configuração da opção SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 ou SQL_STATIC_CURSOR_ATTRIBUTES2 (dependendo do tipo de cursor) retornado por uma chamada para **SQLGetInfo**. Esse bitmask indica para cada tipo de cursor se a contagem de linhas retornada é exato, aproximado, ou não está disponível em todos os. Se contagens de linhas para estática ou cursores controlados por conjuntos de chaves são afetados pelas alterações feitas por meio de **SQLBulkOperations** ou **SQLSetPos**, ou por atualização posicionada ou instruções delete, depende de outros bits retornou os mesmos argumentos de opção listados anteriormente. Para obter mais informações, consulte o [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função.
