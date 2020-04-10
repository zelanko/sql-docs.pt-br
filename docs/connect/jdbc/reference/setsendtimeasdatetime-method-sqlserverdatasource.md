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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ded6641232939ce0f76ade9f332646bbdd4c4d3
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927822"
---
# <a name="setsendtimeasdatetime-method-sqlserverdatasource"></a>Método setSendTimeAsDatetime (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Esse método foi adicionado ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0.  
  
 Modifica a configuração da propriedade de conexão **sendTimeAsDatetime**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setSendTimeAsDatetime(boolean sendTimeAsDateTime)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sendTimeAsDateTime*  
  
 Um valor booliano. Quando true, os valores java.sql.Time são enviados ao servidor como tipos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do **datetime**. Quando true, os valores java.sql.Time são enviados ao servidor como tipos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do **time**.  
  
## <a name="remarks"></a>Comentários  
 O [SQLServerDataSource.getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md) retorna a configuração da propriedade de conexão **sendTimeAsDatetime**.  
  
 Para obter mais informações na propriedade de conexão **sendTimeAsDatetime**, confira [Configuração das propriedades de conexão](../../../connect/jdbc/setting-the-connection-properties.md).  
  
 Para mais informações, confira [Como configurar a maneira como os valores de java.sql.Time são enviados ao servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
