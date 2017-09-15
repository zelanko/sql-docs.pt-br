---
title: Atualizando linhas por indicador com SQLBulkOperations | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], updating rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: c9ad82b7-8dba-45b0-bdb9-f4668b37c0d6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4426465ea41b257a4805399b703f28ccc22d704b
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>Atualizando linhas por indicador com SQLBulkOperations
Ao atualizar uma linha pelo indicador, **SQLBulkOperations** faz com que a fonte de dados atualizar uma ou mais linhas da tabela. As linhas são identificadas pelo indicador em uma coluna de indicador associado. A linha é atualizada usando dados em buffers do aplicativo para cada coluna associada (exceto quando o valor no buffer de comprimento/indicador para uma coluna é SQL_COLUMN_IGNORE). Colunas não associadas não serão atualizadas.  
  
 Para atualizar linhas por indicador com **SQLBulkOperations**, o aplicativo:  
  
1.  Recupera e armazena em cache os indicadores de todas as linhas a serem atualizadas. Se houver mais de um indicador e a associação é usada, os indicadores são armazenados em uma matriz; Se houver mais de um indicador e a associação é usada, os indicadores são armazenados em uma matriz de estruturas de linha.  
  
2.  Define o atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE como o número de indicadores e associa o buffer que contém o valor de indicador ou a matriz de indicadores, a coluna 0.  
  
3.  Coloca os novos valores de dados em buffers do conjunto de linhas. Para obter informações sobre como enviar dados longos com **SQLBulkOperations**, consulte [dados longos e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
4.  Define o valor do buffer de comprimento/indicador de cada coluna, conforme necessário. Esse é o comprimento de bytes dos dados ou SQL_NTS para colunas associadas aos buffers de cadeia de caracteres, o comprimento de bytes de dados para colunas vinculadas buffers binários e SQL_NULL_DATA para todas as colunas a ser definido como NULL.  
  
5.  Define o valor do buffer de comprimento/indicador dessas colunas que não devem ser atualizadas para SQL_COLUMN_IGNORE. Embora o aplicativo pode ignorar esta etapa e reenviar os dados existentes, isso é ineficiente e corre o risco de enviar valores para a fonte de dados que foram truncados quando foram lidas.  
  
6.  Chamadas **SQLBulkOperations** com o *operação* argumento definido como SQL_UPDATE_BY_BOOKMARK.  
  
 Para cada linha que é enviada para a fonte de dados como uma atualização, os buffers do aplicativo devem ter dados de linha válido. Se os buffers do aplicativo foram preenchidos pela busca, se uma matriz de status de linha foi mantida, e se o valor de status de uma linha for SQL_ROW_DELETED, SQL_ROW_ERROR ou SQL_ROW_NOROW, os dados inválidos inadvertidamente foi enviados para a fonte de dados.
