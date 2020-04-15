---
title: Comprimento do buffer de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- buffers [ODBC], data
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 7288d143-f9e5-4f90-9b31-2549df79c109
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d4a4e9a739201d74cfc6c4f7c18e64b91e0fabe4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305257"
---
# <a name="data-buffer-length"></a>Comprimento do buffer de dados
O aplicativo passa o comprimento do byte do buffer de dados para o driver em um argumento, chamado *BufferLength* ou um nome semelhante. Por exemplo, na chamada a seguir para **SQLBindCol,** o aplicativo especifica o comprimento do buffer *ValuePtr* **(sizeof ***(ValuePtr):*****  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 Um driver sempre retornará o número de bytes, não o número de caracteres, no argumento de comprimento de buffer de qualquer função que tenha um argumento de seqüência de caracteres de saída.  
  
 Os comprimentos de buffer de dados são necessários apenas para buffers de saída; o driver usa-os para evitar escrever além do fim do buffer. No entanto, o driver verifica o comprimento do buffer de dados somente quando o buffer contém dados de comprimento variável, como dados de caracteres ou binários. Se o buffer contiver dados de comprimento fixo, como um inteiro ou uma estrutura de data, o driver ignorará o comprimento do buffer de dados e assumirá que o buffer é grande o suficiente para conter os dados; ou seja, nunca trunca dados de comprimento fixo. Por isso, é importante que a aplicação aloque um buffer grande o suficiente para dados de comprimento fixo.  
  
 Quando ocorre uma truncação de strings de saída de não dados (como o nome do cursor retornado para **SQLGetCursorName),** o comprimento retornado no argumento de comprimento de buffer é o comprimento máximo de caractere possível.  
  
 Os comprimentos de buffer de dados não são necessários para buffers de entrada porque o driver não escreve para esses buffers.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Usando valores de comprimento/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [Comprimento de dados, comprimento do buffer e truncamento](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [Dados de caractere e cadeias de caracteres C](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
