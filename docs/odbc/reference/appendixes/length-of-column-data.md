---
description: Comprimento dos dados da coluna
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
ms.openlocfilehash: 96194272d6b291da53986330199d9c7972cef8f1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429658"
---
# <a name="length-of-column-data"></a>Comprimento dos dados da coluna
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 A biblioteca de cursores cria um buffer no cache para cada buffer de comprimento/indicador associado ao conjunto de resultados com **SQLBindCol**. Ele usa os valores nesses buffers para construir uma cláusula **Where** quando emula as instruções UPDATE ou DELETE posicionadas. Ele atualiza esses buffers dos buffers de conjunto de linhas quando busca dados da fonte de dados e quando executa instruções UPDATE posicionadas.  
  
 Se o tipo C de um buffer de dados for SQL_C_CHAR ou SQL_C_BINARY e o valor de comprimento/indicador for SQL_NTS, o comprimento da cadeia de caracteres dos dados será colocado no buffer de comprimento/indicador.  
  
> [!NOTE]  
>  A biblioteca de cursores não atualiza seu cache para uma coluna se **StrLen_or_IndPtr* no buffer do conjunto de linhas correspondente for SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC.
