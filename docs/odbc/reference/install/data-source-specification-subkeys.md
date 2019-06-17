---
title: Subchaves de especificação de fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data source specification subkeys [ODBC]
- registry entries for data sources [ODBC], data source specification subkeys
- subkeys [ODBC], data source specification subkeys
ms.assetid: d7e88a07-e6ab-4258-a45d-1ca21234fbec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad210f91d00f9e692c8ee20fef01a808a01501c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63198211"
---
# <a name="data-source-specification-subkeys"></a>Subchaves de especificação de fonte de dados
Cada fonte de dados listado na subchave de fontes de dados ODBC tem uma subchave de seu próprio. Essa subchave tem o mesmo nome que o valor correspondente sob a subchave de fontes de dados ODBC. Os valores nessa subchave devem listar o DLL do driver e podem listar uma descrição da fonte de dados. Se o driver dá suporte a conversores, os valores podem listar o nome de um conversor padrão, a DLL de conversão padrão e a opção de conversão padrão. Os valores também podem listar outras informações necessárias pelo driver para se conectar à fonte de dados. Por exemplo, o driver pode exigir um nome do servidor, o nome do banco de dados ou o nome do esquema.  
  
 Os formatos de valores são conforme mostrado na tabela a seguir. Somente o valor do Driver é necessário.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|Descrição|REG_SZ|*description*|  
|Driver|REG_SZ|*driver-DLL-path*|  
|TranslationDLL|REG_SZ|*translator-DLL-path*|  
|TranslationName|REG_SZ|*translator-name*|  
|TranslationOption|REG_SZ|*translation-option*|  
|*opt-value-name*|*opt-value-type*|*opt-value-data*|  
  
 Por exemplo, suponha que o driver do SQL Server requer o nome do servidor e um sinalizador de OEM para a conversão de ANSI e define os valores de servidor e OEMTOANSI para eles. Vamos supor também que a fonte de dados de inventário usa a página de código do Microsoft® Translator para traduzir entre o Windows® Latin 1 (1250) e páginas de código multilíngue (850). Os valores sob a subchave de inventário podem ser da seguinte maneira:  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
