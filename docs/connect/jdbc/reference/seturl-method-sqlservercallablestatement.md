---
title: Método setURL (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3d83675e-74ca-49d9-8461-6326773c5c8c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 93602b5b1176aa71828fc6c94fc06b37dc28b2b5
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80901802"
---
# <a name="seturl-method-sqlservercallablestatement"></a>Método setURL (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o valor de URL fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setURL(java.lang.String sCol,  
                   java.net.URL u)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sCol*  
  
 Uma **Cadeia de Caracteres** que contém o nome do parâmetro.  
  
 *u*  
  
 Um objeto URL.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setURL é especificado pelo método setURL na interface java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
