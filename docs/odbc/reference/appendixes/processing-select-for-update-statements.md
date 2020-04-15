---
title: Processamento SELECT PARA ATUALIZAÇÕES Declarações | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81308007"
---
# <a name="processing-select-for-update-statements"></a>Processar instruções SELECT FOR UPDATE
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Para a interoperabilidade máxima, os aplicativos devem gerar conjuntos de resultados que serão atualizados com uma declaração de atualização posicionada executando uma declaração **SELECT FOR UPDATE.** Embora a biblioteca do cursor não exija isso, ela é exigida pela maioria das fontes de dados que suportam instruções de atualização posicionadas.  
  
 A biblioteca do cursor ignora as colunas na cláusula **FOR UPDATE** de uma declaração SELECT **FOR UPDATE;** ele remove esta cláusula antes de passar a declaração para o motorista. Na biblioteca do cursor, o atributo de declaração SQL_ATTR_CONCURRENCY, juntamente com as restrições mencionadas na seção anterior, controla se as colunas em um conjunto de resultados podem ser atualizadas.
