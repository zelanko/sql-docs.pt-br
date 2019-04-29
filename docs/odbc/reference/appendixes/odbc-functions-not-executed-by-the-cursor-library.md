---
title: Funções ODBC não executadas pela biblioteca de cursores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursor library [ODBC], functions
- functions [ODBC], cursor library
- ODBC functions [ODBC], cursor library
- ODBC cursor library [ODBC], functions
ms.assetid: f2941522-75eb-4db9-9468-4800b884dac2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e3daee4ea5f5d46ecf0e7490e1d2e82303dd8a4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63018373"
---
# <a name="odbc-functions-not-executed-by-the-cursor-library"></a>Funções ODBC não executadas pela biblioteca de cursores
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 A biblioteca de cursores não executa as seguintes funções. Quando um aplicativo chama uma dessas funções, o Gerenciador de Driver invoca o driver, não a biblioteca de cursores.  
  
|||  
|-|-|  
|**SQLFetch**|**SQLGetEnvAttr**|  
|**SQLGetConnectAttr**|**SQLSetDescRec**|  
|**SQLGetDiagField**|**SQLSetEnvAttr**|  
|**SQLGetDiagRec**||
