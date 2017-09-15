---
title: "Subchaves de especificação de fonte de dados | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data source specification subkeys [ODBC]
- registry entries for data sources [ODBC], data source specification subkeys
- subkeys [ODBC], data source specification subkeys
ms.assetid: d7e88a07-e6ab-4258-a45d-1ca21234fbec
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 61b485f55be504e894754f74c4ab779b9ebbaf5a
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="data-source-specification-subkeys"></a>Subchaves de especificação de fonte de dados
Cada fonte de dados listado na subchave fontes de dados ODBC tem uma subchave de seu próprio. Essa subchave tem o mesmo nome que o valor correspondente na subchave fontes de dados ODBC. Os valores sob essa subchave devem listar o DLL do driver e podem listar uma descrição da fonte de dados. Se o driver dá suporte a conversores, os valores podem listar o nome de um conversor de padrão, a DLL de conversão padrão e a opção de conversão padrão. Os valores também podem listar outras informações exigidas pelo driver para se conectar à fonte de dados. Por exemplo, o driver pode exigir um nome de servidor, o nome de banco de dados ou o nome do esquema.  
  
 Os formatos dos valores são conforme mostrado na tabela a seguir. Somente o valor do Driver é necessário.  
  
|Nome|Tipo de dados|data|  
|----------|---------------|----------|  
|Description|REG_SZ|*Descrição*|  
|Driver|REG_SZ|*caminho de DLL do driver*|  
|TranslationDLL|REG_SZ|*caminho de DLL do conversor*|  
|TranslationName|REG_SZ|*nome do conversor*|  
|TranslationOption|REG_SZ|*opção de conversão*|  
|*aceitar o valor-nome*|*aceitar-tipo de valor*|*dados aceitação de valor*|  
  
 Por exemplo, suponha que o driver do SQL Server requer o nome do servidor e um sinalizador de OEM para conversão de ANSI e define os valores de servidor e OEMTOANSI para eles. Suponha também que a fonte de dados de inventário usa o conversor de página de código do Microsoft® para converter entre o Windows® Latin 1 (1250) e páginas de código multilíngue (850). Os valores na subchave estoque podem ser como segue:  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
