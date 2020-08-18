---
description: Notas da implementação
title: Notas de implementação | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7ec14b9c-69b8-4c6e-838a-88d1ebdc8725
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7117e0d8af856a16a47414f5a8c3ec11c475cb92
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483259"
---
# <a name="implementation-notes"></a>Notas da implementação
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Esta seção descreve como a biblioteca de cursores ODBC é implementada. Ele descreve como a biblioteca de cursores mantém seu cache, executa instruções SQL e implementa funções ODBC.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Cache de biblioteca de cursores](../../../odbc/reference/appendixes/cursor-library-cache.md)  
  
-   [Processando instruções SQL](../../../odbc/reference/appendixes/processing-sql-statements.md)  
  
-   [Funções ODBC e a biblioteca de cursores](../../../odbc/reference/appendixes/odbc-functions-and-the-cursor-library.md)
