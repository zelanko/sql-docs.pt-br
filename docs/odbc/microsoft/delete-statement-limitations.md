---
title: "Limitações de instrução DELETE | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 767008325089473195f4ceb6f71c54d4e1890090
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="delete-statement-limitations"></a>EXCLUIR as limitações de instrução
Não há suporte para a instrução DELETE para o driver do Microsoft Excel ou texto. Observe que a instrução INSERT tem suporte para o driver de texto.  
  
 O driver dBASE não oferece suporte a uma tabela para remover valores "excluído" de remessa.  
  
 Para o driver Paradox excluir uma linha de uma tabela, a tabela deve ter um índice exclusivo (chave primária do Paradox).
