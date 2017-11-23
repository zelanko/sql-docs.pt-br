---
title: "Função de mapeamento no Gerenciador de Driver | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC], functions
- driver manager [ODBC], function mapping
- functions [ODBC], Unicode functions
ms.assetid: ff093b29-671a-4fc0-86c9-08a311a98e54
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 63c908b668e4cecd93cc9930f638ccde9173b563
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="function-mapping-in-the-driver-manager"></a>Mapeamento de função no Gerenciador de Driver
O Gerenciador de driver dá suporte a dois pontos de entrada para as funções que usam argumentos de cadeia de caracteres. A função não decorada (**SQLDriverConnect**) é o formato ANSI da função. O formato Unicode é decorado com um *W* (**SQLDriverConnectW**.)  
  
 O arquivo de cabeçalho ODBC também oferece suporte às funções decoradas com um *A,* (**SQLDriverConnectA**) para a conveniência de aplicativos do ANSI/Unicode mistos. Chamadas feitas para o **um** funções são, na verdade, as chamadas para o ponto de entrada não decorado (**SQLDriverConnect**.)  
  
 Se o aplicativo é compilado com o Unicode **#define**, o arquivo de cabeçalho ODBC mapeará chamadas de função não decorados (**SQLDriverConnect**) para a versão Unicode (**SQLDriverConnectW** .)  
  
 O Gerenciador de Driver reconhece um driver como um driver de Unicode se **SQLConnectW** é suportado pelo driver.  
  
 Se o driver é um driver de Unicode, o Gerenciador de Driver faz chamadas de função da seguinte maneira:  
  
-   Passa uma função sem parâmetros ou argumentos de cadeia de caracteres diretamente por meio do driver.  
  
-   Passa funções Unicode (com o *W* sufixo) diretamente por meio do driver.  
  
-   Converte uma função de ANSI (com o *um* sufixo) para uma função Unicode (com o *W* sufixo) ao converter os argumentos de cadeia de caracteres em Unicode, caracteres e passa a função Unicode para o driver.  
  
 Se o driver é um driver de ANSI, o Gerenciador de Driver faz chamadas de função da seguinte maneira:  
  
-   Passa funções sem argumentos de cadeia de caracteres ou parâmetros diretamente por meio do driver.  
  
-   Converte as funções Unicode (com o *W* sufixo) para ANSI chamada de função e o transmite para o driver.  
  
-   Passa uma função ANSI diretamente para o driver.  
  
 O Gerenciador de Driver está habilitado para Unicode internamente. Como resultado, o desempenho ideal é obtido por um aplicativo Unicode trabalhando com um driver de Unicode, porque o Gerenciador de Driver simplesmente passa funções Unicode por meio do driver. Quando um aplicativo ANSI está funcionando com um driver de ANSI, o Gerenciador de Driver deve converter cadeias de caracteres de ANSI em Unicode durante o processamento de algumas funções, tais como **SQLDriverConnect**. Depois de processar a função, o Gerenciador de Driver deve converter a cadeia de caracteres de Unicode novamente em ANSI antes de enviar a função para o driver de ANSI.  
  
 Um aplicativo não deve modificar ou ler seus buffers de parâmetro associado quando o driver retorna SQL_NEED_DATA ou SQL_STILL_EXECUTING. O Gerenciador de Driver deixa os buffers associados ao ANSI até que o driver retorna SQL_SUCCESS, SQL_SUCCESS_WITH_INFO ou SQL_ERROR. Um aplicativo multithread não deve ter acesso a quaisquer valores de parâmetro associados que outro thread está executando uma instrução SQL no. O Gerenciador de Driver converte os dados de Unicode em ANSI "no local", e o outro thread poderá ver dados ANSI nesses buffers enquanto o driver ainda está processando a instrução SQL. Aplicativos que associam os dados de Unicode para um driver de ANSI não devem associar duas colunas diferentes para o mesmo endereço.
