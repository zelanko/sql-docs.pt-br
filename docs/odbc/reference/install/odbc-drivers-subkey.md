---
title: Subchave de drivers ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
author: MightyPen
ms.author: genemi
ms.openlocfilehash: eb54ba7becad42d8d9d2c2870c02db37a3c7d89f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093978"
---
# <a name="odbc-drivers-subkey"></a>Subchave de drivers ODBC
Os valores na subchave drivers ODBC listam os drivers instalados. O formato desses valores é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|data|  
|----------|---------------|----------|  
|*Descrição do driver*|REG_SZ|**Recém-instalado**|  
  
 O nome do *Driver-Descrição* é definido pelo desenvolvedor do driver. Normalmente, é o nome do DBMS associado ao driver.  
  
 Por exemplo, suponha que os drivers tenham sido instalados para arquivos de texto formatados e SQL Server. Os valores na subchave de drivers ODBC podem ser:  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
