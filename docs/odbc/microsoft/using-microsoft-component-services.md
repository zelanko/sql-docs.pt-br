---
description: Usar os serviços de componentes da Microsoft
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
ms.openlocfilehash: 8214b706394c9fe8e2b8a6fd2491156292475fa9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471338"
---
# <a name="using-microsoft-component-services"></a>Usar os serviços de componentes da Microsoft
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Você pode habilitar um banco de dados Oracle para trabalhar com serviços de componentes transacionais (ou MTS, se você estiver usando o Windows NT) no Microsoft Windows NT/Windows 2000 e no Microsoft Windows 95/98. Para permitir que um banco de dados Oracle funcione com serviços de componentes que dão suporte a transações, os administradores de sistema devem criar uma exibição chamada V $ XATRANS $. Para criar esse script, você deve executar um script fornecido pela Oracle. Para obter mais informações, consulte a ajuda dos serviços de componentes ou a documentação do Oracle.
