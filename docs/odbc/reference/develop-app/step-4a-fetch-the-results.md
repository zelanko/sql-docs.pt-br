---
title: 'Etapa 4a: buscar os resultados | Microsoft Docs'
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
ms.openlocfilehash: 3ab0bdabe8b2d66bf054f07ea51056a4044b4ae8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114192"
---
# <a name="step-4a-fetch-the-results"></a>Etapa 4a: Buscar os resultados
A próxima etapa é buscar os resultados, conforme mostrado na ilustração a seguir.  
  
 ![Mostra a busca de resultados em um aplicativo ODBC](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 Se a instrução executada na "etapa 3: criar e executar uma instrução SQL" for uma instrução **Select** ou uma função de catálogo, o aplicativo primeiro chamará **SQLNumResultCols** para determinar o número de colunas no conjunto de resultados. Essa etapa não será necessária se o aplicativo já souber o número de colunas do conjunto de resultados, como quando a instrução SQL é embutida em código em um aplicativo vertical ou personalizado.  
  
 Em seguida, o aplicativo recupera o nome, o tipo de dados, a precisão e a escala de cada coluna do conjunto de resultados com **SQLDescribeCol**. Novamente, isso não é necessário para aplicativos como aplicativos verticais e personalizados que já conhecem essas informações. O aplicativo passa essas informações para **SQLBindCol**, que associa uma variável de aplicativo a uma coluna no conjunto de resultados.  
  
 Agora, o aplicativo chama **SQLFetch** para recuperar a primeira linha de dados e coloca os dados dessa linha nas variáveis associadas a **SQLBindCol**. Se houver dados longos na linha, ele chamará **SQLGetData** para recuperar esses dados. O aplicativo continua a chamar **SQLFetch** e **SQLGetData** para recuperar dados adicionais. Depois de concluir a busca de dados, ele chama **SQLCloseCursor** para fechar o cursor.  
  
 Para obter uma descrição completa da recuperação de resultados, consulte [recuperando resultados (básico)](../../../odbc/reference/develop-app/retrieving-results-basic.md) e [recuperando resultados (avançado)](../../../odbc/reference/develop-app/retrieving-results-advanced.md).  
  
 O aplicativo agora retorna para a "etapa 3: criar e executar uma instrução SQL" para executar outra instrução na mesma transação; ou prossegue para a "etapa 5: confirmar a transação" para confirmar ou reverter a transação.
