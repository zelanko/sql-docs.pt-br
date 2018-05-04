---
title: Construtor SQLServerBlob (SQLServerConnection, byte) | Microsoft Docs
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
- SQLServerConnection, byte[].SQLServerBlob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fe573e3-30db-4828-abab-e9346493e931
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1c7cc5041821fae51364271ad4ecf7666627cb0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverblob-constructor-sqlserverconnection-byte"></a>Construtor SQLServerBlob (SQLServerConnection, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa uma nova instância do [SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md) classe quando é fornecido um [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto e um **bytes** matriz.  
  
> [!NOTE]  
>  Este método foi substituído no JDBC Driver versão 2.0. Em vez disso, use o [createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md) método o [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) classe.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public SQLServerBlob(SQLServerConnection connection,  
                     byte[] data)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *conexão*  
  
 Um objeto SQLServerConnection.  
  
 *data*  
  
 Um **bytes** matriz.  
  
## <a name="see-also"></a>Consulte também  
 [Construtores SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-constructors.md)   
 [Membros SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
