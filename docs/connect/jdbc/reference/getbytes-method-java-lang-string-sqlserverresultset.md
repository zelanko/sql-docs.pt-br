---
title: Método getBytes (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBytes (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ff617165-47f8-41c1-9c51-37ffc7714923
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6ad7f9ee6fc5250ac2bc349ccadb8909fc0e3cbe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66804026"
---
# <a name="getbytes-method-javalangstring-sqlserverresultset"></a>Método getBytes (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como uma matriz de **bytes** na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public byte[] getBytes(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Uma **Cadeia de Caracteres** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor retornado  
 Uma matriz de **bytes** valores.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getBytes é especificado pelo método getBytes na interface java.sql.ResultSet.  
  
 Esse método oferece suporte à recuperação de todas as colunas como uma leitura bruta de bytes do servidor. Ele retorna uma matriz de bytes diretamente do servidor no formato armazenado no servidor.  
  
 Em uma versão anterior do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], era possível usar o SQLServerResultSet.getBytes para converter valores entre matrizes de bytes e os tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **date**, **time**, **datetime2** ou **datetimeoffset**. Agora, ao usar esse método com esses tipos de dados, ocorrerá uma exceção indicando que não há suporte para a conversão.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getBytes &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
