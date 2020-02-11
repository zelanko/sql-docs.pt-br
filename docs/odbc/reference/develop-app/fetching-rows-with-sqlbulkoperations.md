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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069840"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>Buscar linhas com SQLBulkOperations
Os dados podem ser buscados novamente em um conjunto de linhas usando indicadores por uma chamada para **SQLBulkOperations.** As linhas a serem buscadas são identificadas pelos indicadores em uma coluna de indicador associado. Colunas com um valor de SQL_COLUMN_IGNORE não são buscadas.  
  
 Para executar buscas em massa com **SQLBulkOperations**, o aplicativo faz o seguinte:  
  
1.  Recupera e armazena em cache os indicadores de todas as linhas a serem atualizadas. Se houver mais de um indicador e a associação por coluna for usada, os indicadores serão armazenados em uma matriz; Se houver mais de um indicador e uma associação de linha-inteligente for usada, os indicadores serão armazenados em uma matriz de estruturas de linha.  
  
2.  Define o atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas a serem buscadas e vincula o buffer que contém o valor de indicador, ou a matriz de indicadores, à coluna 0.  
  
3.  Define o valor no buffer de comprimento/indicador de cada coluna, conforme necessário. Esse é o comprimento de bytes dos dados ou SQL_NTS para colunas vinculadas a buffers de cadeia de caracteres, o comprimento de bytes dos dados para colunas vinculadas a buffers binários e SQL_NULL_DATA para qualquer coluna a ser definida como NULL. O aplicativo define o valor no buffer de comprimento/indicador dessas colunas que devem ser definidas para o padrão (se houver) ou NULL (se não houver) para SQL_COLUMN_IGNORE.  
  
4.  Chama **SQLBulkOperations** com o argumento de *operação* definido como SQL_FETCH_BY_BOOKMARK.  
  
 Não é necessário que o aplicativo use a matriz de operação de linha para impedir que a operação seja executada em determinadas colunas. O aplicativo seleciona as linhas que deseja buscar copiando somente os indicadores para essas linhas na matriz de indicador acoplada.
