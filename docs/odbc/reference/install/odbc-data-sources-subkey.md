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
ms.openlocfilehash: 2a1d0c506c4a4b33d7138378032947821d4e9f3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093987"
---
# <a name="odbc-data-sources-subkey"></a>Subchave de fontes de dados ODBC
Os valores sob a subchave de fontes de dados ODBC listam as fontes de dados. O formato desses valores é conforme mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Data|  
|----------|---------------|----------|  
|*data-source-name*|REG_SZ|*driver-description*|  
  
 O *nome da fonte de dados* valor é definido pelo programa de administração (que normalmente solicita ao usuário para ele), e *descrição do driver* é definido pelo desenvolvedor de driver (geralmente é o nome das DBMS associado com o driver).  
  
 Por exemplo, suponha que três fontes foram definidas de dados: Inventário, que usa o SQL Server; Folha de pagamento, que usa dBASE; e pessoal, que usa formatadas em arquivos de texto. Os valores sob a subchave de fontes de dados ODBC podem ser da seguinte maneira:  
  
```  
Inventory : REG_SZ : SQL Server  
Payroll : REG_SZ : dBASE  
Personnel : REG_SZ : Text  
```
