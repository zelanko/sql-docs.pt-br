---
title: Caracteres de dados e cadeias de caracteres C | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 54f9d438571b1535d16f5fc3b333e9a9cede42eb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="character-data-and-c-strings"></a>Dados de caractere e cadeias de caracteres C
Parâmetros de entrada que fazem referência aos dados de caractere de comprimento variável (como nomes de colunas, parâmetros dinâmicos e valores de atributo de cadeia de caracteres) tem um parâmetro de comprimento associado. Se o aplicativo terminar de cadeias de caracteres com o caractere nulo, como é normal em C, ele fornece como um argumento o comprimento em bytes da cadeia de caracteres (não incluindo o terminador nulo) ou SQL_NTS (cadeia de caracteres Null-Terminated). Um argumento de comprimento negativo especifica o comprimento real da cadeia de caracteres associada. O argumento de comprimento pode ser 0 para especificar uma cadeia de caracteres de comprimento zero, que é diferente de um valor nulo. O valor negativo SQL_NTS instrui o driver para determinar o comprimento da cadeia de caracteres localizando o caractere null de terminação.  
  
 Quando dados de caracteres são retornados do driver para o aplicativo, o driver deve sempre nulo-encerrá-lo. Isso dá ao aplicativo a opção de manipular os dados como uma cadeia de caracteres ou uma matriz de caracteres. Se o buffer de aplicativo não for grande o suficiente para retornar todos os dados de caractere, o driver trunca no comprimento de bytes do buffer menos o número de bytes necessários para o caractere null de terminação null-Finaliza os dados truncados e armazena no buffer. Portanto, aplicativos sempre devem alocar espaço extra para o caractere null de terminação em buffers usados para recuperar dados de caractere. Por exemplo, um buffer de bytes de 51 é necessário para recuperar a 50 caracteres de dados.  
  
 Deve ter especial cuidado pelo aplicativo e o driver ao enviar ou recuperar dados de caracteres longa em partes com **SQLPutData** ou **SQLGetData**. Se os dados são passados como uma série de cadeias de caracteres terminada em nulo, os caracteres de terminação nula nessas cadeias de caracteres devem ser retirados antes que os dados podem ser reorganizados.  
  
 Um número de programadores ODBC ter confundido dados de caractere e cadeias de caracteres C. Se isso tiver ocorrido é um artefato do uso da linguagem C ao definir funções ODBC. Se um aplicativo ou driver ODBC usa outro idioma, lembre-se de que o ODBC é independente de linguagem — essa confusão tem menos probabilidade de ocorrer.  
  
 Quando cadeias de caracteres C são usadas para armazenar dados de caractere, o caractere null de terminação não é considerado parte dos dados e não é contado como parte de seu tamanho em bytes. Por exemplo, o dados de caracteres "ABC" pode ser mantido como a cadeia de caracteres C "ABC\0" ou a matriz de caracteres {'A', 'B', 'C''}. O comprimento de bytes dos dados é 3, ou não será tratada como uma cadeia de caracteres ou uma matriz de caracteres.  
  
 Embora aplicativos e drivers normalmente usarem cadeias de caracteres C (matrizes de caracteres terminada em nulo) para armazenar dados de caracteres, não há nenhum requisito para fazer isso. Em C, os dados de caracteres também podem ser tratados como uma matriz de caracteres (sem null de terminação) e seu tamanho de byte transmitido separadamente no buffer de comprimento/indicador.  
  
 Como os dados de caractere podem ser mantidos em uma matriz de não-terminada em nulo e seu tamanho de byte transmitido separadamente, é possível inserir caracteres nulos nos dados de caractere. No entanto, nesse caso, o comportamento de funções ODBC é indefinido e é específico do driver se um driver lida com isso corretamente. Dessa forma, aplicativos interoperáveis sempre devem lidar com dados de caracteres que podem conter caracteres nulos inseridos como dados binários.
