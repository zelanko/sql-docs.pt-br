---
description: Método setCatalog (SQLServerConnection)
title: Método setCatalog (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 553c0603-c07d-436a-86eb-3ba6b51bd696
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 655da723b4f3babb1cd3dd7a938f38382b4e93e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432328"
---
# <a name="setcatalog-method-sqlserverconnection"></a>Método setCatalog (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o nome de catálogo especificado para selecionar um subespaço do banco de dados deste objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) no qual trabalhar.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setCatalog(java.lang.String catalog)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *catalog*  
  
 Uma **String** que contém o nome do catálogo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setCatalog é especificado pelo método setCatalog na interface java.sql.Connection.  
  
 O argumento *catalog* é escapado automaticamente pelo [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Usar este método define a propriedade catalog para o objeto Connection. Ela não é definida implicitamente de nenhuma outra maneira.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
