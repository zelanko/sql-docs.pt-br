---
title: Método getSendTimeAsDatetime (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02287122-5dc1-455d-987f-95fd9a69d503
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f18836d12be9834512783f90a2d7730fcfc98798
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845204"
---
# <a name="getsendtimeasdatetime-method-sqlserverdatasource"></a>Método getSendTimeAsDatetime (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Esse método foi adicionado ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0.  
  
 Retorna a configuração do **sendTimeAsDatetime** propriedade de conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean getSendTimeAsDatetime();  
```  
  
## <a name="return-value"></a>Valor retornado  
 **Verdadeiro** se os valores time serão enviados ao servidor como um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **datetime** tipo. **False** se os valores time serão enviados ao servidor como um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **tempo** tipo.  
  
## <a name="remarks"></a>Remarks  
 Ver [definindo as propriedades de Conexão](../../../connect/jdbc/setting-the-connection-properties.md) para obter mais informações sobre o **sendTimeAsDatetime** propriedade de conexão.  
  
 O [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) permite definir programaticamente a propriedade de conexão **sendTimeAsDatetime**.  
  
 Para obter mais informações, consulte [time configurando como os valores são enviados para o servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
