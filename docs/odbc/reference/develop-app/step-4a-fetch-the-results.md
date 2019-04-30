---
title: 'Etapa 4a: Buscar os resultados | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], fetching results
- fetches [ODBC], fetching results
ms.assetid: 77d30142-c774-473c-96fb-b364bb92ac60
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cad33f1ccf798a08ef1f11667e59b4d5fb4888d8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149206"
---
# <a name="step-4a-fetch-the-results"></a>Etapa 4a: Buscar os resultados
A próxima etapa é buscar os resultados, conforme mostrado na ilustração a seguir.  
  
 ![Mostra a busca de resultados em um aplicativo ODBC](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 Se a instrução é executada em "etapa 3: Compilar e executar uma instrução SQL"foi uma **selecionar** instrução ou uma função de catálogo, o aplicativo primeiro chama **SQLNumResultCols** para determinar o número de colunas no conjunto de resultados. Essa etapa não é necessária se o aplicativo já sabe o número de resultados a definir colunas, como quando a instrução SQL é embutido no código em um aplicativo vertical ou personalizado.  
  
 Em seguida, o aplicativo recupera o nome, tipo de dados, precisão e escala de cada coluna do conjunto de resultados com **SQLDescribeCol**. Novamente, isso não é necessário para aplicativos como aplicativos verticais e personalizados que já conhecer essas informações. O aplicativo passa essas informações para **SQLBindCol**, que associa uma variável de aplicativo a uma coluna no conjunto de resultados.  
  
 O aplicativo agora chama **SQLFetch** para recuperar a primeira linha de dados e inserir os dados do que a linha nas variáveis associadas **SQLBindCol**. Se houver quaisquer dados long na linha, em seguida, chama **SQLGetData** para recuperar dados. O aplicativo continua a chamar **SQLFetch** e **SQLGetData** para recuperar dados adicionais. Após ter concluído ao buscar dados, ele chama **SQLCloseCursor** para fechar o cursor.  
  
 Para obter uma descrição completa de recuperar os resultados, consulte [recuperando resultados (básico)](../../../odbc/reference/develop-app/retrieving-results-basic.md) e [recuperando resultados (Avançado)](../../../odbc/reference/develop-app/retrieving-results-advanced.md).  
  
 Agora o aplicativo retorna para "etapa 3: Compilar e executar uma instrução SQL"para executar outra instrução na mesma transação; ou, prosseguirá para "etapa 5: Confirmar a transação"para confirmar ou reverter a transação.
