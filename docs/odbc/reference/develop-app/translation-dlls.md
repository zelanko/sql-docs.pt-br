---
title: DLLs de conversão | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec1d0e23019f3e5b68ad38711c1f041b160ceb31
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47833854"
---
# <a name="translation-dlls"></a>DLLs de conversão
O aplicativo e a fonte de dados geralmente armazenam dados em conjuntos de caracteres diferentes. O ODBC fornece um mecanismo genérico que permite que o driver converter dados de um conjunto de caracteres para outra. Ele consiste em uma DLL que implementa as funções de conversão **SQLDriverToDataSource** e **SQLDataSourceToDriver**, que são chamados pelo driver para converter todos os dados fluindo entre a fonte de dados e o driver. Essa DLL pode ser escrito pelo desenvolvedor do aplicativo, o desenvolvedor de driver, ou por terceiros.  
  
 A DLL de conversão para uma determinada fonte de dados pode ser especificado nas informações do sistema para essa fonte de dados; Para obter mais informações, consulte [subchaves de especificação de fonte de dados](../../../odbc/reference/install/data-source-specification-subkeys.md). Ele também pode ser definido em tempo de execução com os atributos de conexão SQL_ATTR_TRANSLATE_DLL e SQL_ATTR_TRANSLATE_OPTION.  
  
 A opção de conversão é um valor que pode ser interpretado somente por uma DLL de conversão específica. Por exemplo, se a tradução DLL converte entre diferentes páginas de código, a opção pode dar os números das páginas de código usadas pelo aplicativo e a fonte de dados. Não há nenhum requisito para uma DLL de conversão para usar uma opção de tradução.  
  
 Depois de uma tradução que dll tiver sido especificado, o driver carrega e chama-o para converter todos os dados fluindo entre o aplicativo e a fonte de dados. Isso inclui todas as instruções SQL e os parâmetros de caracteres que estão sendo enviados à fonte de dados e todos os resultados de caractere, metadados de caractere, como nomes de coluna e mensagens de erro são recuperados da fonte de dados. Dados de Conexão não são traduzidos, porque a DLL de conversão não é carregada até depois que o aplicativo se conectou à fonte de dados.
