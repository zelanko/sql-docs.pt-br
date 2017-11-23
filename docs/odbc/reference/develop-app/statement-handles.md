---
title: "Identificadores de instrução | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 65d6d78b-a8c8-489a-9dad-f8d127a44882
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dedc2ece9c73c0be4e9bbab61e231ab8e2d3060a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="statement-handles"></a>Identificadores de instrução
Um *instrução* é mais fácil pensar como uma instrução SQL, como **selecione \* do funcionário**. No entanto, uma instrução é mais do que apenas uma instrução SQL — consiste em todas as informações associadas a essa instrução SQL, como conjuntos de resultados criados pela instrução e os parâmetros usados na execução da instrução. Uma instrução não mesmo precisa ter uma instrução SQL definido pelo aplicativo. Por exemplo, quando uma função de catálogo como **SQLTables** é executado em uma instrução, ele executa uma instrução SQL predefinida que retorna uma lista de nomes de tabela.  
  
 Cada instrução é identificada por um identificador de instrução. Uma instrução é associada uma única conexão, e pode haver várias instruções nessa conexão. Alguns drivers de limitam o número de instruções ativas que eles oferecem suporte; opção o SQL_MAX_CONCURRENT_ACTIVITIES **SQLGetInfo** Especifica quantas instruções ativas um driver oferece suporte em uma única conexão. Uma instrução é definida para ser *active* se ela tiver resultados pendentes, onde resultados são um conjunto de resultados ou a contagem de linhas afetadas por uma **inserir**, **atualização**, ou **Excluir** instrução, ou os dados estão sendo enviados com várias chamadas para **SQLPutData**.  
  
 Dentro de um trecho de código que implementa ODBC (o Gerenciador de Driver ou um driver), o identificador de instrução identifica uma estrutura que contém informações sobre a instrução, como:  
  
-   Estado da instrução  
  
-   O diagnóstico de nível de instrução atual  
  
-   Os endereços das variáveis de aplicativo associada aos parâmetros da instrução e colunas do conjunto de resultados  
  
-   As configurações atuais de cada atributo de instrução  
  
 Identificadores de instrução são usados na maioria das funções ODBC. Em especial, eles são usados nas funções para associar parâmetros e colunas do conjunto de resultados (**SQLBindParameter** e **SQLBindCol**), preparar e executar instruções (**SQLPrepare** **SQLExecute**, e **SQLExecDirect**), recuperar metadados (**SQLColAttribute** e **SQLDescribeCol**), busca resultados (**SQLFetch**) e recuperar o diagnóstico (**SQLGetDiagField** e **SQLGetDiagRec**). Eles também são usados em funções de catálogo (**SQLColumns**, **SQLTables**, e assim por diante) e um número de outras funções.  
  
 Identificadores de instrução são alocados com **SQLAllocHandle** e liberadas com **SQLFreeHandle**.
