---
title: DLLs de tradução | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- translation DLLs [ODBC]
ms.assetid: 38975059-b346-410f-bb27-326f3f7bbf39
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0aaed3a9ef5f4ae81cad3407cdecb0c18b753b6d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="translation-dlls"></a>DLLs de tradução
O aplicativo e a fonte de dados geralmente armazenam dados em conjuntos de caracteres diferentes. ODBC fornece um mecanismo genérico que permite que o driver converter dados de um conjunto de caracteres para outro. Ele consiste em uma DLL que implementa as funções de conversão **SQLDriverToDataSource** e **SQLDataSourceToDriver**, que é chamado pelo driver para converter todos os dados fluindo entre a fonte de dados e o driver. Essa DLL pode ser gravado pelo desenvolvedor do aplicativo, o desenvolvedor de driver, ou de terceiros.  
  
 A DLL de conversão para uma determinada fonte de dados pode ser especificado nas informações do sistema para essa fonte de dados; Para obter mais informações, consulte [subchaves de especificação de fonte de dados](../../../odbc/reference/install/data-source-specification-subkeys.md). Ele também pode ser definido em tempo de execução com os atributos de conexão SQL_ATTR_TRANSLATE_DLL e SQL_ATTR_TRANSLATE_OPTION.  
  
 A opção de conversão é um valor que pode ser interpretado apenas por uma DLL de conversão específica. Por exemplo, se a conversão DLL converte entre diferentes páginas de código, a opção pode fornecer os números das páginas de código usadas pelo aplicativo e a fonte de dados. Não há nenhum requisito para uma DLL de conversão para usar uma opção de conversão.  
  
 Depois de uma tradução que dll foi especificado, o driver carrega e chamá-lo para converter todos os dados que fluem entre o aplicativo e a fonte de dados. Isso inclui todas as instruções SQL e parâmetros de caracteres que está sendo enviados para a fonte de dados e todos os resultados de caractere, os metadados de caractere, como nomes de coluna e mensagens de erro são recuperados da fonte de dados. Dados de Conexão não são traduzidos, porque a DLL de conversão não é carregado após o aplicativo conectou-se à fonte de dados.
