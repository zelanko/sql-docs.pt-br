---
title: Fontes de dados ODBC subchave | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3141bf0b16c6be579bf76a77b13e240ad5befef4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
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
