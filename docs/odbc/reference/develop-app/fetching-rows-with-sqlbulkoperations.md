---
title: Buscando linhas com SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], fetching rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: 0efee2d6-ce94-411e-9976-97ba28b8da37
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 60b6673c4a6d618e52c78b48fe7307c20c8628f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069840"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>Buscar linhas com SQLBulkOperations
Dados podem ser refetched em um conjunto de linhas usando indicadores por uma chamada para **SQLBulkOperations.** As linhas a serem buscados são identificadas por indicadores em uma coluna de indicador associado. Colunas com um valor de SQL_COLUMN_IGNORE não tiverem sido buscadas.  
  
 Para executar buscas em massa com **SQLBulkOperations**, o aplicativo faz o seguinte:  
  
1.  Recupera e armazena em cache os indicadores de todas as linhas a serem atualizadas. Se houver mais de um indicador e a associação é usada, os indicadores são armazenados em uma matriz; Se houver mais de um indicador e a associação por linha é usada, os indicadores são armazenados em uma matriz de estruturas de linha.  
  
2.  Define o atributo de instrução de SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas a serem buscadas e associa o buffer que contém o valor de indicador ou a matriz de indicadores, a coluna 0.  
  
3.  Define o valor no buffer de comprimento/indicador de cada coluna, conforme necessário. Esse é o comprimento de bytes dos dados ou SQL_NTS para colunas associadas a buffers de cadeia de caracteres, o tamanho de bytes dos dados para colunas associadas a buffers binários e SQL_NULL_DATA para todas as colunas a ser definido como NULL. O aplicativo define o valor no buffer de comprimento/indicador das colunas que devem ser definidos no padrão (se houver) ou nulo (se não existir um organograma) para SQL_COLUMN_IGNORE.  
  
4.  Chamadas **SQLBulkOperations** com o *operação* argumento definido como SQL_FETCH_BY_BOOKMARK.  
  
 Não é necessário para o aplicativo para usar a matriz de operação de linha para impedir que a operação a ser executada em determinadas colunas. O aplicativo seleciona as linhas que deseja buscar copiando apenas indicadores para as linhas para a matriz de indicador associado.
