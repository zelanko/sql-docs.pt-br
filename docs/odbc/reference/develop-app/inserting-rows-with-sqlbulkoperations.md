---
title: Inserindo linhas com SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], inserting rows
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: ed585ea7-4d56-4df9-8dc3-53ca82382450
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a6fa384292f02026b8390aa92525144dce6f549b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300106"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>Inserir linhas com SQLBulkOperations
Inserir dados com **o SQLBulkOperations** é semelhante à atualização de dados com **o SQLBulkOperations** porque ele usa dados dos buffers de aplicativos vinculados.  
  
 De modo que cada coluna na nova linha tenha um valor, todas as colunas vinculadas com um valor de comprimento/indicador de SQL_COLUMN_IGNORE e todas as colunas não vinculadas devem aceitar valores NULL ou ter um padrão.  
  
 Para inserir linhas com **SQLBulkOperations,** o aplicativo faz o seguinte:  
  
1.  Define o atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE ao número de linhas a serem inseridas e coloca os novos valores de dados nos buffers de aplicativos vinculados. Para obter informações sobre como enviar dados longos com **sqlbulkoperations,** consulte [Long Data e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
2.  Define o valor no buffer de comprimento/indicador de cada coluna conforme necessário. Este é o comprimento do byte dos dados ou SQL_NTS para colunas vinculadas a buffers de seqüência, o comprimento do byte dos dados para colunas vinculadas a buffers binários e SQL_NULL_DATA para que quaisquer colunas sejam definidas como NULL. O aplicativo define o valor no buffer de comprimento/indicador das colunas que devem ser definidas como padrão (se existir) ou NULL (se não o fizer) para SQL_COLUMN_IGNORE.  
  
3.  Chama **SQLBulkOperations** com o argumento *Operação* definido para SQL_ADD.  
  
 Após o retorno **do SQLBulkOperations,** a linha atual fica inalterada. Se a coluna de marcadores (coluna 0) estiver vinculada, **a SQLBulkOperations** retorna os marcadores das linhas inseridas no buffer de conjunto de linhas vinculados a essa coluna.
