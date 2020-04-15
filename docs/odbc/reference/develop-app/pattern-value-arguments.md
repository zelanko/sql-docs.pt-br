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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0b8e7b7de64d8051118089a54cf14eb45dc96f74
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282376"
---
# <a name="pattern-value-arguments"></a>Argumentos de valor de padrão
Alguns argumentos nas funções do catálogo, como o argumento *TableName* no **SQLTables,** aceitam padrões de pesquisa. Esses argumentos aceitam padrões de pesquisa se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_FALSE; são argumentos identificadores que não aceitam um padrão de pesquisa se esse atributo for definido como SQL_TRUE.  
  
 Os caracteres do padrão de pesquisa são:  
  
-   Um sublinhado (_), que representa qualquer personagem único.  
  
-   Um sinal percentual (%), o que representa qualquer seqüência de zero ou mais caracteres.  
  
-   Um personagem de fuga, que é específico do motorista e é usado para incluir sublinhados, sinais por cento e o caráter de fuga como literals. Se o personagem de fuga precede um personagem não especial, o personagem de fuga não tem significado especial. Se o personagem de fuga precede um personagem especial, ele escapa do caráter especial. Por exemplo, "\a" seria tratado como\\dois caracteres,\\" e "a", mas " %" seria tratado como o caractere único não especial "%".  
  
 O caractere de fuga é recuperado com a opção SQL_SEARCH_PATTERN_ESCAPE no **SQLGetInfo**. Ele deve preceder qualquer sublinhado, sinal percentual ou caráter de fuga em um argumento que aceita padrões de pesquisa para incluir esse personagem como um literal. Exemplos são mostrados na tabela a seguir.  
  
|Padrão de pesquisa|Descrição|  
|--------------------|-----------------|  
|%A%|Todos os identificadores contendo a letra A|  
|ABC_|Todos os quatro identificadores de caracteres começando com ABC|  
|ABC\\_|O identificador ABC_, assumindo que o\\caractere de fuga é uma barra invertida ( )|  
|\\\\%|Todos os identificadores que\\começam com uma barra invertida ( ), assumindo que o caractere de fuga é uma barra invertida|  
  
 Deve-se tomar cuidado especial para escapar dos caracteres padrão de pesquisa em argumentos que aceitem padrões de pesquisa. Isso é particularmente verdadeiro para o personagem sublinhado, que é comumente usado em identificadores. Um erro comum em aplicativos é recuperar um valor de uma função de catálogo e passar esse valor para um argumento de padrão de pesquisa em outra função de catálogo. Por exemplo, suponha que um aplicativo recupere o nome da tabela MY_TABLE do conjunto de resultados para **SQLTables** e passe isso para **SQLColumns** para recuperar uma lista de colunas em MY_TABLE. Em vez de obter as colunas para MY_TABLE, o aplicativo receberá as colunas de todas as tabelas que correspondem ao padrão de pesquisa MY_TABLE, como MY_TABLE, MY1TABLE, MY2TABLE e assim por diante.  
  
> [!NOTE]
>  ODBC 2. *x* drivers não suportam padrões de pesquisa no argumento *CatalogName* no **SQLTables**. Os drivers ODBC 3 *.x* aceitam padrões de pesquisa neste argumento se o atributo de ambiente SQL_ATTR_ ODBC_VERSION estiver definido como SQL_OV_ODBC3; eles não aceitam padrões de pesquisa neste argumento se ele está definido para SQL_OV_ODBC2.  
  
 Passar um ponteiro nulo para um argumento de padrão de pesquisa não restringe a busca por esse argumento; ou seja, um ponteiro nulo e o padrão de pesquisa % (quaisquer caracteres) são equivalentes. No entanto, um padrão de pesquisa de comprimento zero - ou seja, um ponteiro válido para uma seqüência de comprimento zero - corresponde apenas à seqüência vazia ("").
