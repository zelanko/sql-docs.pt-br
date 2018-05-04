---
title: Fontes de dados ODBC subchave | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23ca0ff3f499c23be9b46209d183a12e8ae92b25
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-data-sources-subkey"></a>Subchave de fontes de dados ODBC
Os valores na subchave fontes de dados ODBC listam as fontes de dados. O formato desses valores é conforme mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|data|  
|----------|---------------|----------|  
|*nome da fonte de dados*|REG_SZ|*Descrição do driver*|  
  
 O *nome da fonte de dados* valor é definido pelo programa de administração (que geralmente solicita ao usuário para que ele), e *descrição do driver* é definido pelo desenvolvedor de driver (normalmente é o nome das DBMS associado com o driver).  
  
 Por exemplo, suponha que três fontes de dados foram definidas: inventário, que usa o SQL Server; Folha de pagamento, que usa dBASE; e pessoal, que usa arquivos de texto com formatação. Os valores na subchave fontes de dados ODBC podem ser como segue:  
  
```  
Inventory : REG_SZ : SQL Server  
Payroll : REG_SZ : dBASE  
Personnel : REG_SZ : Text  
```
