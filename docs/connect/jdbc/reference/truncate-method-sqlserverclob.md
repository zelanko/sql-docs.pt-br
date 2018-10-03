---
title: Método TRUNCATE (SQLServerClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.truncate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ea3b2a03-387e-49d7-a4d6-ca6a6a354c90
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a5535cbc5d2417cfabfba1a3a001deee2ec27fe5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47615434"
---
# <a name="truncate-method-sqlserverclob"></a>Método truncate (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Trunca o CLOB no comprimento fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *len*  
  
 O comprimento, em caracteres, no qual o CLOB deve ser truncado.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Esse método de truncamento é especificado pelo método na interface do CLOB truncate.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
