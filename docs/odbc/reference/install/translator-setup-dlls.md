---
title: DLLs de configuração do tradutor | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296046"
---
# <a name="translator-setup-dlls"></a>DLLs de instalação do conversor
> [!NOTE]  
>  Começando com o Windows XP e o Windows Server 2003, o ODBC está incluído no sistema operacional windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 A configuração do tradutor DLL contém a função **ConfigTranslator,** que retorna a opção padrão para um tradutor. Se necessário, ele solicita ao usuário essas informações. Para obter uma descrição completa desta função, consulte [Configuração de referência de API DLL](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 A configuração do tradutor DLL é escrita pelo desenvolvedor do tradutor. Pode ser parte do DLL tradutor ou de um DLL separado.
