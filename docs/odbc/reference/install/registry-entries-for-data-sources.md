---
title: Entradas do registro para fontes de dados | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: d5f5f865c0b50ea75548bb3a409caef8acf64b51
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692914"
---
# <a name="registry-entries-for-data-sources"></a>Entradas do Registro para fontes de dados
> [!NOTE]  
>  Começando com o Windows XP e Windows Server 2003, ODBC está incluído no sistema operacional Windows. Você deve instalar apenas explicitamente ODBC em versões anteriores do Windows.  
  
 A DLL do instalador mantém informações sobre cada fonte de dados do registro. No Microsoft Windows NT/Windows 2000 e no Microsoft Windows 95/98, essas informações são armazenadas em subchaves sob uma das seguintes duas chaves do registro:  
  
 HKEY_LOCAL_MACHINE  
  
 SOFTWARE  
  
 ODBC  
  
 INI  
  
 HKEY_CURRENT_USER  
  
 SOFTWARE  
  
 ODBC  
  
 INI  
  
 Qual chave é usado depende se a fonte de dados é um *fonte de dados do sistema* que está disponível para todos os usuários, ou um *fonte de dados do usuário,* que está disponível somente para o usuário atual. Fontes de dados do sistema são armazenadas na árvore de HKEY_LOCAL_MACHINE e fontes de dados do usuário são armazenadas na árvore de HKEY_CURRENT_USER. Em todos os outros aspectos, as fontes de dados do sistema e fontes de dados do usuário são idênticas.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Subchave de fontes de dados ODBC](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [Subchaves de especificação de fonte de dados](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [Subchave padrão](../../../odbc/reference/install/default-subkey.md)  
  
-   [Subchave do ODBC](../../../odbc/reference/install/odbc-subkey.md)
