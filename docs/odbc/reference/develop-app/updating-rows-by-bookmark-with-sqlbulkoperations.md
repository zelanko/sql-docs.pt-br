---
title: Atualizando linhas por Marcador com SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], updating rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: c9ad82b7-8dba-45b0-bdb9-f4668b37c0d6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9c755297e8beadad92b5be81d78ca534bb96ecae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283194"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>Atualizar linhas por indicador com SQLBulkOperations
Ao atualizar uma linha por marcador, **a SQLBulkOperations** faz com que a fonte de dados atualize uma ou mais linhas da tabela. As linhas são identificadas pelo marcador em uma coluna de marcadores vinculada. A linha é atualizada usando dados nos buffers de aplicativos para cada coluna vinculada (exceto quando o valor no buffer comprimento/indicador de uma coluna é SQL_COLUMN_IGNORE). As colunas não vinculadas não serão atualizadas.  
  
 Para atualizar linhas por marcador com **SQLBulkOperations,** o aplicativo:  
  
1.  Recupera e armazena os marcadores de todas as linhas a serem atualizadas. Se houver mais de um marcador e a vinculação em termos de coluna for usada, os marcadores serão armazenados em uma matriz; se houver mais de um marcador e a vinculação em termos de linha for usada, os marcadores são armazenados em uma matriz de estruturas de linha.  
  
2.  Define o atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE ao número de marcadores e vincula o buffer contendo o valor do marcador, ou a matriz de marcadores, à coluna 0.  
  
3.  Coloca os novos valores de dados nos buffers de conjunto de linhas. Para obter informações sobre como enviar dados longos com **sqlbulkoperations,** consulte [Long Data e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
4.  Define o valor no buffer de comprimento/indicador de cada coluna conforme necessário. Este é o comprimento do byte dos dados ou SQL_NTS para colunas vinculadas a buffers de seqüência, o comprimento do byte dos dados para colunas vinculadas a buffers binários e SQL_NULL_DATA para que quaisquer colunas sejam definidas como NULL.  
  
5.  Define o valor no buffer de comprimento/indicador das colunas que não devem ser atualizadas para SQL_COLUMN_IGNORE. Embora o aplicativo possa pular essa etapa e reenviar dados existentes, isso é ineficiente e corre o risco de enviar valores para a fonte de dados que foram truncados quando foram lidos.  
  
6.  Chama **SQLBulkOperations** com o argumento *Operação* definido para SQL_UPDATE_BY_BOOKMARK.  
  
 Para cada linha enviada à fonte de dados como uma atualização, os buffers do aplicativo devem ter dados de linha válidos. Se os buffers de aplicativo foram preenchidos por busca, se uma matriz de status de linha foi mantida e se o valor de status de uma linha for SQL_ROW_DELETED, SQL_ROW_ERROR ou SQL_ROW_NOROW, dados inválidos podem ser enviados inadvertidamente para a fonte de dados.
