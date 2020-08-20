---
description: DLLs de instalação do conversor
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
ms.openlocfilehash: 2fe4d514f098773024392666d8f528592d362da4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487389"
---
# <a name="translator-setup-dlls"></a>DLLs de instalação do conversor
> [!NOTE]  
>  A partir do Windows XP e do Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 A DLL de instalação do tradutor contém a função **ConfigTranslator** , que retorna a opção padrão para um tradutor. Se necessário, ele solicita essas informações ao usuário. Para obter uma descrição completa dessa função, consulte [Setup DLL API Reference](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 A DLL de instalação do tradutor é escrita pelo desenvolvedor do tradutor. Ele pode fazer parte da DLL do tradutor ou de uma DLL separada.
