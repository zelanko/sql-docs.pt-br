---
title: Mapeamento de função no Gerenciador de driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- driver manager [ODBC], function mapping
- functions [ODBC], Unicode functions
ms.assetid: ff093b29-671a-4fc0-86c9-08a311a98e54
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db8e525bb7e8f3e167deb8061a4dd5b75073933c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305577"
---
# <a name="function-mapping-in-the-driver-manager"></a>Mapeamento de função no Gerenciador de Driver
O Gerenciador de driver dá suporte a dois pontos de entrada para funções que usam argumentos de cadeia de caracteres. A função não decorada (**SQLDriverConnect**) é a forma ANSI da função. O formulário Unicode é decorado com uma *W* (**SQLDriverConnectW**.)  
  
 O arquivo de cabeçalho ODBC também dá suporte a funções decoradas com um *a,* (**SQLDriverConnectA**) para a conveniência de aplicativos ANSI/Unicode mistos. Chamadas feitas às funções a são, na verdade, chamadas **para o ponto** de entrada não decorado (**SQLDriverConnect**).  
  
 Se o aplicativo for compilado com o _UNICODE **#define**, o arquivo de cabeçalho ODBC mapeará chamadas de função não decoradas (**SQLDriverConnect**) para a versão Unicode (**SQLDriverConnectW**).  
  
 O Gerenciador de driver reconhece um driver como um driver Unicode se **SQLConnectW** tiver suporte do driver.  
  
 Se o driver for um driver Unicode, o Gerenciador de driver fará chamadas de função da seguinte maneira:  
  
-   Passa uma função sem argumentos de cadeia de caracteres ou parâmetros diretamente para o driver.  
  
-   Passa funções Unicode (com o sufixo *W* ) diretamente para o driver.  
  
-   Converte uma função ANSI ( *com o sufixo a)* em uma função Unicode (com o sufixo *W* ) convertendo os argumentos de cadeia de caracteres em caracteres Unicode e passa a função Unicode para o driver.  
  
 Se o driver for um driver ANSI, o Gerenciador de driver fará chamadas de função da seguinte maneira:  
  
-   Passa funções sem argumentos de cadeia de caracteres ou parâmetros diretamente para o driver.  
  
-   Converte funções Unicode (com o sufixo *W* ) em uma chamada de função ANSI e passa-as para o driver.  
  
-   Passa uma função ANSI diretamente para o driver.  
  
 O Gerenciador de driver é habilitado para Unicode internamente. Como resultado, o desempenho ideal é obtido por um aplicativo Unicode que trabalha com um driver Unicode, pois o Gerenciador de driver simplesmente passa as funções Unicode para o driver. Quando um aplicativo ANSI está trabalhando com um driver ANSI, o Gerenciador de driver deve converter cadeias de caracteres de ANSI para Unicode ao processar algumas funções, como **SQLDriverConnect**. Depois de processar a função, o Gerenciador de driver deve converter a cadeia de caracteres Unicode de volta em ANSI antes de enviar a função para o driver ANSI.  
  
 Um aplicativo não deve modificar ou ler seus buffers de parâmetro associados quando o driver retorna SQL_STILL_EXECUTING ou SQL_NEED_DATA. O Gerenciador de driver deixa os buffers ligados ao ANSI até que o driver retorne SQL_SUCCESS, SQL_SUCCESS_WITH_INFO ou SQL_ERROR. Um aplicativo multi-threaded não deve obter acesso a nenhum valor de parâmetro associado ao qual outro thread esteja executando uma instrução SQL. O Gerenciador de driver converte os dados de Unicode para ANSI "em vigor" e o outro thread pode ver dados ANSI nesses buffers enquanto o driver ainda está processando a instrução SQL. Os aplicativos que associam dados Unicode a um driver ANSI não devem associar duas colunas diferentes ao mesmo endereço.
