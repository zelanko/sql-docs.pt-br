---
title: Dados da Coluna | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 0425818c-9469-493f-9e3c-fc03d9411c5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ff89566efa65c88325d98422fe17788f27d2c8ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306587"
---
# <a name="column-data"></a>Dados de coluna
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 A biblioteca do cursor cria um buffer no cache para cada buffer de dados vinculado ao conjunto de resultados com **SQLBindCol**. Ele usa os valores nesses buffers para construir uma cláusula **WHERE** quando emula uma atualização posicionada ou exclui a declaração. Ele atualiza esses buffers a partir dos buffers de conjunto de linhas quando ele busca dados da fonte de dados e quando executa instruções de atualização posicionadas.  
  
 Quando a biblioteca do cursor atualiza seu cache a partir dos buffers de conjunto de linhas, ele transfere os dados de acordo com o tipo de dados C especificado no **SQLBindCol**. Por exemplo, se o tipo de dados C de um buffer de conjunto de linhas for SQL_C_SLONG, a biblioteca do cursor transfere quatro bytes de dados; se for SQL_C_CHAR e *BufferLength* é 10, a biblioteca do cursor transfere 10 bytes de dados. A biblioteca do cursor não realiza nenhuma verificação de tipo ou conversões nos dados que transfere.  
  
> [!NOTE]  
>  A biblioteca do cursor não atualiza seu cache para uma coluna se **StrLen_or_IndPtr* no buffer de conjunto de linhas correspondente for SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC.  
  
 Quando ele atualiza uma coluna, uma fonte de dados em branco bloqueia dados de caracteres de comprimento fixo e dados binários de comprimento fixo zero, conforme necessário. Por exemplo, uma fonte de dados armazena "Smith" em uma coluna CHAR(10) como "Smith ". A biblioteca do cursor não faz dados em branco ou de bloco zero nos buffers de conjunto de linhas quando copia esses dados em seu cache após a execução de uma declaração de atualização posicionada. Portanto, se um aplicativo exigir que os valores no cache da biblioteca do cursor estejam acolchoados em branco ou acolchoados em branco, ele deve bloquear ou bloquear os valores nos buffers de conjunto de linhas antes de executar uma declaração de atualização posicionada.
