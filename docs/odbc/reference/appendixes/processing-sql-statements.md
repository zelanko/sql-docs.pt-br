---
title: Processando instruções SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d9452ade90f6967dff6d72d5692efcf91b93154d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057238"
---
# <a name="processing-sql-statements"></a>Processar instruções SQL
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 A biblioteca de cursores ODBC passa todas as instruções SQL diretamente para o driver, exceto o seguinte:  
  
-   Posicionado atualização e instruções delete  
  
-   **SELECT FOR UPDATE** instruções  
  
-   Instruções SQL em lote  
  
 Para executar a atualização posicionadas e instruções delete e posicionar o cursor em uma linha para chamar **SQLGetData** para aquela linha, a biblioteca de cursores constrói uma instrução pesquisada que identifica a linha.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Processando instruções de atualização e exclusão posicionadas](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [Processando instruções SELECT FOR UPDATE](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [Processando lotes de instruções SQL](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [Construindo instruções pesquisadas](../../../odbc/reference/appendixes/constructing-searched-statements.md)
