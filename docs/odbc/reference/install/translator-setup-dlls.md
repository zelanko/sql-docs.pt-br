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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b6c99dffc94f2675efdbbc3d5c1d142a5ae9b7e5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093845"
---
# <a name="translator-setup-dlls"></a>DLLs de instalação do conversor
> [!NOTE]  
>  A partir do Windows XP e do Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 A DLL de instalação do tradutor contém a função **ConfigTranslator** , que retorna a opção padrão para um tradutor. Se necessário, ele solicita essas informações ao usuário. Para obter uma descrição completa dessa função, consulte [Setup DLL API Reference](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 A DLL de instalação do tradutor é escrita pelo desenvolvedor do tradutor. Ele pode fazer parte da DLL do tradutor ou de uma DLL separada.
