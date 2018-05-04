---
title: Método TRUNCATE (SQLServerBlob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerBlob.truncate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ef181e04-003a-442a-9b7e-0c508a7cc873
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cd804132cff7897a780d6a17a26ce80fc2dd0fdf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="truncate-method-sqlserverblob"></a>Método truncate (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Trunca um BLOB, considerando o comprimento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *len*  
  
 O novo comprimento do BLOB.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Esse método truncate é especificado pelo método truncate na interface Java.SQL.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membros SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
