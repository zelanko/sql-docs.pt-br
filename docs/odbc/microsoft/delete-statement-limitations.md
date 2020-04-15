---
title: DELETE Statement Limitações | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 365b54ab8c0678253e184b397f1f71e39aed3b9b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303527"
---
# <a name="delete-statement-limitations"></a>Limitações da instrução DELETE
A declaração DELETE não é suportada para o microsoft excel ou driver de texto. Observe que a instrução INSERT é suportada para o driver Texto.  
  
 O driver dBASE não suporta embalar uma tabela para remover valores "excluídos".  
  
 Para que o driver Paradoxo exclua uma linha de uma tabela, a tabela deve ter um índice único (chave primária paradoxo).
