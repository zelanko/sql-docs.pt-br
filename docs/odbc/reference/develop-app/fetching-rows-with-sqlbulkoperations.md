---
title: Buscar linhas com SQLBulkOperations | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae0b4c2114059cecaaf8f8825169300f131bd473
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305645"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>Buscar linhas com SQLBulkOperations
Os dados podem ser rebuscados em um conjunto de linhas usando marcadores por uma chamada para **SQLBulkOperations.** As linhas a serem buscadas são identificadas pelos marcadores em uma coluna de marcadores vinculada. Colunas com valor de SQL_COLUMN_IGNORE não são buscadas.  
  
 Para realizar buscas em massa com **o SQLBulkOperations,** o aplicativo faz o seguinte:  
  
1.  Recupera e armazena os marcadores de todas as linhas a serem atualizadas. Se houver mais de um marcador e a vinculação em termos de coluna for usada, os marcadores serão armazenados em uma matriz; se houver mais de um marcador e a vinculação em termos de linha for usada, os marcadores são armazenados em uma matriz de estruturas de linha.  
  
2.  Define o atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE ao número de linhas a serem buscadas e vincula o buffer contendo o valor do marcador, ou a matriz de marcadores, à coluna 0.  
  
3.  Define o valor no buffer de comprimento/indicador de cada coluna conforme necessário. Este é o comprimento do byte dos dados ou SQL_NTS para colunas vinculadas a buffers de seqüência, o comprimento do byte dos dados para colunas vinculadas a buffers binários e SQL_NULL_DATA para que quaisquer colunas sejam definidas como NULL. O aplicativo define o valor no buffer de comprimento/indicador das colunas que devem ser definidas como padrão (se existir) ou NULL (se não o fizer) para SQL_COLUMN_IGNORE.  
  
4.  Chama **SQLBulkOperations** com o argumento *Operação* definido para SQL_FETCH_BY_BOOKMARK.  
  
 Não há necessidade de o aplicativo usar o array de operação de linha para evitar que a operação seja executada em determinadas colunas. O aplicativo seleciona as linhas que deseja buscar copiando apenas os marcadores para essas linhas na matriz de marcadores vinculados.
