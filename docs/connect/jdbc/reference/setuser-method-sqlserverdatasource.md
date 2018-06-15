---
title: Método setUser (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.setUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d2ea7906-2d10-438d-aa51-f576eea923c7
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8b6bf6d311e318dd9f233de2f698ad1d7892714e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32845051"
---
# <a name="setuser-method-sqlserverdatasource"></a>Método setUser (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o nome do usuário que é usado para se conectar à fonte de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setUser(java.lang.String user)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *user*  
  
 Um **cadeia de caracteres** que contém o nome de usuário.  
  
## <a name="remarks"></a>Remarks  
 O método setUser define o nome de usuário que será usado para se conectar ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Se o valor de nome de usuário não for definido, o [getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md) método retorna o valor padrão de null.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
