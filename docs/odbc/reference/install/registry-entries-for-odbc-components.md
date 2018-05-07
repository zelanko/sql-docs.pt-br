---
title: Entradas do registro para componentes ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- installing ODBC components [ODBC], registry entries
- registry entries for components [ODBC]
- subkeys [ODBC], for components
- registry entries for components [ODBC], about registry entries
ms.assetid: c90aa8a4-6ece-48de-901c-17d23739a9ff
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4cf61535ecda3e95f25dbd9e1b01a1d3ad25d4ab
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="registry-entries-for-odbc-components"></a>Entradas do registro para componentes ODBC
> [!NOTE]  
>  Começando com o Windows XP e Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Instale somente explicitamente ODBC em versões anteriores do Windows.  
  
 O instalador DLL mantém informações no registro sobre cada componente do ODBC instalado. Em computadores que executam o Microsoft Windows NT e o Microsoft Windows 95/98, essas informações são armazenadas em subchaves na seguinte chave no registro:  
  
 HKEY_LOCAL_MACHINE  
  
 SOFTWARE  
  
 ODBC  
  
 Odbcinst.ini  
  
 Como uma subchave da árvore HKEY_LOCAL_MACHINE Odbcinst.ini, as informações sobre componentes ODBC estão disponíveis para todos os usuários da máquina.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Subchave do núcleo ODBC](../../../odbc/reference/install/odbc-core-subkey.md)  
  
-   [Subchave de drivers ODBC](../../../odbc/reference/install/odbc-drivers-subkey.md)  
  
-   [Subchaves de especificação de driver](../../../odbc/reference/install/driver-specification-subkeys.md)  
  
-   [Subchave do driver padrão](../../../odbc/reference/install/default-driver-subkey.md)  
  
-   [Subchave de conversores ODBC](../../../odbc/reference/install/odbc-translators-subkey.md)  
  
-   [Subchaves de especificação do conversor](../../../odbc/reference/install/translator-specification-subkeys.md)
