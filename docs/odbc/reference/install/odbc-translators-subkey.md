---
description: Subchave de conversores ODBC
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46308518f1f806cea21bbb824312d5269f8b61e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499709"
---
# <a name="odbc-translators-subkey"></a>Subchave de conversores ODBC
Os valores na subchave de conversores ODBC listam os tradutores instalados. O formato desses valores é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|*Tradutor-desc*|REG_SZ|**Instalado**|  
  
 O nome do *Tradutor-desc* é definido pelo desenvolvedor do tradutor.  
  
 Por exemplo, suponha que um usuário tenha instalado o tradutor de página de código do Microsoft® e um conversor ASCII personalizado para EBCDIC. Os valores na subchave de conversores ODBC podem ser os seguintes:  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
