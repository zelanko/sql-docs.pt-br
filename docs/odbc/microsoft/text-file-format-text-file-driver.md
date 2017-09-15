---
title: Formato de arquivo de texto (Driver de arquivo de texto) | Microsoft Docs
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
- delimited text lines
- fixed-width text files
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: f53cd4b5-0721-4562-a90f-4c55e6030cb9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eb3505a7750bf2b538078139cf84b9e88a7e23bd
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="text-file-format-text-file-driver"></a>Formato de arquivo de texto (Driver de arquivo de texto)
O driver ODBC texto dá suporte a ambos os arquivos de texto delimitados e de largura fixa. Um arquivo de texto consiste em uma linha de cabeçalho opcionais e zero ou mais linhas de texto.  
  
 Embora a linha de cabeçalho usa o mesmo formato que as outras linhas no arquivo de texto, o driver ODBC texto interpreta as entradas de linha de cabeçalho como nomes de coluna, não dados.  
  
 Uma linha de texto delimitado contém um ou mais valores de dados separados por delimitadores: vírgulas, tabulações ou um delimitador personalizado. Mesmo delimitador deve ser usado em todo o arquivo. Valores de dados nulos são indicados pelos dois delimitadores em uma linha sem dados entre eles. Cadeias de caracteres em uma linha de texto delimitado que podem ser colocadas entre aspas duplas (""). Nenhum espaço em branco pode ocorrer antes ou depois de valores delimitados.  
  
 A largura de cada entrada de dados em uma linha de texto de largura fixa é especificada em um esquema. Valores de dados nulos são indicados por espaços em branco.  
  
 As tabelas estão limitadas a um máximo de 255 campos. Nomes de campo são limitados a 64 caracteres e larguras de campo são limitadas a 32.766 caracteres. Registros são limitados a 65.000 bytes.  
  
 Um arquivo de texto pode ser aberto somente para um único usuário. Não há suporte para vários usuários.  
  
 Gramática a seguir, escrita para programadores, define o formato de um arquivo de texto que possa ser lido pelo driver ODBC texto:  
  
|Formato|Representação|  
|------------|--------------------|  
|Não itálico|Caracteres que devem ser inseridos, conforme mostrado|  
|*itálico*|Argumentos que são definidos em outro lugar na gramática|  
|colchetes ([])|Itens opcionais|  
|chaves ({})|Uma lista de opções mutuamente exclusivas|  
|barras verticais (&#124;)|Opções mutuamente exclusivas separadas|  
|reticências (...)|Itens que podem ser repetidos uma ou mais vezes|  
  
 O formato de arquivo de texto é:  
  
```  
text-file ::=  
   [delimited-header-line] [delimited-text-line]... end-of-file |  
   [fixed-width-header-line] [fixed-width-text-line]... end-of-file  
delimited-header-line ::= delimited-text-line  
delimited-text-line ::=  
   blank-line |  
   delimited-data [delimiter delimited-data]... end-of-line  
fixed-width-header-line ::= fixed-width-text-line  
fixed-width-text-line ::=  
   blank-line |  
   fixed-width-data [fixed-width-data]... end-of-line  
end-of-file ::= <EOF>  
blank-line ::= end-of-line  
delimited-data ::= delimited-string | number | date | delimited-null  
fixed-width-data ::= fixed-width-string | number | date | fixed-width-null  
```  
  
> [!NOTE]  
>  A largura de cada coluna em um arquivo de texto de largura fixa é especificada no arquivo Schema.ini.  
  
```  
  
      end-of-line ::= <CR> | <LF> | <CR><LF>  
delimited-string ::= unquoted-string | quoted-stringunquoted-string ::= [character | digit] [character | digit | quote-character]...  
quoted-string ::=  
   quote-character  
   [character | digit | delimiter | end-of-line | embedded-quoted-string]...  
   quote-characterembedded-quoted-string ::=   quote-characterquote-character  
   [character | digit | delimiter | end-of-line]  
   quote-characterquote-characterfixed-width-string ::= [character | digit | delimiter | quote-character] ...  
character ::= any character except:  
   delimiterdigitend-of-fileend-of-linequote-characterdigit ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9  
delimiter ::= , | <TAB> |   
custom-delimitercustom-delimiter ::= any character except:  
   end-of-fileend-of-linequote-character  
```  
  
> [!NOTE]  
>  O delimitador em um arquivo de texto delimitado por personalizado é especificado no arquivo Schema.ini.  
  
```  
quote-character ::= "  
number ::= exact-number | approximate-number  
exact-number ::= [+ | -] {unsigned-integer[.unsigned-integer] |  
   unsigned-integer. |  
   .unsigned-integer}  
approximate-number ::= exact-number{e | E}[+ | -]unsigned-integer  
unsigned-integer ::= {digit}...  
date ::=  
   mm date-separator dd date-separator yy |  
   mmm date-separator dd date-separator yy |  
   dd date-separator mmm date-separator yy |  
   yyyy date-separator mm date-separator dd |  
   yyyy date-separator mmm date-separator dd  
mm ::= digit [digit]  
dd ::= digit [digit]  
yy ::= digit digit  
yyyy ::= digit digit digit digit  
mmm ::= Jan | Feb | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov | Dec  
date-separator ::= - | / | .  
delimited-null ::=  
```  
  
> [!NOTE]  
>  Para arquivos delimitados, um valor nulo é representado por nenhum dado entre dois delimitadores.  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  Para arquivos de largura fixa, um valor nulo é representado por espaços.
