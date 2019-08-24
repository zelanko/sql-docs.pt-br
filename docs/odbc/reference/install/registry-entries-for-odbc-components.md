---
title: Entradas de registro para componentes ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- installing ODBC components [ODBC], registry entries
- registry entries for components [ODBC]
- subkeys [ODBC], for components
- registry entries for components [ODBC], about registry entries
ms.assetid: c90aa8a4-6ece-48de-901c-17d23739a9ff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cbee5187a7318e0953ea61d92f7478d83e5afaff
ms.sourcegitcommit: 594cee116fa4ee321e1f5e5206f4a94d408f1576
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2019
ms.locfileid: "70009342"
---
# <a name="registry-entries-for-odbc-components"></a>Entradas do Registro para componentes ODBC
> [!NOTE]  
>  A partir do Windows XP e do Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 A DLL do instalador mantém informações no registro sobre cada componente ODBC instalado. Em computadores que executam o Microsoft Windows NT e o Microsoft Windows 95/98, essas informações são armazenadas em subchaves sob a seguinte chave no registro:  

 ```console
 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\Odbcinst.ini
 ```

 Como o Odbcinst. ini é uma subchave da árvore HKEY_LOCAL_MACHINE, as informações sobre os componentes ODBC estão disponíveis para todos os usuários do computador.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Subchave do núcleo ODBC](../../../odbc/reference/install/odbc-core-subkey.md)  
  
-   [Subchave de drivers ODBC](../../../odbc/reference/install/odbc-drivers-subkey.md)  
  
-   [Subchaves de especificação de driver](../../../odbc/reference/install/driver-specification-subkeys.md)  
  
-   [Subchave do driver padrão](../../../odbc/reference/install/default-driver-subkey.md)  
  
-   [Subchave de conversores ODBC](../../../odbc/reference/install/odbc-translators-subkey.md)  
  
-   [Subchaves de especificação do conversor](../../../odbc/reference/install/translator-specification-subkeys.md)
