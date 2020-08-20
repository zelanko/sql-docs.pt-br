---
description: Buffers
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
ms.openlocfilehash: b1c82927c122197249b02a2d327364e68bd851a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494776"
---
# <a name="buffers"></a>Buffers
Um buffer é qualquer parte da memória do aplicativo usada para passar dados entre o aplicativo e o driver. Por exemplo, os buffers de aplicativo podem ser associados ou *vinculados a* colunas de conjunto de resultados com **SQLBindCol**. À medida que cada linha é buscada, os dados são retornados para cada coluna nesses buffers. Os *buffers de entrada* são usados para passar dados do aplicativo para o driver; os *buffers de saída* são usados para retornar dados do driver para o aplicativo.  
  
> [!NOTE]  
>  Se uma função ODBC retornar SQL_ERROR, o conteúdo de qualquer argumento de saída para essa função será indefinido.  
  
 Essa discussão se refere principalmente a buffers de tipo indeterminado. Os endereços desses buffers aparecem como argumentos do tipo SQLPOINTER, como o argumento *TargetValuePtr* em **SQLBindCol**. No entanto, alguns dos itens discutidos aqui, como os argumentos usados com buffers, também se aplicam aos argumentos usados para passar cadeias de caracteres para o driver, como o argumento *TableName* em **SQLTables**.  
  
 Esses buffers geralmente vêm em pares. Os *buffers de dados* são usados para passar os dados em si, enquanto os *buffers de comprimento/indicador* são usados para passar o comprimento dos dados no buffer de dados ou um valor especial como SQL_NULL_DATA, o que indica que os dados são nulos. O comprimento dos dados em um buffer de dados é diferente do comprimento do buffer de dados em si. A ilustração a seguir mostra a relação entre o buffer de dados e o buffer de comprimento/indicador.  
  
 ![Buffer de dados e comprimento&#47;buffer do indicador](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 Um buffer de comprimento/indicador é necessário sempre que o buffer de dados contém dados de comprimento variável, como caracteres ou dados binários. Se o buffer de dados contiver dados de comprimento fixo, como uma estrutura de inteiro ou de data, um buffer de comprimento/indicador será necessário apenas para passar valores de indicador porque o comprimento dos dados já é conhecido. Se um aplicativo usar um buffer de comprimento/indicador com dados de comprimento fixo, o driver ignorará todos os comprimentos passados.  
  
 O comprimento do buffer de dados e dos dados que ele contém é medido em bytes, em vez de caracteres. Essa distinção não é importante para programas que usam cadeias de caracteres ANSI porque comprimentos em bytes e caracteres são os mesmos.  
  
 Quando o buffer de dados representa um campo de descritor, um campo de diagnóstico ou um atributo definido pelo driver, o aplicativo deve indicar ao Gerenciador de driver a natureza do argumento da função que indica o valor para o campo ou atributo. O aplicativo faz isso definindo o argumento Length em qualquer chamada de função que define o campo ou atributo como um dos valores a seguir. (O mesmo é verdadeiro para funções que recuperam os valores do campo ou atributo, com a exceção de que o argumento aponta para os valores que para a função de configuração estão no próprio argumento.)  
  
-   Se o argumento de função que indica o valor para o campo ou atributo for um ponteiro para uma cadeia de caracteres, o argumento *Length* será o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se o argumento da função que indica o valor do campo ou do atributo for um ponteiro para um buffer binário, o aplicativo colocará o resultado da macro SQL_LEN_BINARY_ATTR (*comprimento*) no argumento de *comprimento* . Isso coloca um valor negativo no argumento *Length* .  
  
-   Se o argumento de função que indica o valor para o campo ou atributo for um ponteiro para um valor diferente de uma cadeia de caracteres ou uma cadeia de caracteres binária, o argumento de *comprimento* deverá ter o valor SQL_IS_POINTER.  
  
-   Se o argumento de função que indica o valor para o campo ou atributo contiver um valor de comprimento fixo, o argumento de *comprimento* será SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT ou SQL_ISI_USMALLINT, conforme apropriado.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Buffers adiados](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [Alocar e liberar buffers](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [Usar buffers de dados](../../../odbc/reference/develop-app/using-data-buffers.md)
