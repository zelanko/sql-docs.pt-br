---
title: Entradas de registro para fontes de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- data sources [ODBC], registry entries
- registry entries for data sources [ODBC], about registry entries
- data sources [ODBC], configuring
- registry entries for data sources [ODBC]
ms.assetid: 78aaa3d3-d081-4550-80e3-720c910d5996
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1fe76ba3926f2883e2518e255eddf0d567134f4d
ms.sourcegitcommit: 594cee116fa4ee321e1f5e5206f4a94d408f1576
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2019
ms.locfileid: "70009352"
---
# <a name="registry-entries-for-data-sources"></a>Entradas do Registro para fontes de dados
> [!NOTE]  
>  A partir do Windows XP e do Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 A DLL do instalador mantém informações no registro sobre cada fonte de dados. No Microsoft Windows NT/Windows 2000 e no Microsoft Windows 95/98, essas informações são armazenadas em subchaves em uma das duas chaves a seguir no registro:  

 ```console
 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\Odbc.ini  
 ```

 ```console
 HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini
 ```

 Qual chave é usada depende se a fonte de dados é uma *fonte de dados do sistema,* que está disponível para todos os usuários ou uma *fonte de dados do usuário,* que está disponível somente para o usuário atual. As fontes de dados do sistema são armazenadas na árvore HKEY_LOCAL_MACHINE e as fontes de dados do usuário são armazenadas na árvore HKEY_CURRENT_USER. Em todos os outros aspectos, as fontes de dados do sistema e as fontes de dados do usuário são idênticas.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Subchave de fontes de dados ODBC](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [Subchaves de especificação de fonte de dados](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [Subchave padrão](../../../odbc/reference/install/default-subkey.md)  
  
-   [Subchave do ODBC](../../../odbc/reference/install/odbc-subkey.md)
