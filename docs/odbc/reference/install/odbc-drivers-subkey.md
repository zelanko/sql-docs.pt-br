---
description: Subchave de drivers ODBC
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b950a352c3da69a2a8de9a89f7bbebf87e0a597a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448916"
---
# <a name="odbc-drivers-subkey"></a>Subchave de drivers ODBC
Os valores na subchave drivers ODBC listam os drivers instalados. O formato desses valores é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|*Descrição do driver*|REG_SZ|**Instalado**|  
  
 O nome do *Driver-Descrição* é definido pelo desenvolvedor do driver. Normalmente, é o nome do DBMS associado ao driver.  
  
 Por exemplo, suponha que os drivers tenham sido instalados para arquivos de texto formatados e SQL Server. Os valores na subchave de drivers ODBC podem ser:  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
