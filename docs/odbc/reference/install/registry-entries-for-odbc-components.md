---
title: Inscrições de registro para componentes ODBC | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bead63f11b253342cd444e1d5bd0697ee00cfbc1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296166"
---
# <a name="registry-entries-for-odbc-components"></a>Entradas do Registro para componentes ODBC
> [!NOTE]  
>  Começando com o Windows XP e o Windows Server 2003, o ODBC está incluído no sistema operacional windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 O instalador DLL mantém informações no registro sobre cada componente ODBC instalado. Nos computadores que executam o Microsoft Windows NT e o Microsoft Windows 95/98, essas informações são armazenadas em subchaves sob a seguinte chave no registro:  

 ```console
 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\Odbcinst.ini
 ```

 Como o Odbcinst.ini é um subchave da árvore HKEY_LOCAL_MACHINE, as informações sobre os componentes do ODBC estão disponíveis para todos os usuários da máquina.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Subchave do núcleo ODBC](../../../odbc/reference/install/odbc-core-subkey.md)  
  
-   [Subchave de drivers ODBC](../../../odbc/reference/install/odbc-drivers-subkey.md)  
  
-   [Subchaves de especificação de driver](../../../odbc/reference/install/driver-specification-subkeys.md)  
  
-   [Subchave do driver padrão](../../../odbc/reference/install/default-driver-subkey.md)  
  
-   [Subchave de conversores ODBC](../../../odbc/reference/install/odbc-translators-subkey.md)  
  
-   [Subchaves de especificação do conversor](../../../odbc/reference/install/translator-specification-subkeys.md)
