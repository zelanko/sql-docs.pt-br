---
title: DLLs de instalação do conversor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- translator setup DLL [ODBC]
ms.assetid: b3ca79e9-01b9-4541-81de-bbbad24ca736
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2aabec831ba9b623a24f261551684e9bb259e24
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="translator-setup-dlls"></a>DLLs de instalação do conversor
> [!NOTE]  
>  Começando com o Windows XP e Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Instale somente explicitamente ODBC em versões anteriores do Windows.  
  
 A instalação do tradutor DLL contém o **ConfigTranslator** função, que retorna a opção padrão para um conversor. Se necessário, ele solicita ao usuário essas informações. Para obter uma descrição completa dessa função, consulte [referência de API de DLL de instalação](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 A instalação do tradutor DLL é gravado pelo desenvolvedor do conversor. Ele pode fazer parte do tradutor DLL ou uma DLL separada.
