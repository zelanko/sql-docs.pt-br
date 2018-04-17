---
title: Limitações de declaração de tabela DROP | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- ODBC SQL grammar, DROP TABLE statement limitations
- DROP TABLE statement limitations [ODBC]
ms.assetid: 0a1c80f5-c9f2-4655-9bfd-0131b2f015a9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae6cfb8306c2422585dbb8775e4863108004a5a7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="drop-table-statement-limitations"></a>Remover tabela limitações de instrução
Quando o driver do Microsoft Excel 5.0, 7.0 ou 97 é usado, a instrução DROP TABLE limpa a planilha, mas não exclui o nome da planilha. Porque o nome da planilha ainda existe na pasta de trabalho, outra planilha não pode ser criada com o mesmo nome.
