---
title: Dados de Caracteres e Cordas C | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- data buffers [ODBC], character data
- buffers [ODBC], C strings
- buffers [ODBC], character data
- character data and buffers [ODBC]
- length of data buffers [ODBC]
- data buffers [ODBC], C strings
- buffers [ODBC], length
- C strings and buffers [ODBC]
ms.assetid: 3a141cb4-229d-4027-9349-615cb2995e36
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7bb25022d4e0c0559f2a8f77b89a4ba26aeba33a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307486"
---
# <a name="character-data-and-c-strings"></a>Dados de caractere e cadeias de caracteres C
Os parâmetros de entrada que se referem a dados de caracteres de comprimento variável (como nomes de colunas, parâmetros dinâmicos e valores de atributos de seqüência) têm um parâmetro de comprimento associado. Se o aplicativo encerrar as seqüências com o caractere nulo, como é típico em C, ele fornece como argumento o comprimento em bytes da string (sem incluir o exterminador nulo) ou SQL_NTS (Sequência anulada por Nula). Um argumento de comprimento não negativo especifica o comprimento real da seqüência associada. O argumento de comprimento pode ser 0 para especificar uma seqüência de comprimento zero, que é distinta de um valor NULL. O valor negativo SQL_NTS orienta o driver a determinar o comprimento da seqüência localizando o caractere de rescisão nula.  
  
 Quando os dados de caracteres são devolvidos do driver para o aplicativo, o motorista deve sempre anular-os. Isso dá ao aplicativo a escolha de lidar com os dados como uma seqüência ou uma matriz de caracteres. Se o buffer de aplicativo não for grande o suficiente para retornar todos os dados de caracteres, o driver truncará-os para o comprimento do byte do buffer menos o número de bytes exigidos pelo caractere de rescisão nula, anular os dados truncados e os armazena no buffer. Portanto, os aplicativos devem sempre alocar espaço extra para o caractere de rescisão nula em buffers usados para recuperar dados de caracteres. Por exemplo, um buffer de 51 bytes é necessário para recuperar 50 caracteres de dados.  
  
 Deve-se ter cuidado especial tanto pelo aplicativo quanto pelo driver ao enviar ou recuperar dados de caracteres longos em partes com **SQLPutData** ou **SQLGetData**. Se os dados forem passados como uma série de strings terminadas por nulidade, os caracteres de rescisão nula nessas strings devem ser despidos antes que os dados possam ser remontados.  
  
 Vários programadores oDBC confundiram dados de caracteres e seqüências C. Que isso ocorreu é um artefato de usar a linguagem C ao definir funções ODBC. Se um driver ou aplicativo ODBC usar outra linguagem - lembre-se que o ODBC é independente do idioma - essa confusão é menos provável de surgir.  
  
 Quando as seqüências C são usadas para conter dados de caracteres, o caractere de rescisão nula não é considerado parte dos dados e não é contado como parte de seu comprimento de byte. Por exemplo, os dados de caracteres "ABC" podem ser mantidos como a seqüência C "ABC\0" ou a matriz de caracteres {'A', 'B', 'C'}. O comprimento do byte dos dados é 3, quer seja ou não tratado como uma seqüência ou uma matriz de caracteres.  
  
 Embora aplicativos e drivers geralmente usem strings C (matrizes de caracteres com término nulo) para manter dados de caracteres, não há necessidade de fazer isso. Em C, os dados de caracteres também podem ser tratados como uma matriz de caracteres (sem nulidade) e seu comprimento de byte passou separadamente no buffer comprimento/indicador.  
  
 Como os dados de caracteres podem ser mantidos em uma matriz não-nula e seu comprimento de byte passado separadamente, é possível incorporar caracteres nulos nos dados do caractere. No entanto, o comportamento das funções oDBC neste caso é indefinido e é específico do motorista se um motorista lida com isso corretamente. Assim, os aplicativos interoperáveis devem sempre lidar com dados de caracteres que podem conter caracteres nulos incorporados como dados binários.
