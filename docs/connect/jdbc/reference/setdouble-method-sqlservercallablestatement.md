---
title: Método setDouble (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setDouble
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c054bb84-1292-4b70-b574-2ae189cd4e68
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d4ba5cce322b9fe925f3455929f0a040e05b3aa
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925799"
---
# <a name="setdouble-method-sqlservercallablestatement"></a>Método setDouble (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o valor **double** fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setDouble(java.lang.String sCol,  
                      double d)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sCol*  
  
 Uma **String** que contém o nome do parâmetro.  
  
 *d*  
  
 Um valor **double**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setDouble é especificado pelo método setDouble na interface java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
