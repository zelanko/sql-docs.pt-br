---
title: Inscrições de Registro para Fontes de Dados | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c73ea704b091bc37afb1ac42b520304022d929c3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296266"
---
# <a name="registry-entries-for-data-sources"></a>Entradas do Registro para fontes de dados
> [!NOTE]  
>  Começando com o Windows XP e o Windows Server 2003, o ODBC está incluído no sistema operacional windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 O instalador DLL mantém informações no registro sobre cada fonte de dados. No Microsoft Windows NT/Windows 2000 e no Microsoft Windows 95/98, essas informações são armazenadas em subchaves sob uma das duas chaves a seguir no registro:  

 ```console
 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\Odbc.ini  
 ```

 ```console
 HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini
 ```

 Qual chave é usada depende se a fonte de dados é uma *fonte de dados do sistema,* que está disponível para todos os usuários, ou uma fonte de dados do *usuário,* que está disponível apenas para o usuário atual. As fontes de dados do sistema são armazenadas na árvore HKEY_LOCAL_MACHINE e as fontes de dados do usuário são armazenadas na árvore HKEY_CURRENT_USER. Em todos os outros aspectos, as fontes de dados do sistema e as fontes de dados do usuário são idênticas.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Subchave de fontes de dados ODBC](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [Subchaves de especificação de fonte de dados](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [Subchave padrão](../../../odbc/reference/install/default-subkey.md)  
  
-   [Subchave do ODBC](../../../odbc/reference/install/odbc-subkey.md)
