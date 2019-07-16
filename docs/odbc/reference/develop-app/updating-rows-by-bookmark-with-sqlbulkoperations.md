---
title: Atualizando linhas por indicador com SQLBulkOperations | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e9b10037883ef9cfa4051195270e6477c5cc04ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091618"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>Atualizar linhas por indicador com SQLBulkOperations
Ao atualizar uma linha por indicador, **SQLBulkOperations** faz com que a fonte de dados atualize uma ou mais linhas da tabela. As linhas são identificadas pelo indicador em uma coluna de indicador associado. A linha é atualizada com o uso de dados nos buffers de aplicativo para cada coluna associada (exceto quando o valor no buffer de comprimento/indicador para uma coluna é SQL_COLUMN_IGNORE). Colunas não associadas não serão atualizadas.  
  
 Para atualizar linhas por indicador com **SQLBulkOperations**, o aplicativo:  
  
1.  Recupera e armazena em cache os indicadores de todas as linhas a serem atualizadas. Se houver mais de um indicador e a associação é usada, os indicadores são armazenados em uma matriz; Se houver mais de um indicador e a associação por linha é usada, os indicadores são armazenados em uma matriz de estruturas de linha.  
  
2.  Define o atributo da instrução SQL_ATTR_ROW_ARRAY_SIZE como o número de indicadores e associa o buffer que contém o valor de indicador ou a matriz de indicadores, a coluna 0.  
  
3.  Coloca os novos valores de dados nos buffers de conjunto de linhas. Para obter informações sobre como enviar dados longos com **SQLBulkOperations**, consulte [dados Long e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
4.  Define o valor no buffer de comprimento/indicador de cada coluna, conforme necessário. Esse é o comprimento de bytes dos dados ou SQL_NTS para colunas associadas a buffers de cadeia de caracteres, o tamanho de bytes dos dados para colunas associadas a buffers binários e SQL_NULL_DATA para todas as colunas a ser definido como NULL.  
  
5.  Define o valor no buffer de comprimento/indicador dessas colunas que não devem ser atualizados para SQL_COLUMN_IGNORE. Embora o aplicativo pode ignorar esta etapa e reenviar os dados existentes, isso é ineficiente e o risco de enviar valores para a fonte de dados foram truncados quando foram lidas.  
  
6.  Chamadas **SQLBulkOperations** com o *operação* argumento definido como SQL_UPDATE_BY_BOOKMARK.  
  
 Para cada linha é enviada à fonte de dados como uma atualização, os buffers do aplicativo devem ter dados de linha válido. Se os buffers do aplicativo foram preenchidos pela busca, se uma matriz de status de linha foi mantida, e se o valor de status para uma linha é SQL_ROW_DELETED, SQL_ROW_ERROR ou SQL_ROW_NOROW, dados inválidos inadvertidamente poderiam ser enviados à fonte de dados.
