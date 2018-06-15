---
title: Aplicativos Unicode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], compiling as Unicode application
- Unicode [ODBC], functions
- compiling Unicode applications [ODBC]
- functions [ODBC], Unicode functions
ms.assetid: 7986c623-2792-4e77-bfee-c86cbf84f08d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5ff0858bbfe88ecc9f49306af2426d88a1db072f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32916191"
---
# <a name="unicode-applications"></a>Aplicativos de Unicode
Você pode recompilar um aplicativo como um aplicativo de Unicode em uma das duas maneiras:  
  
-   Incluir o Unicode **#define** contidos no arquivo de cabeçalho sqlucode no aplicativo.  
  
-   Compile o aplicativo com a opção de Unicode do compilador. (Essa opção será diferente para diferentes compiladores.)  
  
 Para converter um aplicativo de ANSI em um aplicativo de Unicode, grave o aplicativo para armazenar e transmitir dados Unicode. Além disso, chamadas para funções que oferecem suporte a argumentos SQLPOINTER devem ser convertidas para usar a contagem de bytes.  
  
 Depois que um aplicativo é compilado como um aplicativo de Unicode, se o aplicativo chama uma função de API de ODBC (sem um sufixo), o Gerenciador de Driver reconhece o aplicativo como um aplicativo Unicode e converte a chamada de função para uma função Unicode (com o  *W* sufixo) se o driver subjacente oferece suporte a Unicode. Quando um aplicativo ANSI faz com que uma função chamada sem um sufixo, o Gerenciador de Driver o converte em ANSI se o driver subjacente oferece suporte ao ANSI. Se o aplicativo e o driver oferecer suporte a mesma codificação de caractere, o Gerenciador de driver passa as chamadas para o driver (com exceções para aplicativos ANSI).  
  
 Um aplicativo pode chamar ambas as funções Unicode (com o *W* sufixo) e funções de ANSI (com ou sem o *um* sufixo). Podem ser misturadas a chamadas de função ANSI e Unicode. Se a biblioteca de cursores é usada, no entanto, as chamadas de função ANSI e Unicode não podem ser misturadas. A biblioteca de cursores é Unicode ou ANSI, não uma combinação.  
  
 Um aplicativo pode ser gravado, de modo que ele pode ser compilado como um aplicativo Unicode ou um aplicativo de ANSI. Nesse caso, os tipos de dados de caractere podem ser declarados como SQL_C_TCHAR. Isso é uma macro que insere SQL_C_WCHAR se o aplicativo é compilado como um aplicativo Unicode ou insere SQL_C_CHAR se ele é compilado como um aplicativo de ANSI. O programador de aplicativo deve ter cuidado de funções que usam SQLPOINTER como seu argumento, porque o tamanho do argumento de comprimento será alterado (para tipos de dados de cadeia de caracteres) dependendo se o aplicativo é ANSI ou Unicode.  
  
 Uma função pode ser chamada em uma das três maneiras: como uma chamada de função somente Unicode (com o *W* sufixo), como uma chamada de função somente ANSI (com o *um* sufixo), ou como a chamada de função ODBC com nenhum sufixo. Os argumentos para as três formas de uma função são idênticos. Apenas as funções com SQLCHAR \* argumentos ou argumentos SQLPOINTER que apontam para cadeias de caracteres requerem formas de ANSI e Unicode. Para funções com argumentos que podem ser declarados como um tipo de caractere, como **SQLBindCol** ou **SQLGetData** (que não possuem formulários ANSI e Unicode), o argumento pode ser declarado como o tipo de Unicode o ANSI de tipo ou, no caso de um C tipo de argumento, a macro SQL_C_TCHAR. Para obter mais informações, consulte [dados Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 Um aplicativo pode ser escrito como um aplicativo de Unicode, mesmo se nenhum driver de Unicode está disponível para trabalhar com. O Gerenciador de Driver mapeará os tipos de funções e os dados Unicode em ANSI. Há algumas restrições para o Unicode para mapeamentos de ANSI que podem ser executadas. A existência de um driver de Unicode para o aplicativo de Unicode para trabalhar com resultará em um melhor desempenho e removerá as restrições inerentes o Unicode para mapeamentos de ANSI.
