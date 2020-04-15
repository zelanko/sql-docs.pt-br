---
title: Aplicações Unicode | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94bd5211c878904453624adb2acd0fe435ebc812
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298942"
---
# <a name="unicode-applications"></a>Aplicativos Unicode
Você pode recompilar um aplicativo como um aplicativo Unicode de duas maneiras:  
  
-   Inclua o **unicode #define** contido no arquivo de cabeçalho Sqlucode.h no aplicativo.  
  
-   Compile o aplicativo com a opção Unicode do compilador. (Esta opção será diferente para diferentes compiladores.)  
  
 Para converter um aplicativo ANSI em um aplicativo Unicode, escreva o aplicativo para armazenar e passar dados Unicode. Além disso, as chamadas para funções que suportam argumentos SQLPOINTER devem ser convertidas para usar a contagem de bytes.  
  
 Depois que um aplicativo é compilado como um aplicativo Unicode, se o aplicativo chamar uma função DePi ODBC (sem um sufixo), o Driver Manager reconhece o aplicativo como um aplicativo Unicode e converte a chamada de função para uma função Unicode (com o sufixo *W)* se o driver subjacente suportar unicode. Quando um aplicativo ANSI faz uma chamada de função sem um sufixo, o Gerenciador de driver converte-o em ANSI se o driver subjacente suportar ANSI. Se o aplicativo e o motorista suportarem a mesma codificação de caracteres, o gerenciador de driver passa as chamadas para o driver (com certas exceções para aplicativos ANSI).  
  
 Um aplicativo pode chamar as funções Unicode (com o sufixo *W)* e as funções ANSI (com ou sem o sufixo *A).* As chamadas de função Unicode e ANSI podem ser misturadas. No entanto, se a biblioteca do cursor for usada, as chamadas de função Unicode e ANSI não podem ser misturadas. A biblioteca do cursor é Unicode ou ANSI, não uma mistura.  
  
 Um aplicativo pode ser escrito de forma que possa ser compilado como um aplicativo Unicode ou um aplicativo ANSI. Neste caso, os tipos de dados de caracteres podem ser declarados como SQL_C_TCHAR. Esta é uma macro que insere SQL_C_WCHAR se o aplicativo for compilado como um aplicativo Unicode ou inserir SQL_C_CHAR se for compilado como um aplicativo ANSI. O programador de aplicativos deve ter cuidado com as funções que tomam o SQLPOINTER como argumento, porque o tamanho do argumento de comprimento mudará (para tipos de dados de seqüência) dependendo se o aplicativo é ANSI ou Unicode.  
  
 Uma função pode ser chamada de uma das três maneiras: como uma chamada de função somente Unicode (com o sufixo *W),* como uma chamada de função somente ANSI (com o sufixo *A),* ou como a chamada de função ODBC sem sufixo. Os argumentos para as três formas de uma função são idênticos. Apenas essas funções com \* argumentos SQLCHAR ou argumentos SQLPOINTER que apontam para strings exigem formulários Unicode e ANSI. Para funções que possuem argumentos que podem ser declarados como um tipo de caractere, como **SQLBindCol** ou **SQLGetData** (que não possuem formulários Unicode e ANSI), o argumento pode ser declarado como o tipo Unicode, o tipo ANSI ou no caso de um argumento tipo C, a macro SQL_C_TCHAR. Para obter mais informações, consulte [Unicode Data](../../../odbc/reference/develop-app/unicode-data.md).  
  
 Um aplicativo pode ser escrito como um aplicativo Unicode, mesmo que não haja drivers Unicode disponíveis para ele trabalhar. O Gerenciador de driver mapeará funções unicode e tipos de dados para ANSI. Existem algumas restrições aos mapeamentos Unicode para ANSI que podem ser realizadas. A existência de um driver Unicode para o aplicativo Unicode funcionar resultará em melhor desempenho e removerá as restrições inerentes aos mapeamentos Unicode para ANSI.
