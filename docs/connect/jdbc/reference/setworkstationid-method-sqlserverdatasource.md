---
title: Método setWorkstationID (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.setWorkstationID
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c1093615-90bf-4918-9f05-8abd765ffb03
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6e505445d3ea1a7f9ba96b46b2764893d4628ed3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setworkstationid-method-sqlserverdatasource"></a>Método setWorkstationID (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o nome do cliente em nome do computador que é usado para se conectar à fonte de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setWorkstationID(java.lang.String workstationID)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *workstationID*  
  
 Um **cadeia de caracteres** que contém o nome do computador cliente.  
  
## <a name="remarks"></a>Remarks  
 A workstationID é o nome do computador cliente ou da estação de trabalho. Se a propriedade workstationID não for definida, o valor padrão será construído chamando o método InetAddress.getLocalHost().getHostName(). Se getHostName retorna um valor em branco, o método getHostAddress().toString() é chamado.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
