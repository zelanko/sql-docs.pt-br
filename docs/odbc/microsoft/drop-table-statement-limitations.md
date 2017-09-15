---
title: "Limitações de declaração de tabela DROP | Microsoft Docs"
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
- ODBC SQL grammar, DROP TABLE statement limitations
- DROP TABLE statement limitations [ODBC]
ms.assetid: 0a1c80f5-c9f2-4655-9bfd-0131b2f015a9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 65c47ece213312b749dee0e83b76e8de89cf3dc9
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="drop-table-statement-limitations"></a>Remover tabela limitações de instrução
Quando o driver do Microsoft Excel 5.0, 7.0 ou 97 é usado, a instrução DROP TABLE limpa a planilha, mas não exclui o nome da planilha. Porque o nome da planilha ainda existe na pasta de trabalho, outra planilha não pode ser criada com o mesmo nome.
