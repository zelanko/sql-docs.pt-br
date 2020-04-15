---
title: Subchave de Tradutores ODBC | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 617416adfcddfbf041c48acbf83cb9589e34ae27
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296216"
---
# <a name="odbc-translators-subkey"></a>Subchave de conversores ODBC
Os valores sob a sub-chave ODBC Translators listam os tradutores instalados. O formato desses valores é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|*tradutor-desc*|REG_SZ|**Instalado**|  
  
 O nome *tradutor-desc* é definido pelo desenvolvedor do tradutor.  
  
 Por exemplo, suponha que um usuário tenha instalado o Microsoft® Code Page Translator e um ASCII personalizado para tradutor EBCDIC. Os valores sob a sub-chave Tradutores ODBC podem ser os seguintes:  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
