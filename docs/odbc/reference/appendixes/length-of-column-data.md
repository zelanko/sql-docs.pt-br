---
title: Comprimento dos dados de coluna | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d14fa4303dd1f67a77bf14dcebeeb933ccce9e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188830"
---
# <a name="length-of-column-data"></a>Comprimento dos dados da coluna
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 A biblioteca de cursores cria um buffer em cache para cada buffer de comprimento/indicador associado ao conjunto de resultados com **SQLBindCol**. Ele usa os valores nesses buffers para construir uma **onde** cláusula quando ela emula atualização posicionada ou instruções delete. Ele atualiza esses buffers dos buffers de conjunto de linhas quando ele busca dados da fonte de dados e quando ele executa instruções update posicionadas.  
  
 Se o tipo C de um buffer de dados é SQL_C_CHAR ou SQL_C_BINARY e o valor de comprimento/indicador é SQL_NTS, o comprimento da cadeia de caracteres dos dados é colocado no buffer de comprimento/indicador.  
  
> [!NOTE]  
>  A biblioteca de cursores não atualiza seu cache para uma coluna se **StrLen_or_IndPtr* no conjunto de linhas correspondente buffer é o resultado da macro SQL_LEN_DATA_AT_EXEC ou SQL_DATA_AT_EXEC.
