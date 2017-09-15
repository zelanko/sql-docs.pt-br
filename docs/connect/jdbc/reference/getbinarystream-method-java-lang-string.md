---
title: "Método (Java) getBinaryStream | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.getBinaryStream (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 149609b5-a6de-4e23-a440-7061775d0899
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ff004671c2e261d055b49e1a1de3b0643c1fc94b
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getbinarystream-method-javalangstring"></a>Método getBinaryStream (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um fluxo binário de bytes não interpretados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.InputStream getBinaryStream(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Um **cadeia de caracteres** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto InputStream.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getBinaryStream é especificado pelo método getBinaryStream na interface Java.SQL. resultset.  
  
 Esse método pode ser usado apenas com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipos de dados de binary, varbinary, varbinary (max) e de imagem. A tentativa de usá-lo com outros tipos de dados fará com que uma exceção seja lançada.  
  
 Depois que esse método obtiver o valor como um fluxo, o valor poderá ser lido em partes do fluxo. Esse método é especialmente adequado para recuperar valores LONGVARBINARY grandes.  
  
> [!NOTE]  
>  Todos os dados do fluxo retornado devem ser lidos antes de se obter o valor de outra coluna. A próxima chamada para um método getter fechará o fluxo de forma implícita. Além disso, um fluxo pode retornar 0 quando o método InputStream.available é chamado, se há dados disponíveis ou não.  
  
## <a name="see-also"></a>Consulte também  
 [Método getBinaryStream &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
