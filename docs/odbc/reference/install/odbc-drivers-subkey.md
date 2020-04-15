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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dd1f8d3293e35a543cce6b5079d9c6e10a331a88
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304027"
---
# <a name="odbc-drivers-subkey"></a>Subchave de drivers ODBC
Os valores sob a sub-chave Drivers ODBC listam os drivers instalados. O formato desses valores é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|*driver-descrição*|REG_SZ|**Instalado**|  
  
 O nome *da descrição do driver* é definido pelo desenvolvedor do driver. Geralmente é o nome do DBMS associado ao motorista.  
  
 Por exemplo, suponha que os drivers tenham sido instalados para arquivos de texto formatados e SQL Server. Os valores sob a sub-tecla Drivers ODBC podem ser:  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
