---
title: Limitações de instrução DELETE | Microsoft Docs
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
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caa4855c83815c8876c4674bf01de3f9c4bd4231
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="delete-statement-limitations"></a>EXCLUIR as limitações de instrução
Não há suporte para a instrução DELETE para o driver do Microsoft Excel ou texto. Observe que a instrução INSERT tem suporte para o driver de texto.  
  
 O driver dBASE não oferece suporte a uma tabela para remover valores "excluído" de remessa.  
  
 Para o driver Paradox excluir uma linha de uma tabela, a tabela deve ter um índice exclusivo (chave primária do Paradox).
