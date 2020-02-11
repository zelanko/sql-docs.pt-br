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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 05b8f71d6f4c885c7dc64887dd92b1f600005ca7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138919"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>Inserir linhas com SQLBulkOperations
A inserção de dados com **SQLBulkOperations** é semelhante à atualização de dados com o **SQLBulkOperations** porque ele usa dados dos buffers de aplicativo associados.  
  
 Para que cada coluna na nova linha tenha um valor, todas as colunas associadas com um valor de comprimento/indicador de SQL_COLUMN_IGNORE e todas as colunas não associadas devem aceitar valores nulos ou ter um padrão.  
  
 Para inserir linhas com **SQLBulkOperations**, o aplicativo faz o seguinte:  
  
1.  Define o atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas a serem inseridas e coloca os novos valores de dados nos buffers de aplicativo associados. Para obter informações sobre como enviar dados longos com o **SQLBulkOperations**, consulte [Long data e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
2.  Define o valor no buffer de comprimento/indicador de cada coluna, conforme necessário. Esse é o comprimento de bytes dos dados ou SQL_NTS para colunas vinculadas a buffers de cadeia de caracteres, o comprimento de bytes dos dados para colunas vinculadas a buffers binários e SQL_NULL_DATA para qualquer coluna a ser definida como NULL. O aplicativo define o valor no buffer de comprimento/indicador dessas colunas que devem ser definidas para o padrão (se houver) ou NULL (se não houver) para SQL_COLUMN_IGNORE.  
  
3.  Chama **SQLBulkOperations** com o argumento de *operação* definido como SQL_ADD.  
  
 Depois que **SQLBulkOperations** retorna, a linha atual é inalterada. Se a coluna de indicador (coluna 0) estiver associada, **SQLBulkOperations** retornará os indicadores das linhas inseridas no buffer de conjunto de linhas associado a essa coluna.
