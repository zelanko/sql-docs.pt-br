---
title: Método getSubString (SQLServerClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.getSubString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bf915590-a883-4403-befa-5b5bb42f34d8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f5409040a5f7bb8cf7c03923da8ff976e4ab08ce
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926175"
---
# <a name="getsubstring-method-sqlserverclob"></a>Método getSubString (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna uma cópia da subcadeia de caracteres especificada no CLOB com base na posição inicial fornecida e no número de caracteres a serem copiados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getSubString(long pos,  
                                     int length)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *pos*  
  
 O primeiro caractere da subcadeia a ser extraído. O primeiro caractere está na posição 1.  
  
 *length*  
  
 O número de caracteres consecutivos a serem copiados.  
  
## <a name="return-value"></a>Valor retornado  
 Uma **cadeia de caracteres** que é a subcadeia de caracteres especificada no CLOB.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getSubString é especificado pelo método getSubString na interface java.sql.Clob.  
  
 A tentativa de obter zero caracteres de um CLOB nulo ou de comprimento zero retorna uma cadeia de caracteres vazia. A tentativa de obter qualquer comprimento de caracteres em qualquer posição que não seja a posição 1 em um CLOB de comprimento zero fará com que uma exceção de posição seja lançada.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
