---
title: SQLSpecialColumns (Drivers do banco de dados de área de trabalho) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Desktop Database Drivers
ms.assetid: 3de66fdf-053b-4354-979d-e76a5a5e975f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aebdcc1d45584ec0fa7d287715e2defc8ef278fb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32902881"
---
# <a name="sqlspecialcolumns-desktop-database-drivers"></a>SQLSpecialColumns (Drivers do banco de dados de área de trabalho)
Um índice exclusivo será retornado (se houver) para o sinalizador de SQL_BEST_ROWID *fColType*. Nenhum conjunto de resultados será retornado para o sinalizador SQL_ROWVER.  
  
 Todas as IDs de linha têm um escopo de SQL_SCOPE_CURROW.  
  
 Não há suporte para a correspondência de padrão para qualquer um de *szTableQualifier* ou *szTableName* argumento.
