---
title: DLL de instalação do driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], driver setup DLL
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: 49bab021-81fa-402e-b7a4-a5214f1fadc4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 088c9b60861266bf99649343aec2e763097bf155
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198198"
---
# <a name="driver-setup-dll"></a>DLL de instalação do driver
> [!NOTE]  
>  Começando com o Windows XP e Windows Server 2003, ODBC está incluído no sistema operacional Windows. Você deve instalar apenas explicitamente ODBC em versões anteriores do Windows.  
  
 A instalação do driver DLL contém o **ConfigDriver** e **ConfigDSN** funções. **ConfigDriver** executa tarefas de instalação específicas do driver, como inserir informações específicas de driver no registro. **ConfigDSN** mantém informações específicas de driver sobre fontes de dados no registro. Para obter uma descrição completa dessas funções, consulte [referência de API de DLL de instalação](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 **ConfigDSN** chama as funções a seguir no instalador do DLL para manter informações de fonte de dados no registro:  
  
-   **SQLWriteDSNToIni**. Adicione uma fonte de dados.  
  
-   **SQLRemoveDSNFromIni**. Exclua uma fonte de dados.  
  
-   **SQLWritePrivateProfileString**. Grava um valor específico do driver em uma subchave de especificação de fonte de dados.  
  
-   **SQLGetPrivateProfileString**. Ler um valor específico do driver de uma subchave de especificação de fonte de dados.  
  
-   **SQLGetTranslator**. Solicita ao usuário um nome de tradução e uma opção. Essa função chama **ConfigTranslator** no tradutor DLL de instalação.  
  
 A instalação do driver DLL é escrito pelo desenvolvedor de driver. Ele pode fazer parte do driver de DLL ou uma DLL separada.
