---
description: Construtor SQLServerBlob (SQLServerConnection, byte[])
title: Construtor SQLServerBlob (SQLServerConnection, byte[]) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection, byte[].SQLServerBlob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fe573e3-30db-4828-abab-e9346493e931
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 968c32094196c88ab8eb607e6faa8992de40ed00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472158"
---
# <a name="sqlserverblob-constructor-sqlserverconnection-byte"></a>Construtor SQLServerBlob (SQLServerConnection, byte[])
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa uma nova instância da classe [SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md), considerando um objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) e uma matriz de **byte**.  
  
> [!NOTE]  
>  Este método foi substituído no JDBC Driver versão 2.0. Em vez disso, use o método [createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md) da classe [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public SQLServerBlob(SQLServerConnection connection,  
                     byte[] data)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *connection*  
  
 Um objeto SQLServerConnection.  
  
 *data*  
  
 Uma matriz de **bytes**.  
  
## <a name="see-also"></a>Consulte Também  
 [Construtores SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-constructors.md)   
 [Membros de SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
