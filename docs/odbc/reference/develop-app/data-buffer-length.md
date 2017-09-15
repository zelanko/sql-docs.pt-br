---
title: Comprimento do Buffer de dados | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data buffers [ODBC], length
- buffers [ODBC], data
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 7288d143-f9e5-4f90-9b31-2549df79c109
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 84bacf4e45760b14515d44a9d81f46de4485ee5f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="data-buffer-length"></a>Tamanho do Buffer de dados
O aplicativo passa o comprimento de bytes do buffer de dados para o driver em um argumento nomeado *BufferLength* ou um nome semelhante. Por exemplo, na seguinte chamada para **SQLBindCol**, o aplicativo especifica o comprimento do *ValuePtr* buffer (**sizeof (***ValuePtr***)**):  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 Um driver sempre retornará o número de bytes, não o número de caracteres, o argumento de comprimento de buffer de qualquer função que tem um argumento de cadeia de caracteres de saída.  
  
 Comprimentos de buffer de dados são necessários somente para buffers de saída; o driver usa-las para evitar a gravação após o final do buffer. No entanto, o driver verifica o comprimento do buffer de dados somente quando o buffer contém dados de comprimento variável, como caractere ou dados binários. Se o buffer contém dados de comprimento fixo, como uma estrutura de data ou inteiros, o driver ignora o tamanho do buffer de dados e supõe que o buffer é grande o suficiente para manter os dados; ou seja, ele nunca trunca os dados de comprimento fixo. Portanto, é importante para o aplicativo para alocar um buffer grande o suficiente para dados de comprimento fixo.  
  
 Ocorre quando o truncamento de dados não cadeias de caracteres de saída (como o nome do cursor retornado para **SQLGetCursorName**), o tamanho retornado no argumento de comprimento de buffer é o número máximo de caracteres possíveis.  
  
 Comprimentos de buffer de dados não são necessários para buffers de entrada porque o driver não gravará esses buffers.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Usando valores de comprimento/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [Comprimento de dados, comprimento do buffer e truncamento](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [Dados de caractere e cadeias de caracteres C](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
