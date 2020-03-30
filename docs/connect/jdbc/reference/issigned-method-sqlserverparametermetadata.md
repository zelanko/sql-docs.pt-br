---
title: Método isSigned (SQLServerParameterMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.isSigned
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1a4af386-e379-4a60-a107-a99e63a490ac
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 46b93b2b5c45491ad91be8b1e40fc909f0c4510d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67977233"
---
# <a name="issigned-method-sqlserverparametermetadata"></a>Método isSigned (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se os valores do parâmetro designado podem ser números assinados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isSigned(int param)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *param*  
  
 Um **int** que indica o índice do parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 **true** se o parâmetro designado puder conter números assinados. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método isSigned é especificado pelo método isSigned na interface java.sql.ParameterMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [Membros SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [Classe SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
