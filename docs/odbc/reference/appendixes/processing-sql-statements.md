---
title: Processamento de instruções SQL | Microsoft Docs
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
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
ms.assetid: 54dad6a3-e86c-477b-ba7c-4e95e0385ec1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 603cb680e2986d484074a43d14f56de210da0b4a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="processing-sql-statements"></a>Processamento de instruções SQL
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 A biblioteca de cursores ODBC passa todas as instruções SQL diretamente para o driver exceto o seguinte:  
  
-   Posicionado atualização e exclusão de instruções  
  
-   **Selecione para atualização** instruções  
  
-   Instruções SQL em lote  
  
 Para executar a atualização posicionada e instruções delete e para posicionar o cursor em uma linha para chamar **SQLGetData** para aquela linha, a biblioteca de cursores constrói uma instrução pesquisada que identifica a linha.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Processando instruções de atualização e exclusão posicionadas](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [Processando instruções SELECT FOR UPDATE](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [Processando lotes de instruções SQL](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [Construindo instruções pesquisadas](../../../odbc/reference/appendixes/constructing-searched-statements.md)
