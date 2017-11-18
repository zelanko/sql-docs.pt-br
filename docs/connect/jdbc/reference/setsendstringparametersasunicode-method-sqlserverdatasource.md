---
title: "Método setSendStringParametersAsUnicode (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.setSendStringParametersAsUnicode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49198d63-76cb-4843-8d04-e49b1fbb6916
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 554c7e2483e96e27de627f764193a1d4fcabb6dd
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="setsendstringparametersasunicode-method-sqlserverdatasource"></a>Método setSendStringParametersAsUnicode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define uma **booliano** valor que indica se o envio de parâmetros de cadeia de caracteres para o servidor no formato UNICODE está habilitado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setSendStringParametersAsUnicode(boolean sendStringParametersAsUnicode)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *propriedade sendStringParametersAsUnicode*  
  
 **True** se os parâmetros de cadeia de caracteres são enviados para o servidor no formato UNICODE. Caso contrário, **false**.  
  
## <a name="remarks"></a>Comentários  
 Se a propriedade sendStringParametersAsUnicode for definida como **true**, que é o valor padrão, parâmetros string serão enviados para o servidor no formato UNICODE. Se sendStringParametersAsUnicode for definido como **false** parâmetros string serão enviados para o servidor em um formato ASCII/MBCS, e não em UNICODE. Se sendStringParametersAsUnicode não for definido, [getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md) retorna o valor padrão de **true**.  
  
 Para obter mais informações sobre a propriedade de conexão sendStringParametersAsUnicode, consulte [definindo as propriedades de Conexão](../../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

