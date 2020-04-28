---
title: Processando instruções SELECT FOR UPDATE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], select for update statements
- select for update [ODBC]
- SQL statements [ODBC], cursor library
- cursor library [ODBC], select for update statements
- ODBC cursor library [ODBC], select for update statements
- cursor library [ODBC], statement processing
ms.assetid: 8d2e79a4-5daf-458e-a536-d8b6e588753e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 904028cd7b3798fcac8f9e5afa6186fae3e9fa29
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81308007"
---
# <a name="processing-select-for-update-statements"></a>Processar instruções SELECT FOR UPDATE
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Para obter a interoperabilidade máxima, os aplicativos devem gerar conjuntos de resultados que serão atualizados com uma instrução UPDATE posicionada executando uma instrução **SELECT for Update** . Embora a biblioteca de cursores não exija isso, ela é exigida pela maioria das fontes de dados que dão suporte a instruções UPDATE posicionadas.  
  
 A biblioteca de cursores ignora as colunas na cláusula **for Update** de uma instrução **SELECT for Update** ; Ele remove essa cláusula antes de passar a instrução para o driver. Na biblioteca de cursores, o atributo de instrução SQL_ATTR_CONCURRENCY, junto com as restrições mencionadas na seção anterior, controla se as colunas em um conjunto de resultados podem ser atualizadas.
