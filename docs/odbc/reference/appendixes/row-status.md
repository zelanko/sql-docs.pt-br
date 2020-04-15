---
title: Status da linha | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- row status [ODBC]
- cache [ODBC]
ms.assetid: 0f0b1fb6-f697-4ced-811c-2908e210bc71
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d4ae4169dc3f2a491663f4a86c564cfee5c2f4d6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305095"
---
# <a name="row-status"></a>Status da linha
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 A biblioteca do cursor cria um buffer no cache para o status da linha. A biblioteca cursor recupera valores para a matriz de status da linha (especificada com o atributo de declaração SQL_ATTR_ROW_STATUS_PTR) deste buffer. Para cada linha, a biblioteca do cursor define este buffer como:  
  
-   SQL_ROW_DELETED quando executa uma declaração de exclusão posicionada na linha.  
  
-   SQL_ROW_ERROR quando encontra um erro recuperando a linha da fonte de dados com **o SQLFetch**.  
  
-   SQL_ROW_SUCCESS quando ele busca com sucesso a linha da fonte de dados com **SQLFetch**.  
  
-   SQL_ROW_UPDATED quando executa uma declaração de atualização posicionada na linha.
