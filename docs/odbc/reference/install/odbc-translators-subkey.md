---
title: Subchave de conversores ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- subkeys [ODBC], translator subkey
- registry entries for components [ODBC], translator subkey
ms.assetid: 6b170f1f-e263-4aac-9d49-8d0ca0470ca2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e7109a6f1b88cf7639b2fc823ce0c5f14d05002
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280786"
---
# <a name="odbc-translators-subkey"></a>Subchave de conversores ODBC
Os valores sob a subchave de conversores ODBC listam os tradutores instalados. O formato desses valores é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|*translator-desc*|REG_SZ|**instalado**|  
  
 O *tradutor desc* nome é definido pelo desenvolvedor do conversor.  
  
 Por exemplo, suponha que um usuário tiver instalado o conversor de página de código do Microsoft® e um ASCII personalizado ao translator EBCDIC. Os valores sob a subchave de conversores ODBC podem ser da seguinte maneira:  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
