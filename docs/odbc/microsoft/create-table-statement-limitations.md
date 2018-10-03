---
title: TABELA limitações da instrução CREATE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE statement limitations [ODBC]
- ODBC SQL grammar, CREATE TABLE statement limitations
ms.assetid: c5067855-20c9-456f-8d63-f375b4297f2e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5eab1c3bf6891f10c897966035dced2ffdc10ba
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622104"
---
# <a name="create-table-statement-limitations"></a>Limitações da instrução CREATE TABLE
Quando o Microsoft Access, Microsoft Excel ou Paradoxdriver é usado e o comprimento de uma coluna de texto ou binário não for especificado (ou é especificado como 0), o comprimento da coluna será definido como 255.  
  
 Quando o driver do dBASE é usado e o comprimento de uma coluna de texto ou binário não for especificado (ou é especificado como 0), o comprimento da coluna será definido como 254.  
  
 Há suporte para um máximo de 255 colunas.  
  
 Não é possível criar quando o driver do Microsoft Excel é usado em um Microsoft Excel 5.0, 7.0, ou a fonte de 97 dados, uma planilha com o mesmo nome de uma planilha que foi descartado anteriormente. Quando o driver do Microsoft Excel é usado para acessar uma planilha de versão 5.0, 7.0 ou 97, uma instrução DROP TABLE limpa a planilha, mas não exclui o nome da planilha.  
  
 Quando o driver do Paradox é usado, as colunas não podem ser adicionadas depois que um índice foi definido em uma tabela. Se a primeira coluna da lista de argumentos de uma instrução CREATE TABLE cria um índice, uma segunda coluna não pode ser incluída na lista de argumentos.
