---
title: Limitações de declaração de tabela DROP | Microsoft Docs
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
- ODBC SQL grammar, DROP TABLE statement limitations
- DROP TABLE statement limitations [ODBC]
ms.assetid: 0a1c80f5-c9f2-4655-9bfd-0131b2f015a9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2d5959fe83037a61e2dc3a0d25bee65c512fe08
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="drop-table-statement-limitations"></a>Remover tabela limitações de instrução
Quando o driver do Microsoft Excel 5.0, 7.0 ou 97 é usado, a instrução DROP TABLE limpa a planilha, mas não exclui o nome da planilha. Porque o nome da planilha ainda existe na pasta de trabalho, outra planilha não pode ser criada com o mesmo nome.
