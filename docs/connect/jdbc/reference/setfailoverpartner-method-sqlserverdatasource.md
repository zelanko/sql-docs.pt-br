---
title: Método setFailoverPartner (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setFailoverPartner
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5310b7c2-9d10-474f-ad3a-218fe5da694b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 11bd963275f94fd5ab37d17ead561adbfb0bff5c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802956"
---
# <a name="setfailoverpartner-method-sqlserverdatasource"></a>Método setFailoverPartner (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o nome do servidor de failover usado em uma configuração de espelhamento de banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setFailoverPartner(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *serverName*  
  
 Uma **cadeia de caracteres** que contém o nome do servidor de failover.  
  
## <a name="remarks"></a>Remarks  
 O valor definido por este método é usado no caso de uma falha de conexão inicial com o servidor principal; depois que a conexão inicial é feita, este valor é ignorado. O método [setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md) também precisa ser usado junto com este método; caso contrário, uma exceção será gerada.  
  
 O driver não dá suporte à especificação do número de porta do servidor de failover quando o nome do servidor de failover é definido. Porém, chamar os métodos [setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md) e [setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md) com o método [setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) é compatível.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
