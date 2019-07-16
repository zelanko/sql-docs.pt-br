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
ms.openlocfilehash: 7d26f2d33d81e08cfe4bddff9b2260bd2f098f00
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093937"
---
# <a name="odbc-translators-subkey"></a>Subchave de conversores ODBC
Os valores sob a subchave de conversores ODBC listam os tradutores instalados. O formato desses valores é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Data|  
|----------|---------------|----------|  
|*translator-desc*|REG_SZ|**instalado**|  
  
 O *tradutor desc* nome é definido pelo desenvolvedor do conversor.  
  
 Por exemplo, suponha que um usuário tiver instalado o conversor de página de código do Microsoft® e um ASCII personalizado ao translator EBCDIC. Os valores sob a subchave de conversores ODBC podem ser da seguinte maneira:  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
