---
title: Método (lang) getBinaryStream | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBinaryStream (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 149609b5-a6de-4e23-a440-7061775d0899
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 90527a6bfe0b943441f723fd22862832f136c6ca
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799795"
---
# <a name="getbinarystream-method-javalangstring"></a>Método getBinaryStream (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como um fluxo binário de bytes não interpretados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.InputStream getBinaryStream(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Uma **Cadeia de Caracteres** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto InputStream.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getBinaryStream é especificado pelo método getBinaryStream na interface do resultset.  
  
 Esse método pode ser usado somente com tipos de dados binary, varbinary, varbinary(max) e image do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A tentativa de usá-lo com outros tipos de dados fará com que uma exceção seja lançada.  
  
 Depois que esse método obtiver o valor como um fluxo, o valor poderá ser lido em partes do fluxo. Esse método é especialmente adequado para recuperar valores LONGVARBINARY grandes.  
  
> [!NOTE]  
>  Todos os dados do fluxo retornado devem ser lidos antes de se obter o valor de outra coluna. A próxima chamada para um método getter fechará o fluxo de forma implícita. Além disso, um fluxo poderá retornar 0 quando o método InputStream.available for chamado, tendo dados disponíveis ou não.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getBinaryStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
