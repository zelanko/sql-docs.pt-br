---
title: Fontes de dados ODBC subchave | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: e81fe6cc77d92a8fde7530c1f79381025a05856b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915461"
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
