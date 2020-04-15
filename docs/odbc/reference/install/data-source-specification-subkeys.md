---
title: Subtectas de especificação de fonte de dados | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300336"
---
# <a name="data-source-specification-subkeys"></a>Subchaves de especificação de fonte de dados
Cada fonte de dados listada na subchave Fontes de Dados oDBC tem uma subchave própria. Esta subchave tem o mesmo nome do valor correspondente sob a sub-chave ODBC Data Sources. Os valores sob esta subchave devem listar o Driver DLL e podem listar uma descrição da fonte de dados. Se o driver tiver suporte a tradutores, os valores poderão listar o nome de um tradutor padrão, a DLL de tradução padrão e a opção de tradução padrão. Os valores também podem listar outras informações exigidas pelo motorista para se conectar à fonte de dados. Por exemplo, o driver pode exigir um nome de servidor, nome do banco de dados ou nome do esquema.  
  
 Os formatos dos valores são mostrados na tabela a seguir. Apenas o valor do Driver é necessário.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|Descrição|REG_SZ|*Descrição*|  
|Driver|REG_SZ|*driver-DLL-path*|  
|TraduçãoDLL|REG_SZ|*tradutor-DLL-caminho*|  
|Nome da tradução|REG_SZ|*nome do tradutor*|  
|Translationoption|REG_SZ|*tradução-opção*|  
|*nome de valor de opção*|*tipo de valor de opt*|*opt-value-data*|  
  
 Por exemplo, suponha que o driver sql server exija o nome do servidor e um sinalizador para conversão De OEM para ANSI e define os valores servidor e OEMTOANSI para estes. Suponha também que a fonte de dados de inventário use o Tradutor de Página de Código ® Microsoft para traduzir entre as páginas de código Windows® Latin 1 (1250) e Multilíndüál (850). Os valores sob a sub-tecla Inventário podem ser os seguintes:  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
