---
title: Limitações da instrução DELETE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 98bd56051c724186d7308eff669263d29b82ecd5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813824"
---
# <a name="delete-statement-limitations"></a>Limitações da instrução DELETE
Não há suporte para a instrução DELETE para o driver do Microsoft Excel ou texto. Observe que a instrução INSERT tem suporte para o driver de texto.  
  
 O driver do dBASE não oferece suporte a uma tabela para remover valores de "excluído" de remessa.  
  
 Para o driver do Paradox excluir uma linha de uma tabela, a tabela deve ter um índice exclusivo (chave primária do Paradox).
