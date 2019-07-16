---
title: Status de linha | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a62bad0e69a8bf8b5365575f97e4791cbbf270d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057112"
---
# <a name="row-status"></a>Status da linha
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 A biblioteca de cursores cria um buffer em cache para o status de linha. A biblioteca de cursores recupera os valores para a matriz de status de linha (especificado com o atributo da instrução SQL_ATTR_ROW_STATUS_PTR) desse buffer. Para cada linha, a biblioteca de cursores define esse buffer como:  
  
-   SQL_ROW_DELETED quando ele executa um posicionadas Excluir instrução na linha.  
  
-   SQL_ROW_ERROR quando encontra um erro ao recuperar a linha da fonte de dados com **SQLFetch**.  
  
-   SQL_ROW_SUCCESS quando ele busca com êxito a linha da fonte de dados com **SQLFetch**.  
  
-   SQL_ROW_UPDATED quando ele executa uma instrução de atualização posicionada na linha.
