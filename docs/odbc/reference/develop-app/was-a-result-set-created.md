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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c171a154dd16a291c5dbe1dcade8c01ea95fb084
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294544"
---
# <a name="was-a-result-set-created"></a>Um conjunto de resultados foi criado?
Na maioria das situações, os programadores de aplicativos sabem se as declarações executadas pelo aplicativo criarão um conjunto de resultados. Este é o caso se o aplicativo usar instruções SQL codificadas com código rígido escritas pelo programador. Geralmente é o caso quando o aplicativo constrói instruções SQL em tempo de execução: O programador pode facilmente incluir o código que sinaliza se uma instrução **SELECT** ou uma instrução **INSERT** está sendo construída. Em algumas situações, o programador não pode saber se uma declaração criará um conjunto de resultados. Isso é verdade se o aplicativo fornecer uma maneira para o usuário inserir e executar uma declaração SQL. Também é verdade quando o aplicativo constrói uma declaração em tempo de execução para executar um procedimento.  
  
 Nesses casos, o aplicativo chama **SQLNumResultCols** para determinar o número de colunas no conjunto de resultados. Se este for 0, a declaração não criou um conjunto de resultados; se for qualquer outro número, a declaração criou um conjunto de resultados.  
  
 O aplicativo pode chamar **SQLNumResultCols** a qualquer momento após a declaração ser preparada ou executada. No entanto, como algumas fontes de dados não podem descrever facilmente os conjuntos de resultados que serão criados por declarações preparadas, o desempenho sofrerá se **o SQLNumResultCols** for chamado após a preparação de uma declaração, mas antes de ser executada.  
  
 Algumas fontes de dados também suportam determinar o número de linhas que uma declaração SQL retorna em um conjunto de resultados. Para isso, o aplicativo chama **SQLRowCount**. Exatamente o que a contagem de linhas representa é indicado pela configuração do SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 ou SQL_STATIC_CURSOR_ATTRIBUTES2 opção (dependendo do tipo do cursor) retornada por uma chamada para **SQLGetInfo**. Esta máscara de bitindica para cada tipo de cursor se a contagem de linhas retornada é exata, aproximada ou não está disponível. Se a contagem de linhas para cursores estáticos ou orientados por chave são afetadas por alterações feitas através de **SQLBulkOperations** ou **SQLSetPos,** ou por instruções de atualização ou exclusão posicionadas, depende de outros bits retornados pelos mesmos argumentos de opção listados anteriormente. Para obter mais informações, consulte a descrição da função [SQLGetInfo.](../../../odbc/reference/syntax/sqlgetinfo-function.md)
