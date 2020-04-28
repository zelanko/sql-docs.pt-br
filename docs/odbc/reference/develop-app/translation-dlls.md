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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81297941"
---
# <a name="translation-dlls"></a>DLLs de conversão
O aplicativo e a fonte de dados geralmente armazenam dados em conjuntos de caracteres diferentes. O ODBC fornece um mecanismo genérico que permite que o driver traduza dados de um conjunto de caracteres para outro. Ele consiste em uma DLL que implementa as funções de tradução **SQLDriverToDataSource** e **SQLDataSourceToDriver**, que são chamadas pelo driver para converter todo o fluxo de dados entre a fonte de dados e o driver. Essa DLL pode ser escrita pelo desenvolvedor do aplicativo, pelo desenvolvedor do driver ou por terceiros.  
  
 A DLL de tradução para uma determinada fonte de dados pode ser especificada nas informações do sistema para essa fonte de dados; para obter mais informações, consulte [subchaves de especificação de fonte de dados](../../../odbc/reference/install/data-source-specification-subkeys.md). Ele também pode ser definido em tempo de execução com os atributos de conexão SQL_ATTR_TRANSLATE_DLL e SQL_ATTR_TRANSLATE_OPTION.  
  
 A opção de conversão é um valor que pode ser interpretado somente por uma DLL de tradução específica. Por exemplo, se a DLL de tradução estiver convertida entre diferentes páginas de código, a opção poderá fornecer os números das páginas de código usadas pelo aplicativo e pela fonte de dados. Não há nenhum requisito para que uma DLL de tradução use uma opção de conversão.  
  
 Após a especificação de uma DLL de conversão, o driver a carrega e a chama para converter todos os dados que fluem entre o aplicativo e a fonte de dados. Isso inclui todas as instruções SQL e os parâmetros de caractere que estão sendo enviados para a fonte de dados e todos os resultados de caracteres, metadados de caracteres como nomes de coluna e mensagens de erro recuperadas da fonte de dados. Os dados de conexão não são convertidos, pois a DLL de tradução não é carregada até que o aplicativo se conecte à fonte de dados.
