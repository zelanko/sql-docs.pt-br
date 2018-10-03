---
title: Método getLong (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getLong (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b7078ca7-fd2a-4474-ab29-989ae28c77e8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caa1c4eb870f37e7c8bc9e2eb244f8be0ae9abe6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47691864"
---
# <a name="getlong-method-int"></a>Método getLong (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um objeto **long** na linguagem de programação Java, considerando o índice do parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public long getLong(int index)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *index*  
  
 Um **int** que indica o índice do parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 Um **longo** valor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getLong é especificado pelo método getLong na interface java.sql.CallableStatement.  
  
 Esse método só é compatível com os tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que podem retornar com segurança um valor inteiro como bigint, int, smallint, tinyint e bit. Seu uso em quaisquer outros tipos de dados fará com que uma exceção seja lançada.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getLong &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getlong-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
