---
description: Método getAsciiStream (SQLServerNClob)
title: Método getAsciiStream (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ff1d47e4-572a-4169-a631-ac261f7642b3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 04c7acab2316276a78697c4469643446437c76d5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437378"
---
# <a name="getasciistream-method-sqlservernclob"></a>Método getAsciiStream (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor **NCLOB** designado pelo objeto **NClob** como um fluxo ASCII.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.InputStream getAsciiStream()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto InputStream que contém os dados NCLOB.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getAsciiStream é especificado pelo método getAsciiStream na interface java.sql.SQLServerNClob.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
