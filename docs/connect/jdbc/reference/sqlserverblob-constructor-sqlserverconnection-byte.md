---
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
ms.openlocfilehash: ac38e670cbb0aae3d18e3f066440ba1a81491830
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927266"
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
  
#### <a name="parameters"></a>parâmetros  
 *conexão*  
  
 Um objeto SQLServerConnection.  
  
 *data*  
  
 Uma matriz de **bytes**.  
  
## <a name="see-also"></a>Consulte Também  
 [Construtores SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-constructors.md)   
 [Membros de SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
