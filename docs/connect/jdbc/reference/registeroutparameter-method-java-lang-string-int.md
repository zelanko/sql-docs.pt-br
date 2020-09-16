---
description: Método registerOutParameter (java.lang.String, int)
title: Método registerOutParameter para tipo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.registerOutParameter (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5d00242c-4d9c-42cc-86bb-b76f5ef876b8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a3d7c0a511f630683682c427fe73d0808e418375
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432778"
---
# <a name="registeroutparameter-method-javalangstring-int"></a>Método registerOutParameter (java.lang.String, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Registra o parâmetro OUT com o nome especificado para o tipo de JDBC fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void registerOutParameter(java.lang.String s,  
                                 int n)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *s*  
  
 Uma **String** que contém o nome do parâmetro.  
  
 *n*  
  
 Um código do tipo de JDBC, conforme definido em java.sql.Types.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método registerOutParameter é especificado pelo método registerOutParameter na interface java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Método registerOutParameter &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
