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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 40fe9d23f14d4a7af80fe31a418cccf7133b7252
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067424"
---
# <a name="data-buffer-length"></a>Comprimento do buffer de dados
O aplicativo passa o tamanho de bytes do buffer de dados para o driver em um argumento, chamado *BufferLength* ou um nome semelhante. Por exemplo, na chamada a seguir para **SQLBindCol**, o aplicativo especifica o comprimento do buffer *ValuePtr* (**sizeof (***ValuePtr***)**):  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 Um driver sempre retornará o número de bytes, não o número de caracteres, no argumento de comprimento do buffer de qualquer função que tenha um argumento de cadeia de caracteres de saída.  
  
 Comprimentos de buffer de dados são necessários apenas para buffers de saída; o driver os utiliza para evitar a gravação após o final do buffer. No entanto, o driver verifica o comprimento do buffer de dados somente quando o buffer contém dados de comprimento variável, como caracteres ou dados binários. Se o buffer contiver dados de comprimento fixo, como uma estrutura de inteiro ou de data, o driver ignorará o comprimento do buffer de dados e assumirá que o buffer é grande o suficiente para manter os dados; ou seja, ele nunca trunca dados de comprimento fixo. Portanto, é importante que o aplicativo aloque um buffer grande o suficiente para dados de comprimento fixo.  
  
 Quando ocorre um truncamento de cadeias de caracteres de saída que não são de dados (como o nome do cursor retornado para **SQLGetCursorName**), o comprimento retornado no argumento de comprimento do buffer é o comprimento máximo de caracteres possível.  
  
 Comprimentos de buffer de dados não são necessários para buffers de entrada porque o driver não grava nesses buffers.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Usando valores de comprimento/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [Comprimento de dados, comprimento do buffer e truncamento](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [Dados de caractere e cadeias de caracteres C](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
