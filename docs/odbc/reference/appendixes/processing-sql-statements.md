---
title: Processamento de declarações SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
ms.assetid: 54dad6a3-e86c-477b-ba7c-4e95e0385ec1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eda640f6e810eeccbfa17ea2b6ba7c1b19b28e08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307997"
---
# <a name="processing-sql-statements"></a>Processar instruções SQL
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 A biblioteca do cursor ODBC passa todas as instruções SQL diretamente para o driver, exceto as seguintes:  
  
-   Atualização posicionada e exclusão de declarações  
  
-   **SELECIONE PARA INSTRUÇÕES DE ATUALIZAÇÃO**  
  
-   Demonstrações SQL em lote  
  
 Para executar as instruções de atualização e exclusão posicionadas e posicionar o cursor em uma linha para chamar **SQLGetData** para essa linha, a biblioteca do cursor constrói uma instrução pesquisada que identifica a linha.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Processando instruções de atualização e exclusão posicionadas](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [Processando instruções SELECT FOR UPDATE](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [Processando lotes de instruções SQL](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [Construindo instruções pesquisadas](../../../odbc/reference/appendixes/constructing-searched-statements.md)
