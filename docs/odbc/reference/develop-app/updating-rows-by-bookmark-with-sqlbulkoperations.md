---
description: Atualizar linhas por indicador com SQLBulkOperations
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9981136d546d53b131cff0d71edcdeab5b2e650c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482869"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>Atualizar linhas por indicador com SQLBulkOperations
Ao atualizar uma linha por indicador, o **SQLBulkOperations** faz com que a fonte de dados atualize uma ou mais linhas da tabela. As linhas são identificadas pelo indicador em uma coluna de indicador associado. A linha é atualizada usando dados nos buffers de aplicativo para cada coluna associada (exceto quando o valor no buffer de comprimento/indicador de uma coluna é SQL_COLUMN_IGNORE). As colunas não associadas não serão atualizadas.  
  
 Para atualizar linhas por indicador com **SQLBulkOperations**, o aplicativo:  
  
1.  Recupera e armazena em cache os indicadores de todas as linhas a serem atualizadas. Se houver mais de um indicador e a associação por coluna for usada, os indicadores serão armazenados em uma matriz; Se houver mais de um indicador e uma associação de linha-inteligente for usada, os indicadores serão armazenados em uma matriz de estruturas de linha.  
  
2.  Define o atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE como o número de indicadores e associa o buffer que contém o valor do indicador, ou a matriz de indicadores, à coluna 0.  
  
3.  Coloca os novos valores de dados nos buffers de conjunto de linhas. Para obter informações sobre como enviar dados longos com o **SQLBulkOperations**, consulte [Long data e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
4.  Define o valor no buffer de comprimento/indicador de cada coluna, conforme necessário. Esse é o comprimento de bytes dos dados ou SQL_NTS para colunas vinculadas a buffers de cadeia de caracteres, o comprimento de bytes dos dados para colunas vinculadas a buffers binários e SQL_NULL_DATA para qualquer coluna a ser definida como NULL.  
  
5.  Define o valor no buffer de comprimento/indicador das colunas que não devem ser atualizadas para SQL_COLUMN_IGNORE. Embora o aplicativo possa ignorar essa etapa e reenviar os dados existentes, isso é ineficiente e os riscos de envio de valores para a fonte de dados que foram truncados quando foram lidos.  
  
6.  Chama **SQLBulkOperations** com o argumento de *operação* definido como SQL_UPDATE_BY_BOOKMARK.  
  
 Para cada linha enviada à fonte de dados como uma atualização, os buffers de aplicativo devem ter dados de linha válidos. Se os buffers de aplicativo foram preenchidos pela busca, se uma matriz de status de linha tiver sido mantida e se o valor de status de uma linha for SQL_ROW_DELETED, SQL_ROW_ERROR ou SQL_ROW_NOROW, os dados inválidos poderão ser enviados inadvertidamente à fonte de dados.
