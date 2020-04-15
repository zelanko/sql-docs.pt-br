---
title: Mapeamento de funções no Driver Manager | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305577"
---
# <a name="function-mapping-in-the-driver-manager"></a>Mapeamento de função no Gerenciador de Driver
O gerenciador de driver suporta dois pontos de entrada para funções que aceitam argumentos de seqüência. A função não decorada **(SQLDriverConnect)** é a forma ANSI da função. O formulário Unicode é decorado com um *W* (**SQLDriverConnectW**.)  
  
 O arquivo de cabeçalho ODBC também suporta funções decoradas com *a,* (**SQLDriverConnectA**) para a conveniência de aplicativos ANSI/Unicode mistos. Chamadas feitas para as **funções A** são, na verdade, chamadas para o ponto de entrada não decorado **(SQLDriverConnect**.)  
  
 Se o aplicativo for compilado com o _UNICODE **#define,** o arquivo de cabeçalho ODBC mapeará chamadas de função não decoradas **(SQLDriverConnect)** para a versão Unicode **(SQLDriverConnectW**.)  
  
 O Driver Manager reconhece um driver como um driver Unicode se **o SQLConnectW** for suportado pelo driver.  
  
 Se o driver for um driver Unicode, o Driver Manager faz chamadas de função da seguinte forma:  
  
-   Passa uma função sem argumentos de seqüência ou parâmetros diretamente para o driver.  
  
-   Passa funções Unicode (com o sufixo *W)* diretamente para o driver.  
  
-   Converte uma função ANSI (com o sufixo *A)* em uma função Unicode (com o sufixo *W)* convertendo os argumentos de seqüência em caracteres Unicode e passa a função Unicode para o driver.  
  
 Se o driver for um driver ANSI, o Driver Manager faz chamadas de função da seguinte forma:  
  
-   Passa funções sem argumentos de seqüência ou parâmetros diretamente para o driver.  
  
-   Converte funções Unicode (com o sufixo *W)* para uma chamada de função ANSI e passa-a para o driver.  
  
-   Passa uma função ANSI diretamente para o driver.  
  
 O Driver Manager é habilitado para Unicode internamente. Como resultado, o desempenho ideal é obtido por um aplicativo Unicode trabalhando com um driver Unicode, porque o Driver Manager simplesmente passa funções Unicode através do driver. Quando um aplicativo ANSI está trabalhando com um driver ANSI, o Driver Manager deve converter strings do ANSI para o Unicode ao processar algumas funções, como **o SQLDriverConnect**. Após o processamento da função, o Driver Manager deve converter a seqüência unicode de volta ao ANSI antes de enviar a função para o driver ANSI.  
  
 Um aplicativo não deve modificar ou ler seus buffers de parâmetro saqueados quando o driver retorna SQL_STILL_EXECUTING ou SQL_NEED_DATA. O Driver Manager deixa os buffers vinculados ao ANSI até que o motorista retorne SQL_SUCCESS, SQL_SUCCESS_WITH_INFO ou SQL_ERROR. Um aplicativo multithreaded não deve obter acesso a quaisquer valores de parâmetro vinculados que outro segmento está executando uma declaração SQL. O Gerenciador de driver converte os dados do Unicode para o ANSI "no lugar", e o outro segmento pode ver os dados ANSI nesses buffers enquanto o driver ainda está processando a declaração SQL. Os aplicativos que vinculam os dados unicode a um driver ANSI não devem vincular duas colunas diferentes ao mesmo endereço.
