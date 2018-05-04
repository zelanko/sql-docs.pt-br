---
title: Método getUser (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.getUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3513dd7f-6ae5-4010-bde0-454ac4365bce
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 35559c83e8ced2d532546d372fef5980fa90ec7e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getuser-method-sqlserverdatasource"></a>Método getUser (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o nome do usuário que é usado para se conectar à fonte de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getUser()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **cadeia de caracteres** que contém o nome de usuário.  
  
## <a name="remarks"></a>Remarks  
 O [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) método define o nome de usuário que será usado ao conectar-se à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Se o valor do nome do usuário não for definido, o método getUser retornará o valor padrão de nulo.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
