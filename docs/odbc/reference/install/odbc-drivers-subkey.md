---
title: Subchave de Drivers ODBC | Microsoft Docs
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
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17e0a418957aa4413d0fd7d02ebdc0243596d013
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-drivers-subkey"></a>Subchave de Drivers ODBC
Os valores na subchave Drivers ODBC listam os drivers instalados. O formato desses valores é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|data|  
|----------|---------------|----------|  
|*Descrição do driver*|REG_SZ|**Instalado**|  
  
 O *descrição do driver* nome é definido pelo desenvolvedor de driver. Geralmente é o nome do DBMS associado com o driver.  
  
 Por exemplo, suponha que foram instalados drivers para arquivos de texto formatado e o SQL Server. Os valores na subchave Drivers ODBC podem ser:  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
