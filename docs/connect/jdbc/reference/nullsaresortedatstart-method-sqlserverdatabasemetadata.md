---
title: Método nullsAreSortedAtStart (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.nullsAreSortedAtStart Method (SQLServerDatabaseMetaData)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 372515da-3b0e-46f6-8c0b-01b1b45c5a2f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c5250e5dc1d16e83107d92b24131294a74f2efdb
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80914592"
---
# <a name="nullsaresortedatstart-method-sqlserverdatabasemetadata"></a>Método nullsAreSortedAtStart (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se são classificados valores NULL no início, independentemente da ordem de classificação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean nullsAreSortedAtStart()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se estiver classificado no início. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método nullsAreSortedAtStart é especificado pelo método nullsAreSortedAtStart na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
