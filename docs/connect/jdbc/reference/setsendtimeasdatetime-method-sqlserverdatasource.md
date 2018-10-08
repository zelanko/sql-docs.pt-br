---
title: Método setSendTimeAsDatetime (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 705a0494-b5e2-43db-940a-1b8cec550cdb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad4f7e8cee834619985be1ab140bc39698215060
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798234"
---
# <a name="setsendtimeasdatetime-method-sqlserverdatasource"></a>Método setSendTimeAsDatetime (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Esse método foi adicionado ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0.  
  
 Modifica a configuração do **sendTimeAsDatetime** propriedade de conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setSendTimeAsDatetime(boolean sendTimeAsDateTime)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sendTimeAsDateTime*  
  
 Um valor booliano. Quando true, os valores java.sql.Time são enviados ao servidor como tipos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do **datetime**. Quando true, os valores java.sql.Time são enviados ao servidor como tipos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do **time**.  
  
## <a name="remarks"></a>Remarks  
 [Sqlserverdatasource. Getsendtimeasdatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md) retorna a configuração do **sendTimeAsDatetime** propriedade de conexão.  
  
 Para obter mais informações sobre o **sendTimeAsDatetime** propriedade de conexão, consulte [definindo as propriedades de Conexão](../../../connect/jdbc/setting-the-connection-properties.md).  
  
 Para obter mais informações, consulte [time configurando como os valores são enviados para o servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
