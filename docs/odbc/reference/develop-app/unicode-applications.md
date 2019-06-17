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
manager: craigg
ms.openlocfilehash: 7fc9cb98837d206d5279d1f14d4a57ce56782759
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62633376"
---
# <a name="unicode-applications"></a>Aplicativos Unicode
Você pode recompilar um aplicativo como um aplicativo Unicode em uma das duas maneiras:  
  
-   Incluir o Unicode **#define** contido no arquivo de cabeçalho sqlucode no aplicativo.  
  
-   Compile o aplicativo com a opção do compilador Unicode. (Essa opção será diferente para compiladores diferentes.)  
  
 Para converter um aplicativo ANSI para um aplicativo Unicode, escreva o aplicativo para armazenar e transmitir dados de Unicode. Além disso, as chamadas para funções que dão suporte a argumentos SQLPOINTER devem ser convertidas para usar a contagem de bytes.  
  
 Depois que um aplicativo é compilado como um aplicativo Unicode, se o aplicativo chama uma função de API do ODBC (sem um sufixo), o Gerenciador de Driver reconhece o aplicativo como um aplicativo Unicode e converte a chamada de função para uma função Unicode (com o  *W* sufixo) se o driver subjacente dá suporte a Unicode. Quando um aplicativo ANSI faz com que uma função de chamada sem um sufixo, o Gerenciador de Driver converterá em ANSI se o driver subjacente dá suporte ao ANSI. Se o aplicativo e o driver der suporte a mesma codificação de caractere, o Gerenciador de driver passa as chamadas por meio do driver (com certas exceções para aplicativos ANSI).  
  
 Um aplicativo pode chamar a ambas as funções Unicode (com o *W* sufixo) e funções ANSI (com ou sem o *um* sufixo). Chamadas de função ANSI e Unicode podem ser combinadas. Se a biblioteca de cursores deve ser usado, no entanto, as chamadas de função ANSI e Unicode não podem ser misturadas. A biblioteca de cursores é Unicode ou ANSI, não uma mistura.  
  
 Um aplicativo pode ser gravado, de modo que ele pode ser compilado como um aplicativo Unicode ou um aplicativo ANSI. Nesse caso, os tipos de dados de caractere podem ser declarados como SQL_C_TCHAR. Isso é uma macro que insere SQL_C_WCHAR se o aplicativo é compilado como um aplicativo Unicode ou insere SQL_C_CHAR se ele é compilado como um aplicativo ANSI. O programador de aplicativos deve ter cuidado de funções que usam SQLPOINTER como seu argumento, porque o tamanho do argumento de comprimento será alterado (para tipos de dados de cadeia de caracteres), dependendo se o aplicativo é ANSI ou Unicode.  
  
 Uma função pode ser chamada em uma destas três maneiras: como uma chamada de função somente Unicode (com o *W* sufixo), como uma chamada de função somente ANSI (com o *um* sufixo), ou como a chamada de função ODBC sem sufixo. Os argumentos para as três formas de uma função são idênticos. Apenas as funções com SQLCHAR \* argumentos ou argumentos SQLPOINTER que apontam para cadeias de caracteres requerem formas de ANSI e Unicode. Para as funções que têm os argumentos que podem ser declarados como um tipo de caractere, como **SQLBindCol** ou **SQLGetData** (que não possuem formulários ANSI e Unicode), o argumento pode ser declarado como o tipo de Unicode ANSI de tipo ou, no caso de um C tipo de argumento, a macro SQL_C_TCHAR. Para obter mais informações, consulte [dados Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 Um aplicativo pode ser escrito como um aplicativo Unicode, mesmo se nenhum driver Unicode está disponível para que ele funcione com. O Gerenciador de Driver mapeará os tipos de funções e dados Unicode para ANSI. Há algumas restrições para o Unicode para mapeamentos de ANSI que podem ser executadas. A existência de um driver de Unicode para o aplicativo trabalhar com Unicode resultará em um melhor desempenho e removerá as restrições inerentes no Unicode para mapeamentos de ANSI.
