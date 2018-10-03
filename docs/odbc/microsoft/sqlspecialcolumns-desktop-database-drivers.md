---
title: SQLSpecialColumns (Drivers de banco de dados da área de trabalho) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Desktop Database Drivers
ms.assetid: 3de66fdf-053b-4354-979d-e76a5a5e975f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f319e6a28a1eba5f803e9cf7f7087f45f227fd87
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840004"
---
# <a name="sqlspecialcolumns-desktop-database-drivers"></a>SQLSpecialColumns (Drivers de banco de dados de área de trabalho)
Um índice exclusivo será retornado (se houver) para o sinalizador SQL_BEST_ROWID na *fColType*. Nenhum conjunto de resultados será retornado para o sinalizador SQL_ROWVER.  
  
 Todas as IDs de linha têm um escopo de SQL_SCOPE_CURROW.  
  
 Não há suporte para a correspondência de padrão para qualquer um de *szTableQualifier* ou *szTableName* argumento.
