---
title: Alças de Declaração | Microsoft Docs
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
ms.openlocfilehash: 1be90fe10d10a0b087d1c9724fed249805eb4dba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299672"
---
# <a name="statement-handles"></a>Identificadores de instrução
Uma *declaração* é mais facilmente considerada como uma declaração SQL, como **SELECT \* FROM Employee**. No entanto, uma declaração é mais do que apenas uma declaração SQL - ela consiste em todas as informações associadas a essa declaração SQL, como quaisquer conjuntos de resultados criados pela declaração e parâmetros usados na execução da declaração. Uma declaração nem precisa ter uma declaração SQL definida pelo aplicativo. Por exemplo, quando uma função de catálogo como **SQLTables** é executada em uma declaração, ela executa uma declaração SQL predefinida que retorna uma lista de nomes de tabela.  
  
 Cada declaração é identificada por uma alça de declaração. Uma instrução está associada a uma única conexão, e pode haver várias instruções sobre essa conexão. Alguns drivers limitam o número de declarações ativas que suportam; a opção SQL_MAX_CONCURRENT_ACTIVITIES no **SQLGetInfo** especifica quantas instruções ativas um driver suporta em uma única conexão. Uma instrução é definida como *ativa* se tiver resultados pendentes, onde os resultados são definidos por resultados ou a contagem de linhas afetadas por uma instrução **INSERT,** **UPDATE**ou **DELETE,** ou dados estão sendo enviados com várias chamadas para **SQLPutData**.  
  
 Dentro de um pedaço de código que implementa o ODBC (o Driver Manager ou um driver), a alça da declaração identifica uma estrutura que contém informações de declaração, tais como:  
  
-   O estado da declaração  
  
-   Os diagnósticos atuais em nível de declaração  
  
-   Os endereços das variáveis de aplicação vinculados aos parâmetros da declaração e colunas de conjunto de resultados  
  
-   As configurações atuais de cada atributo de declaração  
  
 As alças de declaração são usadas na maioria das funções ODBC. Notavelmente, eles são usados nas funções para vincular parâmetros e colunas de conjunto de resultados **(SQLBindParameter** e **SQLBindCol),** preparar e executar instruções **(SQLPrepare,** **SQLExecute**e **SQLExecDirect),** recuperar metadados **(SQLColAttribute** e **SQLDescribeCol),** buscar resultados **(SQLFetch)** e recuperar diagnósticos **(SQLGetDiagField** e **SQLGetDiag).** Eles também são usados em funções de catálogo **(SQLColumns,** **SQLTables,** e assim por diante) e uma série de outras funções.  
  
 As alças de declaração são alocadas com **SQLAllocHandle** e liberadas com **SQLFreeHandle**.
