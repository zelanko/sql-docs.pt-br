---
title: Entradas do registro para fontes de dados | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC]
- data sources [ODBC], registry entries
- registry entries for data sources [ODBC], about registry entries
- data sources [ODBC], configuring
- registry entries for data sources [ODBC]
ms.assetid: 78aaa3d3-d081-4550-80e3-720c910d5996
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fe69d4c897491166a632bbc38f466aadfb9a1e63
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="registry-entries-for-data-sources"></a>Entradas do registro para fontes de dados
> [!NOTE]  
>  Começando com o Windows XP e Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Instale somente explicitamente ODBC em versões anteriores do Windows.  
  
 O instalador DLL mantém informações sobre cada fonte de dados do registro. No Microsoft Windows NT/Windows 2000 e Microsoft Windows 95/98, essas informações são armazenadas em subchaves em uma das seguintes duas chaves do registro:  
  
 HKEY_LOCAL_MACHINE  
  
 SOFTWARE  
  
 ODBC  
  
 ODBC.ini  
  
 HKEY_CURRENT_USER  
  
 SOFTWARE  
  
 ODBC  
  
 ODBC.ini  
  
 Qual chave é usada depende se a fonte de dados é um *fonte de dados do sistema,* que está disponível para todos os usuários, ou um *fonte de dados de usuário,* que está disponível somente para o usuário atual. Fontes de dados do sistema são armazenados na árvore de HKEY_LOCAL_MACHINE e fontes de dados do usuário são armazenadas na árvore de HKEY_CURRENT_USER. Em todos os outros aspectos, fontes de dados do sistema e fontes de dados de usuário são idênticas.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Subchave de fontes de dados ODBC](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [Subchaves de especificação de fonte de dados](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [Subchave padrão](../../../odbc/reference/install/default-subkey.md)  
  
-   [Subchave do ODBC](../../../odbc/reference/install/odbc-subkey.md)
