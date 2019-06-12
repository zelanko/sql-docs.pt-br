---
title: Método setServerName (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 70920828-eda0-4064-be9f-c1e460db8f00
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a3c099e8bd441ee263202499036e25c738c9898f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66767981"
---
# <a name="setservername-method-sqlserverdatasource"></a>Método setServerName (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o nome do computador que está executando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setServerName(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *serverName*  
  
 Uma **String** que contém o nome do servidor.  
  
## <a name="remarks"></a>Remarks  
 O nome do servidor é o nome do host do computador de destino que executa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se a propriedade serverName não for definida, [getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md) retornará o valor padrão de nulo.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
