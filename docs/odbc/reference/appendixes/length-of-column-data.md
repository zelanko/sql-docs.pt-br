---
title: Comprimento dos dados da coluna | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- length of column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: c762c881-ebe0-4eac-84d5-f30281fc3eca
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d0b7ad515661cce4c5b1d407be768cc3da131bb4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304927"
---
# <a name="length-of-column-data"></a>Comprimento dos dados da coluna
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 A biblioteca do cursor cria um buffer no cache para cada buffer de comprimento/indicador vinculado ao conjunto de resultados com **SQLBindCol**. Ele usa os valores nesses buffers para construir uma cláusula **WHERE** quando emula instruções de atualização posicionadas ou exclusão. Ele atualiza esses buffers a partir dos buffers de conjunto de linhas quando ele busca dados da fonte de dados e quando executa instruções de atualização posicionadas.  
  
 Se o tipo C de um buffer de dados for SQL_C_CHAR ou SQL_C_BINARY e o valor do comprimento/indicador for SQL_NTS, o comprimento da seqüência dos dados será colocado no buffer de comprimento/indicador.  
  
> [!NOTE]  
>  A biblioteca do cursor não atualiza seu cache para uma coluna se **StrLen_or_IndPtr* no buffer de conjunto de linhas correspondente for SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC.
