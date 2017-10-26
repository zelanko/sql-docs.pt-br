---
title: Criar e abrir tabelas (Driver de arquivo de texto) | Microsoft Docs
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
- text file driver [ODBC], creating and opening tables
ms.assetid: e6a07dda-a665-4f5b-a8d6-9ff479700513
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 41190a0a3eabda2f73c8f6046a64b7b7db929fa1
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="creating-and-opening-tables-text-file-driver"></a>Criar e abrir tabelas (Driver de arquivo de texto)
Quando o driver de texto é usado, uma nova tabela é criada usando o formato especificado no Odbcinst.ini. Se não for especificado, as tabelas são criadas no formato CSVDELIMITED. Por padrão, o padrão de colunas de INTEIROS para 11 caracteres e FLOAT colunas padrão 22 caracteres. Colunas de data e usam o formato AAAA-MM-DD. CHAR e colunas LONGCHAR são a largura especificada na instrução CREATE.

