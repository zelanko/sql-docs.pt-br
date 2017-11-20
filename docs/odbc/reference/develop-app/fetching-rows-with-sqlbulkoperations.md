---
title: Buscar linhas com SQLBulkOperations | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], fetching rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: 0efee2d6-ce94-411e-9976-97ba28b8da37
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f0e3f46b5dd742ff1e77c87a8486038c41839764
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="fetching-rows-with-sqlbulkoperations"></a>Buscar linhas com SQLBulkOperations
Dados podem ser refetched em um conjunto de linhas usando indicadores por uma chamada para **SQLBulkOperations.** As linhas a serem obtidos são identificadas por indicadores em uma coluna de indicador associado. Colunas com um valor de SQL_COLUMN_IGNORE não tiverem sido buscadas.  
  
 Para executar buscas em massa com **SQLBulkOperations**, o aplicativo faz o seguinte:  
  
1.  Recupera e armazena em cache os indicadores de todas as linhas a serem atualizadas. Se houver mais de um indicador e a associação é usada, os indicadores são armazenados em uma matriz; Se houver mais de um indicador e a associação é usada, os indicadores são armazenados em uma matriz de estruturas de linha.  
  
2.  Define o atributo de instrução de SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas a serem buscadas e associa o buffer que contém o valor de indicador ou a matriz de indicadores, a coluna 0.  
  
3.  Define o valor do buffer de comprimento/indicador de cada coluna, conforme necessário. Esse é o comprimento de bytes dos dados ou SQL_NTS para colunas associadas aos buffers de cadeia de caracteres, o comprimento de bytes de dados para colunas vinculadas buffers binários e SQL_NULL_DATA para todas as colunas a ser definido como NULL. O aplicativo define o valor do buffer de comprimento/indicador das colunas que devem ser definidas para seu padrão (se houver) ou nulo (se não) a SQL_COLUMN_IGNORE.  
  
4.  Chamadas **SQLBulkOperations** com o *operação* argumento definido como SQL_FETCH_BY_BOOKMARK.  
  
 Não é necessário para o aplicativo para usar a matriz de operação de linha para impedir que a operação a ser executada em determinadas colunas. O aplicativo seleciona as linhas que deseja buscar copiando apenas os indicadores para as linhas para a matriz de indicador associado.

