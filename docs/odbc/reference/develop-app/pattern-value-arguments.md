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
ms.openlocfilehash: 53c091fd0b7a6cfdf390997fb5163fbc9d98e18c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68023349"
---
# <a name="pattern-value-arguments"></a>Argumentos de valor de padrão
Alguns argumentos nas funções de catálogo, como o argumento *TableName* em **SQLTables**, aceitam padrões de pesquisa. Esses argumentos aceitam padrões de pesquisa se o atributo de instrução SQL_ATTR_METADATA_ID for definido como SQL_FALSE; Eles são argumentos de identificador que não aceitam um padrão de pesquisa se esse atributo for definido como SQL_TRUE.  
  
 Os caracteres de padrão de pesquisa são:  
  
-   Um sublinhado (_), que representa qualquer caractere único.  
  
-   Um sinal de porcentagem (%), que representa qualquer sequência de zero ou mais caracteres.  
  
-   Um caractere de escape, que é específico do driver e é usado para incluir sublinhados, sinais de porcentagem e o caractere de escape como literais. Se o caractere de escape precede um caractere não especial, o caractere de escape não terá nenhum significado especial. Se o caractere de escape precede um caractere especial, ele escapa o caractere especial. Por exemplo, "\a" seria tratado como dois caracteres, "\\" e "a", mas "\\%" seria tratado como o único caractere não especial "%".  
  
 O caractere de escape é recuperado com a opção SQL_SEARCH_PATTERN_ESCAPE em **SQLGetInfo**. Ele deve preceder qualquer sublinhado, sinal de porcentagem ou caractere de escape em um argumento que aceite padrões de pesquisa para incluir esse caractere como um literal. Os exemplos são mostrados na tabela a seguir.  
  
|Padrão de pesquisa|DESCRIÇÃO|  
|--------------------|-----------------|  
|Um|Todos os identificadores que contêm a letra A|  
|ABC_|Todos os identificadores de quatro caracteres que começam com ABC|  
|ABC\\_|O identificador ABC_, supondo que o caractere de escape é uma\\barra invertida ()|  
|\\\\%|Todos os identificadores que começam com uma barra\\invertida (), supondo que o caractere de escape seja uma barra invertida|  
  
 Deve-se tomar cuidado especial para escapar caracteres padrão de pesquisa em argumentos que aceitam padrões de pesquisa. Isso é particularmente verdadeiro para o caractere de sublinhado, que é comumente usado em identificadores. Um erro comum nos aplicativos é recuperar um valor de uma função de catálogo e passar esse valor para um argumento de padrão de pesquisa em outra função de catálogo. Por exemplo, suponha que um aplicativo recupere o nome da tabela MY_TABLE do conjunto de resultados para **SQLTables** e passe isso para **SQLColumns** para recuperar uma lista de colunas em MY_TABLE. Em vez de obter as colunas para MY_TABLE, o aplicativo receberá as colunas de todas as tabelas que correspondem ao padrão de pesquisa MY_TABLE, como MY_TABLE, MY1TABLE, MY2TABLE e assim por diante.  
  
> [!NOTE]
>  ODBC 2. os drivers *x* não dão suporte a padrões de pesquisa no argumento *CatalogName* em **SQLTables**. Os drivers ODBC 3 *. x* aceitam padrões de pesquisa neste argumento se o atributo ambiente de ODBC_VERSION de SQL_ATTR_ estiver definido como SQL_OV_ODBC3; Eles não aceitam padrões de pesquisa neste argumento se ele estiver definido como SQL_OV_ODBC2.  
  
 A passagem de um ponteiro nulo para um argumento de padrão de pesquisa não restringirá a pesquisa para esse argumento; ou seja, um ponteiro nulo e o padrão de pesquisa% (quaisquer caracteres) são equivalentes. No entanto, um padrão de pesquisa de comprimento zero, ou seja, um ponteiro válido para uma cadeia de caracteres de comprimento zero-corresponde apenas à cadeia de caracteres vazia ("").
