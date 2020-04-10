---
title: Método getTimestamp (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTimestamp (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a9fd6496-c72e-4cc6-b46a-4aa9f13f90ff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 44f86bdda2868150d1bf52ef193426f7683b06fa
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927330"
---
# <a name="gettimestamp-method-int"></a>Método getTimestamp (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um objeto java.sql.Timestamp na linguagem de programação Java, considerando o índice do parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Timestamp getTimestamp(int index)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *index*  
  
 Um **int** que indica o índice do parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto Timestamp.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getTimestamp é especificado pelo método getTimestamp na interface java.sql.CallableStatement.  
  
 Esse método só retorna valores das colunas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]datetime**e**smalldatetime**do**.  
  
## <a name="see-also"></a>Consulte Também  
 [getTimestamp Method &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
