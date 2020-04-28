---
title: Usando os serviços de componentes da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], component services
- component services [ODBC]
ms.assetid: 06450562-d8f3-4987-b7bd-4a70223ff937
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb5763058fa198cbad7464434e31942ef8d6cd7d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307577"
---
# <a name="using-microsoft-component-services"></a>Usar os serviços de componentes da Microsoft
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Você pode habilitar um banco de dados Oracle para trabalhar com serviços de componentes transacionais (ou MTS, se você estiver usando o Windows NT) no Microsoft Windows NT/Windows 2000 e no Microsoft Windows 95/98. Para permitir que um banco de dados Oracle funcione com serviços de componentes que dão suporte a transações, os administradores de sistema devem criar uma exibição chamada V $ XATRANS $. Para criar esse script, você deve executar um script fornecido pela Oracle. Para obter mais informações, consulte a ajuda dos serviços de componentes ou a documentação do Oracle.
