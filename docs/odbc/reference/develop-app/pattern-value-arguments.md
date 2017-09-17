---
title: "Argumentos de valor de padrão | Microsoft Docs"
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
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], pattern value
- pattern value arguments [ODBC]
ms.assetid: 1d3f0ea6-87af-4836-807f-955e7df2b5df
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6935d0e94b931451aba5940db60877c8443df7c4
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="pattern-value-arguments"></a>Argumentos de valor padrão
Alguns argumentos no catálogo de funções, como o *TableName* argumento **SQLTables**, aceite os padrões de pesquisa. Esses argumentos aceitam padrões de pesquisa se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_FALSE; são argumentos de identificador que não aceitam um padrão de pesquisa se esse atributo é definido como SQL_TRUE.  
  
 Os caracteres de pesquisa padrão são:  
  
-   Um caractere de sublinhado (_), que representa qualquer caractere único.  
  
-   Um sinal de porcentagem (%), que representa qualquer sequência de zero ou mais caracteres.  
  
-   Um caractere de escape, que é específico do driver e é usado para incluir um sublinhado, sinais de porcentagem, e o caractere de escape como literais. Se o caractere de escape precede um caractere não especial, o caractere de escape não tem significado especial. Se o caractere de escape precede um caractere especial, ele ignora o caractere especial. Por exemplo, "\a" seria tratada como dois caracteres, "\\" e "a", mas "\\%" seria tratada como o único caractere não especial "%".  
  
 O caractere de escape é recuperado com a opção SQL_SEARCH_PATTERN_ESCAPE na **SQLGetInfo**. Ela deve preceder quaisquer sublinhado, um sinal de porcentagem ou um caractere de escape em um argumento que aceita padrões de pesquisa para incluir esse caractere como um literal. Exemplos são mostrados na tabela a seguir.  
  
|Padrão de pesquisa|Description|  
|--------------------|-----------------|  
|UM % %|Todos os identificadores que contém a letra A|  
|ABC_|Todos os identificadores de quatro caracteres, começando com ABC|  
|ABC\\_|O identificador ABC_, supondo que o caractere de escape é uma barra invertida (\\)|  
|\\\\%|Todos os identificadores, começando com uma barra invertida (\\), supondo que o caractere de escape é uma barra invertida|  
  
 Deve ter especial cuidado como escape de caracteres de padrão de pesquisa em argumentos que aceitam os padrões de pesquisa. Isso é especialmente verdadeiro para o caractere de sublinhado, que é normalmente usado em identificadores. É um erro comum em aplicativos recuperar um valor de uma função de catálogo e passar esse valor para um argumento de padrão de pesquisa em outra função de catálogo. Por exemplo, suponha que um aplicativo recupera o nome da tabela MY_TABLE do resultado definido para **SQLTables** e passa para **SQLColumns** para recuperar uma lista de colunas em MY_TABLE. Em vez de obter as colunas para MY_TABLE, o aplicativo obterá as colunas de todas as tabelas que correspondem ao padrão de pesquisa MY_TABLE, como MY_TABLE, MY1TABLE, MY2TABLE e assim por diante.  
  
> [!NOTE]  
>  ODBC 2. *x* drivers não oferecem suporte a padrões de pesquisa a *CatalogName* argumento **SQLTables**. ODBC 3*. x* drivers aceitam os padrões de pesquisa esse argumento se o atributo de ambiente sql_attr ODBC_VERSION é definido como SQL_OV_ODBC3; não aceitar os padrões de pesquisa esse argumento se ele for definido como SQL_OV_ODBC2.  
  
 Transmitindo um ponteiro nulo para um argumento de padrão de pesquisa não restringe a pesquisa para o argumento; ou seja, um ponteiro nulo e o padrão de pesquisa % (caracteres) são equivalentes. No entanto, um comprimento zero Pesquisar padrão — ou seja, um ponteiro válido para uma cadeia de caracteres de comprimento zero — corresponde apenas a cadeia de caracteres vazia ("").
