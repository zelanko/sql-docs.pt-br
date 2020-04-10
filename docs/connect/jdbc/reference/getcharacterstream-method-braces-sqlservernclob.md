---
title: Método getCharacterStream () (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7641698e-b25c-4bb2-bcc7-9273bdd08bf0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 71fac2e8febc9959dc6790d06f1eac097895476f
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928186"
---
# <a name="getcharacterstream-method--sqlservernclob"></a>Método getCharacterStream () (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna os dados de **NCLOB** como um objeto **Reader** ou como um fluxo de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.Reader getCharacterStream()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto Reader que contém os dados **NCLOB**.  
  
## <a name="remarks"></a>Comentários  
 Esse método getCharacterStream é especificado pelo método getCharacterStream na interface java.sql.NClob.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getCharacterStream &#40;SQLServerNClob&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)   
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
