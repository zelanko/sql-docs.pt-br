---
title: 'Passo 4a: Buscar os resultados | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c4f810e5c42b54ec871c233ab498936abae610dc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302967"
---
# <a name="step-4a-fetch-the-results"></a>Etapa 4a: Buscar os resultados
O próximo passo é buscar os resultados, como mostra a ilustração a seguir.  
  
 ![Mostra a busca de resultados em um aplicativo ODBC](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 Se a declaração executada em "Etapa 3: Construir e Executar uma Declaração SQL" fosse uma declaração **SELECT** ou uma função de catálogo, o aplicativo primeiro liga para **SQLNumResultCols** para determinar o número de colunas no conjunto de resultados. Essa etapa não é necessária se o aplicativo já souber o número de colunas de conjunto de resultados, como quando a declaração SQL é codificada em um aplicativo vertical ou personalizado.  
  
 Em seguida, o aplicativo recupera o nome, o tipo de dados, a precisão e a escala de cada coluna de conjunto de resultados com **SQLDescribeCol**. Mais uma vez, isso não é necessário para aplicações como aplicações verticais e personalizadas que já conhecem essas informações. O aplicativo passa essas informações para **SQLBindCol**, que vincula uma variável de aplicativo a uma coluna no conjunto de resultados.  
  
 O aplicativo agora chama **o SQLFetch** para recuperar a primeira linha de dados e colocar os dados dessa linha nas variáveis vinculadas ao **SQLBindCol**. Se houver algum dado longo na linha, ele então chama **SQLGetData** para recuperar esses dados. O aplicativo continua a chamar **SQLFetch** e **SQLGetData** para recuperar dados adicionais. Depois de terminar de buscar dados, ele chama **o SQLCloseCursor** para fechar o cursor.  
  
 Para obter uma descrição completa dos resultados de recuperação, consulte [Resultados de recuperação (Básico)](../../../odbc/reference/develop-app/retrieving-results-basic.md) e [Resultados de Recuperação (Avançado)](../../../odbc/reference/develop-app/retrieving-results-advanced.md).  
  
 O aplicativo agora retorna à "Etapa 3: Construir e Executar uma Declaração SQL" para executar outra declaração na mesma transação; ou prossegue para "Passo 5: Comprometa a transação" para cometer ou reverter a transação.
