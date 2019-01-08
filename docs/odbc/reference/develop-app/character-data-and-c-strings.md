---
title: Caracteres de dados e cadeias de caracteres C | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 00daac655f0c435c1ee22239d3d4aafa23065997
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52515886"
---
# <a name="character-data-and-c-strings"></a>Dados de caractere e cadeias de caracteres C
Parâmetros de entrada que se referem aos dados de caractere de comprimento variável (como nomes de colunas, parâmetros dinâmicos e valores de atributo de cadeia de caracteres) têm um parâmetro de comprimento associado. Se o aplicativo terminar de cadeias de caracteres com o caractere nulo, como é normal em C, ele fornece como um argumento seja o comprimento em bytes da cadeia de caracteres (não incluindo o terminador null) ou SQL_NTS (cadeia de caracteres Null-Terminated). Um argumento de comprimento não negativo especifica o comprimento real da cadeia de caracteres associado. O argumento de comprimento pode ser 0 para especificar uma cadeia de caracteres de comprimento zero, o que é diferente de um valor nulo. O valor negativo SQL_NTS direciona o driver para determinar o comprimento da cadeia de caracteres, localizando o caractere nulo de terminação.  
  
 Quando dados de caracteres são retornados do driver para o aplicativo, o driver deve sempre null termine com. Isso dá ao aplicativo a opção de manipular os dados como uma cadeia de caracteres ou uma matriz de caracteres. Se o buffer de aplicativo não for grande o suficiente para retornar todos os dados de caractere, o driver ele truncará o comprimento de bytes do buffer menos o número de bytes necessários para o caractere nulo de terminação, os dados truncados termina em nulo e armazena-o no buffer. Portanto, aplicativos sempre devem alocar espaço extra para o caractere de terminação null em buffers usados para recuperar dados de caractere. Por exemplo, um buffer de bytes de 51 é necessário para recuperar a 50 caracteres de dados.  
  
 Cuidado especial precisa ser tomado pelo aplicativo e o driver ao enviar ou recuperar dados de caracteres longa em partes com **SQLPutData** ou **SQLGetData**. Se os dados são passados como uma série de cadeias de caracteres terminada em nulo, os caracteres de terminação null nessas cadeias de caracteres devem ser retirados antes que os dados podem ser reorganizados.  
  
 Um número de programadores ODBC tem confundido dados de caractere e cadeias de caracteres C. Que isso tenha ocorrido é um artefato de como usar a linguagem C ao definir funções ODBC. Se um driver ODBC ou o aplicativo usa outro idioma - Lembre-se de que o ODBC é independente de linguagem – essa confusão é menos provável de ocorrer.  
  
 Quando cadeias de caracteres C são usadas para armazenar dados de caractere, o caractere de terminação null não é considerado parte dos dados e não é contabilizado como parte de seu tamanho em bytes. Por exemplo, o dados de caracteres "ABC" pode ser mantida como a cadeia de caracteres do C "ABC\0" ou a matriz de caracteres {'A', 'B', 'C''}. O comprimento de bytes dos dados é 3, se ele é tratado como uma cadeia de caracteres ou uma matriz de caracteres.  
  
 Embora os drivers e aplicativos geralmente usam cadeias de caracteres do C (matrizes de caracteres terminada em nulo) para armazenar dados de caractere, não há nenhum requisito para fazer isso. Em C, os dados de caracteres também podem ser tratados como uma matriz de caracteres (sem finalização null) e seu tamanho de byte passado separadamente no buffer de comprimento/indicador.  
  
 Como os dados de caractere podem ser mantidos em uma matriz terminada em nulo não e seu comprimento de byte passado separadamente, é possível inserir caracteres nulos nos dados de caractere. No entanto, nesse caso, o comportamento das funções ODBC é indefinido e é específico do driver se um driver lida com isso corretamente. Assim, aplicativos interoperáveis sempre devem lidar com dados de caracteres que podem conter caracteres nulos inseridos como dados binários.
