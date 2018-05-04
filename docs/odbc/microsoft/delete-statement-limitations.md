---
title: Limitações de instrução DELETE | Microsoft Docs
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
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c731ba4a7482e981e0674c5d108115fc0960cd9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="delete-statement-limitations"></a>EXCLUIR as limitações de instrução
Não há suporte para a instrução DELETE para o driver do Microsoft Excel ou texto. Observe que a instrução INSERT tem suporte para o driver de texto.  
  
 O driver dBASE não oferece suporte a uma tabela para remover valores "excluído" de remessa.  
  
 Para o driver Paradox excluir uma linha de uma tabela, a tabela deve ter um índice exclusivo (chave primária do Paradox).
