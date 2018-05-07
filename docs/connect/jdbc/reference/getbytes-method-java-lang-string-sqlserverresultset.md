---
title: Método (Java) (SQLServerResultSet) getBytes | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBytes (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ff617165-47f8-41c1-9c51-37ffc7714923
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31b969f25fffd2607206f77300d5de04c65610de
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getbytes-method-javalangstring-sqlserverresultset"></a>Método getBytes (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto como um **bytes** matriz na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public byte[] getBytes(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Um **cadeia de caracteres** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Uma matriz de **bytes** valores.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getBytes é especificado pelo método getBytes na interface Java.SQL. resultset.  
  
 Esse método oferece suporte à recuperação de todas as colunas como uma leitura bruta de bytes do servidor. Ele retorna uma matriz de bytes diretamente do servidor no formato armazenado no servidor.  
  
 Em uma versão anterior do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], você pode usar GetBytes para converter valores entre matrizes de bytes e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de dados **data**, **tempo**,  **datetime2**, ou **datetimeoffset**. Agora, ao usar esse método com esses tipos de dados, ocorrerá uma exceção indicando que não há suporte para a conversão.  
  
## <a name="see-also"></a>Consulte também  
 [Método getBytes &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
