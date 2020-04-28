---
title: Subchaves de especificação da fonte de dados | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 281377c307f3f3750e87bf5dc988beb7660067af
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300336"
---
# <a name="data-source-specification-subkeys"></a>Subchaves de especificação de fonte de dados
Cada fonte de dados listada na subchave de fontes de dados ODBC tem uma subchave própria. Essa subchave tem o mesmo nome que o valor correspondente na subchave fontes de dados ODBC. Os valores nessa subchave devem listar a DLL do driver e podem listar uma descrição da fonte de dados. Se o driver oferecer suporte a tradutores, os valores poderão listar o nome de um tradutor padrão, a DLL de tradução padrão e a opção de conversão padrão. Os valores também podem listar outras informações exigidas pelo driver para se conectar à fonte de dados. Por exemplo, o driver pode exigir um nome de servidor, nome de banco de dados ou nome de esquema.  
  
 Os formatos dos valores são mostrados na tabela a seguir. Somente o valor do driver é necessário.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|Descrição|REG_SZ|*ndescrição*|  
|Driver|REG_SZ|*Driver-DLL-caminho*|  
|TranslationDLL|REG_SZ|*Tradutor-DLL-caminho*|  
|Conversão de|REG_SZ|*nome do Tradutor*|  
|TranslationOption|REG_SZ|*opção de tradução*|  
|*nome de consentimento*|*tipo de aceitação de valor*|*dados de aceitação/valor*|  
  
 Por exemplo, suponha que o driver SQL Server exija o nome do servidor e um sinalizador para conversão de OEM para ANSI e defina os valores de servidor e OEMTOANSI para eles. Suponha também que a fonte de dados de inventário use o conversor de página de código do Microsoft® para converter entre as páginas de código do Windows® Latin 1 (1250) e multilíngue (850). Os valores na subchave de inventário podem ser os seguintes:  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
