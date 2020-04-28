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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 617416adfcddfbf041c48acbf83cb9589e34ae27
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296216"
---
# <a name="odbc-translators-subkey"></a>Subchave de conversores ODBC
Os valores na subchave de conversores ODBC listam os tradutores instalados. O formato desses valores é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|*Tradutor-desc*|REG_SZ|**Instalada**|  
  
 O nome do *Tradutor-desc* é definido pelo desenvolvedor do tradutor.  
  
 Por exemplo, suponha que um usuário tenha instalado o tradutor de página de código do Microsoft® e um conversor ASCII personalizado para EBCDIC. Os valores na subchave de conversores ODBC podem ser os seguintes:  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
