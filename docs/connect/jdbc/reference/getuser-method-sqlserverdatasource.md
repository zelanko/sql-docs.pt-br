---
description: Método getUser (SQLServerDataSource)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5b3f1cf26d395e982c21f7f4819ff19b4e633719
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433848"
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
  
## <a name="remarks"></a>Comentários  
 O método [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) define o nome de usuário que será usado ao se conectar à instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se o valor do nome do usuário não for definido, o método getUser retornará o valor padrão de nulo.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
