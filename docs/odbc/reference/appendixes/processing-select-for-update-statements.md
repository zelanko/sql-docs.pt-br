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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f54d31426773f294a4a23f059c9f906d430056f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47721754"
---
# <a name="processing-select-for-update-statements"></a>Processar instruções SELECT FOR UPDATE
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Para interoperabilidade máxima, aplicativos devem gerar conjuntos de resultados serão atualizados com uma instrução de atualização posicionada, executando uma **Selecione para atualizar** instrução. Embora a biblioteca de cursores não requer isso, ele é necessário para a maioria das fontes de dados que dão suporte a instruções update posicionadas.  
  
 A biblioteca de cursores ignora as colunas na **FOR UPDATE** cláusula de uma **SELECT FOR UPDATE** instrução; ele remove essa cláusula antes de passar a instrução para o driver. Na biblioteca de cursor, o atributo de instrução SQL_ATTR_CONCURRENCY, junto com as restrições mencionadas na seção anterior, controles se as colunas em um resultado definido podem ser atualizados.
