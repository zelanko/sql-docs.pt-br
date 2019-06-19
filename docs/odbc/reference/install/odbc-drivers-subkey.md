---
title: Subchave de Drivers ODBC | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 43be1c5e75998903ff4e64fc5f4230818a873ffc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63281131"
---
# <a name="odbc-drivers-subkey"></a>Subchave de drivers ODBC
Os valores sob a subchave de Drivers ODBC listam os drivers instalados. O formato desses valores é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|*driver-description*|REG_SZ|**instalado**|  
  
 O *descrição do driver* nome é definido pelo desenvolvedor de driver. Ele geralmente é o nome do DBMS associado com o driver.  
  
 Por exemplo, suponha que foram instalados drivers para arquivos de texto formatado e o SQL Server. Os valores sob a subchave de Drivers ODBC podem ser:  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
