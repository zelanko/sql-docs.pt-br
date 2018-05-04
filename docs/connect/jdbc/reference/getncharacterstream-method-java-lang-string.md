---
title: Método (Java) getNCharacterStream | Microsoft Docs
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
ms.assetid: 45d2695b-0727-419d-8921-a51d6feef0aa
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f144c7c50bb910925d4dda15b26375dface1fca6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getncharacterstream-method-javalangstring"></a>Método getNCharacterStream (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um objeto do leitor considerando o nome do parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final java.io.Reader getNCharacterStream(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnLabel*  
  
 Um **cadeia de caracteres** que contém o rótulo da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 AReaderobject.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método deve ser usado ao acessar **NCHAR**, **NVARCHAR** e **LONGNVARCHAR** parâmetros.  
  
 Esse método getNCharacterStream é especificado pelo método getNCharacterStream na interface do CallableStatement.  
  
## <a name="see-also"></a>Consulte também  
 [Método getNCharacterStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
