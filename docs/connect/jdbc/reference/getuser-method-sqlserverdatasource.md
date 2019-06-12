---
title: Método getUser (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3513dd7f-6ae5-4010-bde0-454ac4365bce
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: aee686bd06ce449f3dc42c1e7206228e93e66d96
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66782370"
---
# <a name="getuser-method-sqlserverdatasource"></a>Método getUser (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o nome do usuário que é usado para se conectar à fonte de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getUser()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Uma **String** que contém o nome do usuário.  
  
## <a name="remarks"></a>Remarks  
 O método [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) define o nome de usuário que será usado ao se conectar à instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se o valor do nome do usuário não for definido, o método getUser retornará o valor padrão de nulo.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
