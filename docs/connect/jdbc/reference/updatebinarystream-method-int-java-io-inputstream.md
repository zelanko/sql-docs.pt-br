---
title: "Método updateBinaryStream (int, Java.IO. InputStream) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1db3a975-c108-45d1-8c0d-14a094f391bd
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1ede0acb87e477f965696521117c99d410bd0b19
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="updatebinarystream-method-int-javaioinputstream"></a>Método updateBinaryStream (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor de fluxo binário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateBinaryStream(int columnIndex,  
                               java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnIndex*  
  
 Um **int** que indica o índice da coluna.  
  
 *x*  
  
 Um objeto InputStream.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateBinaryStream é especificado pelo método updateBinaryStream na interface Java.SQL. resultset.  
  
 Usando esse método para o **imagem**, **texto**, e **ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipos de dados podem afetar o desempenho.  
  
 Esse método passa bytes de um objeto InputStream selecionado [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] colunas binárias, como binary, varbinary, varbinary (max), imagem, xml e udt. Não há suporte para a atualização de colunas de caracteres nesse método. Para atualizar colunas de caracteres com um InputStream, use o [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) método.  
  
## <a name="see-also"></a>Consulte também  
 [Método updateBinaryStream &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

