---
title: Dados de caractere e C cadeias de caracteres | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ed99ab72e3d5112588a0b1c93df34b01aff7acdd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68044923"
---
# <a name="character-data-and-c-strings"></a>Dados de caractere e cadeias de caracteres C
Os parâmetros de entrada que se referem a dados de caracteres de comprimento variável (como nomes de colunas, parâmetros dinâmicos e valores de atributo de cadeia de caracteres) têm um parâmetro de comprimento associado. Se o aplicativo finalizar cadeias de caracteres com o caractere nulo, como é típico em C, ele fornece como um argumento o comprimento em bytes da cadeia de caracteres (não incluindo o terminador nulo) ou SQL_NTS (cadeia de caracteres terminada em nulo). Um argumento de comprimento não negativo especifica o comprimento real da cadeia de caracteres associada. O argumento de comprimento pode ser 0 para especificar uma cadeia de caracteres de comprimento zero, que é distinta de um valor nulo. O valor negativo SQL_NTS direciona o driver para determinar o comprimento da cadeia de caracteres localizando o caractere de terminação nula.  
  
 Quando os dados de caractere são retornados do driver para o aplicativo, o driver sempre deve terminar de ser nulo. Isso dá ao aplicativo a opção de lidar com a possibilidade de tratar os dados como uma cadeia de caracteres ou uma matriz de caracteres. Se o buffer do aplicativo não for grande o suficiente para retornar todos os dados de caractere, o driver o truncará para o comprimento de bytes do buffer menos o número de bytes exigido pelo caractere de terminação nula, nulo – finaliza os dados truncados e os armazena no completo. Portanto, os aplicativos sempre devem alocar espaço extra para o caractere de terminação nula nos buffers usados para recuperar dados de caractere. Por exemplo, um buffer de 51 bytes é necessário para recuperar 50 caracteres de dados.  
  
 O cuidado especial deve ser feito tanto pelo aplicativo quanto pelo driver ao enviar ou recuperar dados de caractere longo em partes com **SQLPutData** ou **SQLGetData**. Se os dados forem transmitidos como uma série de cadeias de caracteres terminadas em nulo, eles deverão ser removidos antes que os dados possam ser remontados.  
  
 Vários programadores ODBC confundem os dados de caractere e as cadeias de caracteres C. Isso ocorreu é um artefato de uso da linguagem C ao definir funções ODBC. Se um driver ou aplicativo ODBC usar outra linguagem, lembre-se de que o ODBC é independente de linguagem – essa confusão tem menos probabilidade de surgir.  
  
 Quando as cadeias de caracteres C são usadas para armazenar dados de caractere, o caractere de terminação nula não é considerado como parte dos dados e não é contado como parte de seu comprimento de byte. Por exemplo, os dados de caractere "ABC" podem ser mantidos como a cadeia de caracteres C "ABC\0" ou a matriz de caracteres {"A", "B", "C"}. O comprimento de bytes dos dados é 3, seja ou não tratado como uma cadeia de caracteres ou uma matriz de caracteres.  
  
 Embora aplicativos e drivers normalmente usem cadeias de caracteres C (matrizes com terminação nula de personagens) para conter dados de caractere, não há nenhum requisito para fazer isso. Em C, os dados de caractere também podem ser tratados como uma matriz de caracteres (sem terminação nula) e seu comprimento de byte é passado separadamente no buffer de comprimento/indicador.  
  
 Como os dados de caractere podem ser mantidos em uma matriz não terminada em nulo e seu comprimento de byte é passado separadamente, é possível inserir caracteres nulos nos dados de caractere. No entanto, o comportamento de funções ODBC, nesse caso, é indefinido e é específico do driver, independentemente de o driver lidar corretamente. Portanto, os aplicativos interoperáveis sempre devem manipular dados de caracteres que podem conter caracteres nulos inseridos como dados binários.
