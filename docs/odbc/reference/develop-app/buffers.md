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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c49e83e12463665f86f8cc15dc595e6ba2c506f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306281"
---
# <a name="buffers"></a>Buffers
Um buffer é qualquer pedaço de memória de aplicativo usado para passar dados entre o aplicativo e o driver. Por exemplo, buffers de aplicativos podem ser associados ou *vinculados a* colunas de conjunto de resultados com **SQLBindCol**. À medida que cada linha é buscada, os dados são retornados para cada coluna nestes buffers. *Buffers de entrada* são usados para passar dados do aplicativo para o driver; *buffers de saída* são usados para retornar dados do driver para o aplicativo.  
  
> [!NOTE]  
>  Se uma função ODBC retornar SQL_ERROR, o conteúdo de quaisquer argumentos de saída para essa função será indefinido.  
  
 Essa discussão diz respeito principalmente a buffers do tipo indeterminado. Os endereços desses buffers aparecem como argumentos do tipo SQLPOINTER, como o argumento *TargetValuePtr* no **SQLBindCol**. No entanto, alguns dos itens aqui discutidos, como os argumentos usados com buffers, também se aplicam a argumentos usados para passar strings para o driver, como o argumento *TableName* no **SQLTables**.  
  
 Esses buffers geralmente vêm em pares. *Os buffers de dados* são usados para passar os dados em si, enquanto *buffers de comprimento/indicador* são usados para passar o comprimento dos dados no buffer de dados ou um valor especial como SQL_NULL_DATA, o que indica que os dados são NULAS. O comprimento dos dados em um buffer de dados é diferente do comprimento do próprio buffer de dados. A ilustração a seguir mostra a relação entre o buffer de dados e o buffer de comprimento/indicador.  
  
 ![Buffer de dados e buffer indicador de&#47;de comprimento](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 Um buffer de comprimento/indicador é necessário sempre que o buffer de dados contenha dados de comprimento variável, como dados de caracteres ou binários. Se o buffer de dados contiver dados de comprimento fixo, como um inteiro ou uma estrutura de data, um buffer de comprimento/indicador é necessário apenas para passar os valores do indicador porque o comprimento dos dados já é conhecido. Se um aplicativo usar um buffer de comprimento/indicador com dados de comprimento fixo, o driver ignorará todos os comprimentos passados nele.  
  
 O comprimento do buffer de dados e dos dados que ele contém é medido em bytes, em oposição aos caracteres. Essa distinção não é importante para programas que usam strings ANSI porque comprimentos em bytes e caracteres são os mesmos.  
  
 Quando o buffer de dados representa um campo de descritor definido pelo driver, campo de diagnóstico ou atributo, o aplicativo deve indicar ao Gerenciador de driver a natureza do argumento de função que indica o valor para o campo ou atributo. O aplicativo faz isso definindo o argumento de comprimento em qualquer chamada de função que define o campo ou atributo a um dos seguintes valores. (O mesmo vale para funções que recuperam os valores do campo ou atributo, com a exceção de que o argumento aponta para os valores que para a função de configuração estão no próprio argumento.)  
  
-   Se o argumento de função que indica o valor para o campo ou atributo for um ponteiro para uma seqüência de caracteres, o argumento de *comprimento* é o comprimento da seqüência ou SQL_NTS.  
  
-   Se o argumento de função que indica o valor para o campo ou atributo for um ponteiro para um buffer binário, o aplicativo colocará o resultado da macro SQL_LEN_BINARY_ATTR *(comprimento)* no argumento *de comprimento.* Isso coloca um valor negativo no argumento do *comprimento.*  
  
-   Se o argumento de função que indica o valor para o campo ou atributo for um ponteiro para um valor diferente de uma seqüência de caracteres ou de uma seqüência binária, o argumento *de comprimento* deve ter o valor SQL_IS_POINTER.  
  
-   Se o argumento de função que indica o valor para o campo ou atributo contiver um valor de comprimento fixo, o argumento de *comprimento* será SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT ou SQL_ISI_USMALLINT, conforme apropriado.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Buffers adiados](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [Alocar e liberar buffers](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [Usar buffers de dados](../../../odbc/reference/develop-app/using-data-buffers.md)
