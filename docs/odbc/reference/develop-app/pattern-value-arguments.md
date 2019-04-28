---
title: Argumentos de valor de padrão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], pattern value
- pattern value arguments [ODBC]
ms.assetid: 1d3f0ea6-87af-4836-807f-955e7df2b5df
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f4a32d9ab637de5b52466cfcb628a57ff6c044b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62861714"
---
# <a name="pattern-value-arguments"></a>Argumentos de valor de padrão
Alguns argumentos no catálogo de funções, como o *TableName* argumento **SQLTables**, aceite os padrões de pesquisa. Esses argumentos aceitam os padrões de pesquisa se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_FALSE; são argumentos de identificador que não aceitam um padrão de pesquisa se esse atributo é definido como SQL_TRUE.  
  
 Os caracteres de padrão de pesquisa são:  
  
-   Um sublinhado (_), que representa qualquer caractere único.  
  
-   Um sinal de porcentagem (%), que representa qualquer sequência de zero ou mais caracteres.  
  
-   Um caractere de escape, que é específica do driver e é usado para incluir sublinhados, sinais de porcentagem, e o caractere de escape como literais. Se o caractere de escape precede um caractere não especial, o caractere de escape não tem significado especial. Se o caractere de escape precede um caractere especial, ele escapa o caractere especial. Por exemplo, "\a" seria tratada como dois caracteres, "\\" e "a", mas "\\%" seria tratada como o único caractere não especial "%".  
  
 O caractere de escape é recuperado com a opção SQL_SEARCH_PATTERN_ESCAPE **SQLGetInfo**. Ele deve preceder a qualquer caractere de sublinhado, um sinal de porcentagem ou um caractere de escape em um argumento que aceita padrões de pesquisa para incluir esse caractere como um literal. Exemplos são mostrados na tabela a seguir.  
  
|Padrão de pesquisa|Descrição|  
|--------------------|-----------------|  
|%A%|Todos os identificadores que contém a letra A|  
|ABC_|Todos os identificadores de quatro caracteres, começando com o ABC|  
|ABC\\_|O identificador de ABC _, supondo que o caractere de escape é uma barra invertida (\\)|  
|\\\\%|Todos os identificadores, começando com uma barra invertida (\\), supondo que o caractere de escape é uma barra invertida|  
  
 Especial deve ter cuidado para escapar o caracteres de padrão de pesquisa em argumentos que aceitam os padrões de pesquisa. Isso é especialmente verdadeiro para o caractere de sublinhado, que é normalmente usado em identificadores. Um erro comum em aplicativos é recuperar um valor de uma função de catálogo e passa esse valor para um argumento de padrão de pesquisa em outra função de catálogo. Por exemplo, suponha que um aplicativo recupera o nome da tabela MY_TABLE do resultado definido para **SQLTables** e passa isso **SQLColumns** para recuperar uma lista de colunas no MY_TABLE. Em vez de obter as colunas para MY_TABLE, o aplicativo obterá as colunas para todas as tabelas que correspondem ao padrão de pesquisa MY_TABLE como MY_TABLE, MY1TABLE, MY2TABLE e assim por diante.  
  
> [!NOTE]
>  ODBC 2. *x* drivers não dão suporte a padrões de pesquisa do *CatalogName* argumento **SQLTables**. 3 de ODBC *. x* drivers aceitam os padrões de pesquisa neste argumento se o atributo de ambiente sql_attr ODBC_VERSION é definido como SQL_OV_ODBC3; eles não aceitarem os padrões de pesquisa neste argumento se ele for definido como SQL_OV_ODBC2.  
  
 Passando um ponteiro nulo para um argumento de padrão de pesquisa não restringe a pesquisa para o argumento; ou seja, um ponteiro nulo e o padrão de pesquisa % (caracteres) são equivalentes. No entanto, um padrão de pesquisa de comprimento zero - ou seja, um ponteiro válido para uma cadeia de caracteres de comprimento zero - corresponde apenas a cadeia de caracteres vazia ("").
