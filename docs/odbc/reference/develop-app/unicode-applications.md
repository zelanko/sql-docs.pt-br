---
title: Aplicativos Unicode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], compiling as Unicode application
- Unicode [ODBC], functions
- compiling Unicode applications [ODBC]
- functions [ODBC], Unicode functions
ms.assetid: 7986c623-2792-4e77-bfee-c86cbf84f08d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 32b4125d0ecb1f15fab00119a8ef4ed361b6db72
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087745"
---
# <a name="unicode-applications"></a>Aplicativos Unicode
Você pode recompilar um aplicativo como um aplicativo Unicode de uma das duas maneiras:  
  
-   Inclua o **#define** Unicode contido no arquivo de cabeçalho sqlucode. h no aplicativo.  
  
-   Compile o aplicativo com a opção Unicode do compilador. (Essa opção será diferente para compiladores diferentes.)  
  
 Para converter um aplicativo ANSI em um aplicativo Unicode, grave o aplicativo para armazenar e transmitir dados Unicode. Além disso, as chamadas para funções que dão suporte a argumentos SQLPOINTER devem ser convertidas para usar a contagem de bytes.  
  
 Depois que um aplicativo é compilado como um aplicativo Unicode, se o aplicativo chamar uma função de API ODBC (sem um sufixo), o Gerenciador de driver reconhecerá o aplicativo como um aplicativo Unicode e converterá a chamada de função em uma função Unicode (com o sufixo *W* ) se o driver subjacente oferecer suporte a Unicode. Quando um aplicativo ANSI faz uma chamada de função sem um sufixo, o Gerenciador de driver converte-o em ANSI se o driver subjacente oferecer suporte a ANSI. Se o aplicativo e o driver suportarem a mesma codificação de caracteres, o Gerenciador de driver passará as chamadas para o driver (com certas exceções para aplicativos ANSI).  
  
 Um aplicativo pode chamar ambas as funções Unicode (com o sufixo *W* ) e as funções ANSI (com ou sem *um* sufixo). As chamadas de função Unicode e ANSI podem ser misturadas. Se a biblioteca de cursores for usada, no entanto, as chamadas de função Unicode e ANSI não poderão ser misturadas. A biblioteca de cursores é Unicode ou ANSI, não uma mistura.  
  
 Um aplicativo pode ser escrito de modo que possa ser compilado como um aplicativo Unicode ou um aplicativo ANSI. Nesse caso, os tipos de dados de caractere podem ser declarados como SQL_C_TCHAR. Essa é uma macro que insere SQL_C_WCHAR se o aplicativo é compilado como um aplicativo Unicode ou insere SQL_C_CHAR se ele for compilado como um aplicativo ANSI. O programador de aplicativos deve ter cuidado com funções que usam o SQLPOINTER como argumento, pois o tamanho do argumento de comprimento será alterado (para tipos de dados de cadeia de caracteres) dependendo se o aplicativo for ANSI ou Unicode.  
  
 Uma função pode ser chamada de uma das três maneiras: como uma chamada de função somente Unicode (com o sufixo *W* ), como uma chamada de função somente ANSI ( *com o sufixo a)* ou como a função ODBC chamada sem sufixo. Os argumentos para as três formas de uma função são idênticos. Somente as funções com argumentos SQLCHAR \* ou SQLPOINTER que apontam para cadeias de caracteres exigem formulários Unicode e ANSI. Para funções que têm argumentos que podem ser declarados como um tipo de caractere, como **SQLBindCol** ou **SQLGetData** (que não têm formulários Unicode e ANSI), o argumento pode ser declarado como o tipo Unicode, o tipo ANSI ou, no caso de um argumento de tipo C, a SQL_C_TCHAR macro. Para obter mais informações, consulte [dados Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 Um aplicativo pode ser gravado como um aplicativo Unicode, mesmo que não haja drivers Unicode disponíveis para ele funcionar com o. O Gerenciador de driver mapeará funções e tipos de dados Unicode para ANSI. Há algumas restrições para os mapeamentos de Unicode para ANSI que podem ser executadas. A existência de um driver Unicode para o aplicativo Unicode com o qual trabalhar resultará em um melhor desempenho e removerá as restrições inerentes aos mapeamentos de Unicode para ANSI.
