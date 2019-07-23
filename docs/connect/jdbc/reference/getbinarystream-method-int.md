---
title: Método getBinaryStream (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBinaryStream (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: de22a6c4-1ba3-4ed0-91a2-bf235c2ceec3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0add171861f2ea9e021b9f9342968baf1601557
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67953708"
---
# <a name="getbinarystream-method-int"></a>Método getBinaryStream (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do índice da coluna designada na linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como um fluxo binário de bytes não interpretados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.InputStream getBinaryStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnIndex*  
  
 Um **int** que indica o índice de coluna.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto InputStream.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getBinaryStream é especificado pelo método getBinaryStream na interface java. Sql. ResultSet.  
  
 Esse método pode ser usado somente com tipos de dados binary, varbinary, varbinary(max) e image do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A tentativa de usá-lo com outros tipos de dados fará com que uma exceção seja lançada.  
  
 Depois que esse método obtiver o valor como um fluxo, o valor poderá ser lido em partes do fluxo. Esse método é especialmente adequado para recuperar valores LONGVARBINARY grandes.  
  
> [!NOTE]  
>  Todos os dados do fluxo retornado devem ser lidos antes de se obter o valor de outra coluna. A próxima chamada para um método getter fechará o fluxo de forma implícita. Além disso, um fluxo poderá retornar 0 quando o método InputStream.available for chamado, tendo dados disponíveis ou não.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getBinaryStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
