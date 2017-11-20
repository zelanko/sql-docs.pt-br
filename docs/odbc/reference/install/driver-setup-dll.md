---
title: "DLL de instalação do driver | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing ODBC components [ODBC], driver setup DLL
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: 49bab021-81fa-402e-b7a4-a5214f1fadc4
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d75a8985feff2ddfe26d3e19e8bafd91f228d30e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="driver-setup-dll"></a>DLL de instalação do driver
> [!NOTE]  
>  Começando com o Windows XP e Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Instale somente explicitamente ODBC em versões anteriores do Windows.  
  
 A instalação do driver DLL contém o **ConfigDriver** e **ConfigDSN** funções. **ConfigDriver** executa tarefas de instalação específicas do driver, como inserir informações específicas do driver no registro. **ConfigDSN** mantém informações específicas sobre as fontes de dados no registro. Para obter uma descrição completa dessas funções, consulte [referência de API de DLL de instalação](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 **ConfigDSN** chama as funções a seguir no instalador do DLL para manter informações de fonte de dados no registro:  
  
-   **SQLWriteDSNToIni**. Adicione uma fonte de dados.  
  
-   **SQLRemoveDSNFromIni**. Exclua uma fonte de dados.  
  
-   **SQLWritePrivateProfileString**. Grave um valor específico do driver em uma subchave de especificação de fonte de dados.  
  
-   **SQLGetPrivateProfileString**. Ler um valor específico do driver de uma subchave de especificação de fonte de dados.  
  
-   **SQLGetTranslator**. Solicite ao usuário um nome de conversor e uma opção. Esta função chama **ConfigTranslator** no tradutor DLL de instalação.  
  
 A instalação do driver DLL é gravado pelo desenvolvedor do driver. Ele pode fazer parte do driver de DLL ou uma DLL separada.

