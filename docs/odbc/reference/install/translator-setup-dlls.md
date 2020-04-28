---
title: DLLs de instalação do Tradutor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator setup DLL [ODBC]
ms.assetid: b3ca79e9-01b9-4541-81de-bbbad24ca736
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 28c354fddb36b9e035361fa4ba03fbde34b7d399
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296046"
---
# <a name="translator-setup-dlls"></a>DLLs de instalação do conversor
> [!NOTE]  
>  A partir do Windows XP e do Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 A DLL de instalação do tradutor contém a função **ConfigTranslator** , que retorna a opção padrão para um tradutor. Se necessário, ele solicita essas informações ao usuário. Para obter uma descrição completa dessa função, consulte [Setup DLL API Reference](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 A DLL de instalação do tradutor é escrita pelo desenvolvedor do tradutor. Ele pode fazer parte da DLL do tradutor ou de uma DLL separada.
