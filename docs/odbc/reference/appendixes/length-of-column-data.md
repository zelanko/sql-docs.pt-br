---
title: Comprimento dos dados da coluna | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- length of column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: c762c881-ebe0-4eac-84d5-f30281fc3eca
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e53cd64eaa0afb2ba042190b0649721c65979de7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="length-of-column-data"></a>Comprimento dos dados da coluna
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 A biblioteca de cursores cria um buffer em cache para cada buffer de comprimento/indicador associado ao conjunto de resultados com **SQLBindCol**. Ele usa os valores nesses buffers para construir um **onde** cláusula quando ele emula atualização posicionada ou instruções delete. Ele atualiza esses buffers dos buffers de linhas quando ele busca dados da fonte de dados e quando ele executa instruções update posicionadas.  
  
 Se o tipo C de um buffer de dados é SQL_C_CHAR ou SQL_C_BINARY e o valor de comprimento/indicador é SQL_NTS, o comprimento da cadeia de caracteres dos dados é colocado no buffer de comprimento/indicador.  
  
> [!NOTE]  
>  A biblioteca de cursores não atualiza o cache para uma coluna se **StrLen_or_IndPtr* no conjunto de linhas correspondente buffer é o resultado da macro SQL_LEN_DATA_AT_EXEC ou SQL_DATA_AT_EXEC.
