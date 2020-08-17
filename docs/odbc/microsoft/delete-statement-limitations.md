---
description: Limitações da instrução DELETE
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5ffb3a6d0ab28fc2b8bc8785df586ac6bbc86aa0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340892"
---
# <a name="delete-statement-limitations"></a>Limitações da instrução DELETE
A instrução DELETE não tem suporte para o Microsoft Excel ou o driver de texto. Observe que a instrução INSERT tem suporte para o driver de texto.  
  
 O driver do dBASE não oferece suporte a empacotamento de uma tabela para remover valores "excluídos".  
  
 Para que o driver do Paradox exclua uma linha de uma tabela, a tabela deve ter um índice exclusivo (chave primária do Paradox).
