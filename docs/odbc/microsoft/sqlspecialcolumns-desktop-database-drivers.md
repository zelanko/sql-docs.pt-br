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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200503"
---
# <a name="sqlspecialcolumns-desktop-database-drivers"></a>SQLSpecialColumns (Drivers de banco de dados de área de trabalho)
Um índice exclusivo será retornado (se houver) para o sinalizador SQL_BEST_ROWID na *fColType*. Nenhum conjunto de resultados será retornado para o sinalizador SQL_ROWVER.  
  
 Todas as IDs de linha têm um escopo de SQL_SCOPE_CURROW.  
  
 Não há suporte para a correspondência de padrão para qualquer um de *szTableQualifier* ou *szTableName* argumento.
