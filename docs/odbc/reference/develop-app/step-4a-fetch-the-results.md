---
title: 'Etapa 4a: os resultados de busca | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- application process [ODBC], fetching results
- fetches [ODBC], fetching results
ms.assetid: 77d30142-c774-473c-96fb-b364bb92ac60
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 96a6142cf8ea34f192d0bef5af4a4de0977551c3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="step-4a-fetch-the-results"></a>Etapa 4a: buscar os resultados
A próxima etapa é obter os resultados, conforme mostrado na ilustração a seguir.  
  
 ![Mostra a busca de resultados em um aplicativo ODBC](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 Se a instrução executada na "Etapa 3: criar e executar uma instrução SQL" foi uma **selecione** instrução ou uma função de catálogo, o aplicativo primeiro chama **SQLNumResultCols** para determinar o número de colunas no conjunto de resultados. Essa etapa não é necessária se o aplicativo já souber o número de resultados no conjunto de colunas, como quando a instrução SQL é codificado em um aplicativo personalizado ou vertical.  
  
 Em seguida, o aplicativo recupera o nome, tipo de dados, precisão e escala de cada coluna do conjunto de resultados com **SQLDescribeCol**. Novamente, isso não é necessário para aplicativos, como aplicativos verticais e personalizados que já conhecer essas informações. O aplicativo passa essas informações para **SQLBindCol**, que associa uma variável de aplicativo a uma coluna no conjunto de resultados.  
  
 O aplicativo agora chama **SQLFetch** para recuperar a primeira linha de dados e inserir os dados da linha nas variáveis associadas **SQLBindCol**. Se não houver nenhum dado de tempo na linha, em seguida, chama **SQLGetData** para recuperar dados. O aplicativo continua a chamar **SQLFetch** e **SQLGetData** para recuperar dados adicionais. Depois de concluir a busca de dados, ele chama **SQLCloseCursor** para fechar o cursor.  
  
 Para obter uma descrição completa de recuperar os resultados, consulte [recuperar resultados (Basic)](../../../odbc/reference/develop-app/retrieving-results-basic.md) e [recuperar resultados (Avançado)](../../../odbc/reference/develop-app/retrieving-results-advanced.md).  
  
 O aplicativo agora retorna a "Etapa 3: criar e executar uma instrução SQL" para executar outra instrução na mesma transação; ou vai para a "Etapa 5: a transação de confirmação" confirmar ou reverter a transação.
