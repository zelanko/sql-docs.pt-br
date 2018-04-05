---
title: DLLs de instalação do conversor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- translator setup DLL [ODBC]
ms.assetid: b3ca79e9-01b9-4541-81de-bbbad24ca736
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3ce6961ec470bf0e0a7281a129d85f5cf69c9b80
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="translator-setup-dlls"></a>DLLs de instalação do conversor
> [!NOTE]  
>  Começando com o Windows XP e Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Instale somente explicitamente ODBC em versões anteriores do Windows.  
  
 A instalação do tradutor DLL contém o **ConfigTranslator** função, que retorna a opção padrão para um conversor. Se necessário, ele solicita ao usuário essas informações. Para obter uma descrição completa dessa função, consulte [referência de API de DLL de instalação](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 A instalação do tradutor DLL é gravado pelo desenvolvedor do conversor. Ele pode fazer parte do tradutor DLL ou uma DLL separada.
