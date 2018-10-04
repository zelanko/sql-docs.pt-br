---
title: No Gerenciador de Driver de mapeamento de função | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 40dc214fa7f77dfb81c941095ecd71d3d4bf5a36
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762504"
---
# <a name="function-mapping-in-the-driver-manager"></a>Mapeamento de função no Gerenciador de Driver
O Gerenciador de driver dá suporte a dois pontos de entrada para as funções que usam argumentos de cadeia de caracteres. A função não decorada (**SQLDriverConnect**) é o formato ANSI da função. O formulário de Unicode é decorado com um *W* (**SQLDriverConnectW**.)  
  
 O arquivo de cabeçalho ODBC também dá suporte a funções decoradas com um *A,* (**SQLDriverConnectA**) para a conveniência de aplicativos mistos de Unicode/ANSI. Chamadas feitas para o **um** funções são, na verdade, as chamadas para o ponto de entrada não decorado (**SQLDriverConnect**.)  
  
 Se o aplicativo for compilado com o Unicode **#define**, o arquivo de cabeçalho ODBC mapeará chamadas de função não decorado (**SQLDriverConnect**) para a versão Unicode (**SQLDriverConnectW** .)  
  
 O Gerenciador de Driver reconhece um driver como um driver de Unicode, se **SQLConnectW** tem suporte pelo driver.  
  
 Se o driver é um driver de Unicode, o Gerenciador de Driver faz chamadas de função da seguinte maneira:  
  
-   Passa uma função sem argumentos de cadeia de caracteres ou parâmetros diretamente por meio do driver.  
  
-   Passa funções Unicode (com o *W* sufixo) diretamente por meio do driver.  
  
-   Converte uma função de ANSI (com o *um* sufixo) para uma função Unicode (com o *W* sufixo) por converter os argumentos de cadeia de caracteres em Unicode caracteres e passa a função Unicode para o driver.  
  
 Se o driver é um driver de ANSI, o Gerenciador de Driver faz chamadas de função da seguinte maneira:  
  
-   Passa funções sem argumentos de cadeia de caracteres ou parâmetros diretamente por meio do driver.  
  
-   Converte funções Unicode (com o *W* sufixo) a um ANSI chamada de função e o passa para o driver.  
  
-   Passa uma função de ANSI diretamente para o driver.  
  
 O Gerenciador de Driver está habilitado para Unicode internamente. Como resultado, o desempenho ideal é obtido por um aplicativo Unicode trabalhando com um driver de Unicode, porque o Gerenciador de Driver simplesmente passa funções Unicode por meio do driver. Quando um aplicativo ANSI estiver trabalhando com um driver de ANSI, o Gerenciador de Driver deve converter cadeias de caracteres de ANSI em Unicode durante o processamento de algumas funções, tais como **SQLDriverConnect**. Depois de processar a função, o Gerenciador de Driver deve converter a cadeia de caracteres de Unicode novamente em ANSI antes de enviar a função do driver de ANSI.  
  
 Um aplicativo não deve modificar ou ler seus buffers de parâmetro associados quando o driver retorna SQL_NEED_DATA ou SQL_STILL_EXECUTING. O Gerenciador de Driver deixa os buffers associados a ANSI até que o driver retorna SQL_SUCCESS, SQL_SUCCESS_WITH_INFO ou SQL_ERROR. Um aplicativo multithread não deve ter acesso a quaisquer valores de parâmetro associados que outro thread está executando uma instrução SQL no. O Gerenciador de Driver converte os dados de Unicode para ANSI "in-loco" e o outro thread pode ver dados ANSI nesses buffers enquanto o driver ainda está processando a instrução SQL. Aplicativos que associam dados Unicode para um driver de ANSI não devem vincular duas colunas diferentes para o mesmo endereço.
