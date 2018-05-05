---
title: DLLs de instalação do conversor | Microsoft Docs
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
- translator setup DLL [ODBC]
ms.assetid: b3ca79e9-01b9-4541-81de-bbbad24ca736
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 65eca03533940a50a169a948021342f71a032153
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="translator-setup-dlls"></a>DLLs de instalação do conversor
> [!NOTE]  
>  Começando com o Windows XP e Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Instale somente explicitamente ODBC em versões anteriores do Windows.  
  
 A instalação do tradutor DLL contém o **ConfigTranslator** função, que retorna a opção padrão para um conversor. Se necessário, ele solicita ao usuário essas informações. Para obter uma descrição completa dessa função, consulte [referência de API de DLL de instalação](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 A instalação do tradutor DLL é gravado pelo desenvolvedor do conversor. Ele pode fazer parte do tradutor DLL ou uma DLL separada.
