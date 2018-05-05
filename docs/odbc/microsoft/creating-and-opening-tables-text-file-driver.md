---
title: Criar e abrir tabelas (Driver de arquivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], creating and opening tables
ms.assetid: e6a07dda-a665-4f5b-a8d6-9ff479700513
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2693e65aa00628066915ee3dd4b00304eed3fa94
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="creating-and-opening-tables-text-file-driver"></a>Criar e abrir tabelas (Driver de arquivo de texto)
Quando o driver de texto é usado, uma nova tabela é criada usando o formato especificado no Odbcinst.ini. Se não for especificado, as tabelas são criadas no formato CSVDELIMITED. Por padrão, o padrão de colunas de INTEIROS para 11 caracteres e FLOAT colunas padrão 22 caracteres. Colunas de data e usam o formato AAAA-MM-DD. CHAR e colunas LONGCHAR são a largura especificada na instrução CREATE.
