---
title: Subchave de fontes de dados ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9867946ce84163a504582c8a9575100c3c9aacd3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63069815"
---
# <a name="odbc-data-sources-subkey"></a>Subchave de fontes de dados ODBC
Os valores sob a subchave de fontes de dados ODBC listam as fontes de dados. O formato desses valores é conforme mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|*data-source-name*|REG_SZ|*driver-description*|  
  
 O *nome da fonte de dados* valor é definido pelo programa de administração (que normalmente solicita ao usuário para ele), e *descrição do driver* é definido pelo desenvolvedor de driver (geralmente é o nome das DBMS associado com o driver).  
  
 Por exemplo, suponha que três fontes foram definidas de dados: Inventário, que usa o SQL Server; Folha de pagamento, que usa dBASE; e pessoal, que usa formatadas em arquivos de texto. Os valores sob a subchave de fontes de dados ODBC podem ser da seguinte maneira:  
  
```  
Inventory : REG_SZ : SQL Server  
Payroll : REG_SZ : dBASE  
Personnel : REG_SZ : Text  
```
