---
title: Dados da coluna | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f4bc57a5a0b500dc8828d5b0e35c2d6023165ac5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019255"
---
# <a name="column-data"></a>Dados de coluna
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 A biblioteca de cursores cria um buffer no cache para cada buffer de dados associado ao conjunto de resultados com **SQLBindCol**. Ele usa os valores nesses buffers para construir uma cláusula **Where** quando emula uma instrução UPDATE ou DELETE posicionada. Ele atualiza esses buffers dos buffers de conjunto de linhas quando busca dados da fonte de dados e quando executa instruções UPDATE posicionadas.  
  
 Quando a biblioteca de cursores atualiza seu cache dos buffers de conjunto de linhas, ele transfere os dados de acordo com o tipo de dados C especificado em **SQLBindCol**. Por exemplo, se o tipo de dados C de um buffer de conjunto de linhas for SQL_C_SLONG, a biblioteca de cursores transferirá quatro bytes de dados; Se for SQL_C_CHAR e *BufferLength* for 10, a biblioteca de cursores transferirá 10 bytes de dados. A biblioteca de cursores não executa nenhuma verificação de tipo ou conversões nos dados transferidos.  
  
> [!NOTE]  
>  A biblioteca de cursores não atualiza seu cache para uma coluna se **StrLen_or_IndPtr* no buffer do conjunto de linhas correspondente for SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC.  
  
 Quando ele atualiza uma coluna, uma fonte de dados tem dados de caractere de comprimento fixo em branco e dados binários com comprimento fixo de zero-Pads, conforme necessário. Por exemplo, uma fonte de dados armazena "Smith" em uma coluna CHAR (10) como "Smith". A biblioteca de cursores não está em branco ou dados de teclado zero nos buffers de conjunto de linhas quando ele copia esses dados para seu cache após a execução de uma instrução UPDATE posicionada. Portanto, se um aplicativo exigir que os valores no cache da biblioteca de cursores sejam preenchidos em branco ou preenchidos com zero, eles deverão ser colocados em branco ou ter um preenchimento zero dos valores nos buffers de conjunto de linhas antes de executar uma instrução UPDATE posicionada.
