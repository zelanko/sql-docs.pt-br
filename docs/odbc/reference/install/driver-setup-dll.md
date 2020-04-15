---
title: Configuração do driver DLL | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0a2878591c92fe0b2070a295d9dc622c245c17e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306417"
---
# <a name="driver-setup-dll"></a>DLL de instalação do driver
> [!NOTE]  
>  Começando com o Windows XP e o Windows Server 2003, o ODBC está incluído no sistema operacional windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 A configuração do driver DLL contém as funções **ConfigDriver** e **ConfigDSN.** **O ConfigDriver** executa tarefas de instalação específicas do driver, como inserir informações específicas do driver no registro. **O ConfigDSN** mantém informações específicas do driver sobre fontes de dados no registro. Para obter uma descrição completa dessas funções, consulte [Configuração de referência de API DLL](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 **O ConfigDSN** chama as seguintes funções no instalador DLL para manter as informações de origem de dados no registro:  
  
-   **SQLWriteDSNToIni**. Adicione uma fonte de dados.  
  
-   **SQLRemoveDSNFromIni**. Exclua uma fonte de dados.  
  
-   **SQLWritePrivateProfilestring**. Escreva um valor específico do driver em uma subchave de especificação de origem de dados.  
  
-   **SqlgetPrivateProfilestring**. Leia um valor específico do driver a partir de uma subchave de especificação de origem de dados.  
  
-   **SQLGetTranslator**. Solicitar ao usuário um nome e opção de tradutor. Esta função chama **ConfigTranslator** na configuração de tradutor DLL.  
  
 A configuração do driver DLL é escrita pelo desenvolvedor do driver. Pode ser parte do driver DLL ou um DLL separado.
