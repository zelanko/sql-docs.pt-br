---
description: Identificadores de instrução
title: Identificadores de instrução | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 65d6d78b-a8c8-489a-9dad-f8d127a44882
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a93bdd42acccdca0563edc4104734d04522e7879
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476338"
---
# <a name="statement-handles"></a>Identificadores de instrução
Uma *instrução* é mais facilmente considerada como uma instrução SQL, como **selecionar \* do funcionário**. No entanto, uma instrução é mais do que apenas uma instrução SQL – ela consiste em todas as informações associadas a essa instrução SQL, como quaisquer conjuntos de resultados criados pela instrução e os parâmetros usados na execução da instrução. Uma instrução não precisa nem ter uma instrução SQL definida pelo aplicativo. Por exemplo, quando uma função de catálogo como **SQLTables** é executada em uma instrução, ela executa uma instrução SQL predefinida que retorna uma lista de nomes de tabela.  
  
 Cada instrução é identificada por um identificador de instrução. Uma instrução é associada a uma única conexão e pode haver várias instruções nessa conexão. Alguns drivers limitam o número de instruções ativas para as quais dão suporte; a opção SQL_MAX_CONCURRENT_ACTIVITIES em **SQLGetInfo** especifica quantas instruções ativas um driver dá suporte em uma única conexão. Uma instrução é definida como *ativa* se tiver resultados pendentes, onde os resultados são um conjunto de resultados ou a contagem de linhas afetadas por uma instrução **Insert**, **Update**ou **delete** , ou os dados estão sendo enviados com várias chamadas para **SQLPutData**.  
  
 Dentro de um trecho de código que implementa o ODBC (o Gerenciador de driver ou um driver), o identificador de instrução identifica uma estrutura que contém informações de instrução, como:  
  
-   O estado da instrução  
  
-   O diagnóstico atual no nível da instrução  
  
-   Os endereços das variáveis de aplicativo associadas aos parâmetros da instrução e às colunas do conjunto de resultados  
  
-   As configurações atuais de cada atributo de instrução  
  
 Os identificadores de instrução são usados na maioria das funções ODBC. Notavelmente, eles são usados nas funções para associar parâmetros e colunas de conjunto de resultados **(SQLBindParameter** e **SQLBindCol**), instruções de preparação e execução (**SQLPrepare**, **SQLExecute**e **SQLExecDirect**), recuperam metadados (**SQLColAttribute** e **SQLDescribeCol**), buscam resultados (**SQLFetch**) e recuperam diagnósticos (**SQLGetDiagField** e **SQLGetDiagRec**). Eles também são usados em funções de catálogo (**SQLColumns**, **SQLTables**e assim por diante) e em várias outras funções.  
  
 Os identificadores de instrução são alocados com **SQLAllocHandle** e liberados com **SQLFreeHandle**.
