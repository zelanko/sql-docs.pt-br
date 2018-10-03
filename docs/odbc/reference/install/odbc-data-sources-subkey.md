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
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600864"
---
# <a name="odbc-data-sources-subkey"></a>Subchave de fontes de dados ODBC
Os valores sob a subchave de fontes de dados ODBC listam as fontes de dados. O formato desses valores é conforme mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|data|  
|----------|---------------|----------|  
|*nome da fonte de dados*|REG_SZ|*Descrição do driver*|  
  
 O *nome da fonte de dados* valor é definido pelo programa de administração (que normalmente solicita ao usuário para ele), e *descrição do driver* é definido pelo desenvolvedor de driver (geralmente é o nome das DBMS associado com o driver).  
  
 Por exemplo, suponha que três fontes de dados tiverem sido definidos: inventário, que usa o SQL Server; Folha de pagamento, que usa dBASE; e pessoal, que usa formatadas em arquivos de texto. Os valores sob a subchave de fontes de dados ODBC podem ser da seguinte maneira:  
  
```  
Inventory : REG_SZ : SQL Server  
Payroll : REG_SZ : dBASE  
Personnel : REG_SZ : Text  
```
