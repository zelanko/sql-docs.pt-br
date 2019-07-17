---
title: Buffers | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- input buffers [ODBC]
- length/indicator buffers [ODBC]
- output buffers [ODBC]
- buffers [ODBC], about buffers
- application buffers [ODBC]
- buffers [ODBC]
ms.assetid: 42c5226c-cb40-4d1e-809f-2ea50ce6bd55
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ad13379552e3a5a576b0aa5cc8720ca6ca1688a9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118739"
---
# <a name="buffers"></a>Buffers
Um buffer é qualquer parte da memória do aplicativo usada para passar dados entre o aplicativo e o driver. Por exemplo, buffers de aplicativo podem ser associados, ou *vinculados,* colunas com o conjunto de resultados **SQLBindCol**. Como cada linha for encontrada, os dados são retornados para cada coluna nesses buffers. *Buffers de entrada* são usados para transmitir dados do aplicativo para o driver; *buffers de saída* são usados para retornar dados do driver para o aplicativo.  
  
> [!NOTE]  
>  Se uma função ODBC retorna SQL_ERROR, o conteúdo de quaisquer argumentos de saída para essa função é indefinido.  
  
 Esta discussão se preocupa principalmente com buffers tipo indeterminado. Os endereços desses buffers são exibidos como argumentos de tipo SQLPOINTER, como o *TargetValuePtr* argumento **SQLBindCol**. No entanto, alguns dos itens discutidos aqui, como os argumentos usados com buffers, se aplicam também aos argumentos usados para passar cadeias de caracteres para o driver, como o *TableName* argumento **SQLTables**.  
  
 Esses buffers geralmente vêm em pares. *Buffers de dados* são usados para passar os dados em si, enquanto *buffers de comprimento/indicador* são usados para transmitir o comprimento dos dados no buffer de dados ou um valor especial, como SQL_NULL_DATA, que indica que os dados são NULL. O comprimento dos dados em um buffer de dados é diferente do comprimento do buffer de dados em si. A ilustração a seguir mostra a relação entre o buffer de dados e o buffer de comprimento/indicador.  
  
 ![Buffer de dados e comprimento&#47;buffer indicador](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 Um buffer de comprimento/indicador é necessário sempre que o buffer de dados contém dados de comprimento variável, como caractere ou dados binários. Se o buffer de dados contém dados de comprimento fixo, como uma estrutura de inteiro ou uma data, um buffer de comprimento/indicador é necessária apenas para passar valores de indicador, porque o tamanho dos dados já é conhecido. Se um aplicativo usa um buffer de comprimento/indicador com dados de comprimento fixo, o driver ignora qualquer comprimentos passados nele.  
  
 O comprimento do buffer de dados e os dados que ele contém é medido em bytes, em vez de caracteres. Essa distinção é importante para programas que usam cadeias de caracteres ANSI porque o comprimento em bytes e caracteres é iguais.  
  
 Quando o buffer de dados representa um campo de descritor definido pelo driver, o campo de diagnóstico ou o atributo, o aplicativo deve indicar ao Gerenciador de Driver a natureza do argumento de função que indica o valor do campo ou do atributo. O aplicativo faz isso definindo o argumento de comprimento, em qualquer chamada de função que define o campo ou o atributo como um dos valores a seguir. (O mesmo é verdadeiro para as funções que recuperam os valores do campo ou atributo, com exceção de que o argumento aponta para os valores que estão no próprio argumento para a função de configuração.)  
  
-   Se o argumento da função que indica o valor do campo ou do atributo é um ponteiro para uma cadeia de caracteres, o *comprimento* argumento é o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se o argumento da função que indica o valor do campo ou do atributo é um ponteiro para um buffer de binário, o aplicativo coloca o resultado do SQL_LEN_BINARY_ATTR (*comprimento*) macro na *comprimento* argumento. Isso coloca um valor negativo na *comprimento* argumento.  
  
-   Se o argumento da função que indica o valor do campo ou do atributo é um ponteiro para um valor diferente de uma cadeia de caracteres ou uma cadeia de caracteres binária, o *comprimento* argumento deve ter o valor SQL_IS_POINTER.  
  
-   Se o argumento da função que indica o valor do campo ou do atributo contém um valor de comprimento fixo, o *comprimento* argumento é SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT ou SQL_ISI_USMALLINT, conforme apropriado.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Buffers adiados](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [Alocando e liberando buffers](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [Usando buffers de dados](../../../odbc/reference/develop-app/using-data-buffers.md)
