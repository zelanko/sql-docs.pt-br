---
title: DLLs de tradução | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translation DLLs [ODBC]
ms.assetid: 38975059-b346-410f-bb27-326f3f7bbf39
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3dad12bcd71434c1013b4fde5b4bd0231e56016f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297941"
---
# <a name="translation-dlls"></a>DLLs de conversão
O aplicativo e a fonte de dados geralmente armazenam dados em diferentes conjuntos de caracteres. O ODBC fornece um mecanismo genérico que permite ao driver traduzir dados de um caractere definido para outro. Ele consiste em uma DLL que implementa as funções de tradução **SQLDriverToDataSource** e **SQLDataSourceToDriver**, que são chamadas pelo driver para traduzir todos os dados que fluem entre a fonte de dados e o driver. Este DLL pode ser escrito pelo desenvolvedor do aplicativo, pelo desenvolvedor do driver ou por terceiros.  
  
 A dLL de tradução para uma fonte de dados específica pode ser especificada nas informações do sistema para essa fonte de dados; para obter mais informações, consulte [Subchaves de especificação de origem de dados](../../../odbc/reference/install/data-source-specification-subkeys.md). Ele também pode ser definido em tempo de execução com os atributos de conexão SQL_ATTR_TRANSLATE_DLL e SQL_ATTR_TRANSLATE_OPTION.  
  
 A opção de tradução é um valor que pode ser interpretado apenas por uma dLL de tradução específica. Por exemplo, se a dLL de tradução traduzir entre diferentes páginas de código, a opção pode dar os números das páginas de código usadas pelo aplicativo e a fonte de dados. Não há necessidade de uma DLL de tradução usar uma opção de tradução.  
  
 Depois que uma DLL de tradução foi especificada, o driver a carrega e a chama para traduzir todos os dados que fluem entre o aplicativo e a fonte de dados. Isso inclui todas as instruções SQL e parâmetros de caracteres sendo enviados para a fonte de dados e todos os resultados de caracteres, metadados de caracteres, como nomes de colunas e mensagens de erro recuperadas da fonte de dados. Os dados de conexão não são traduzidos, porque a DLL de tradução não é carregada até que o aplicativo tenha sido conectado à fonte de dados.
