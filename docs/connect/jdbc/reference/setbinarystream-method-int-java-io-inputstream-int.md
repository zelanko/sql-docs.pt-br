---
title: Método setBinaryStream (int, java.io.InputStream, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setBinaryStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fd6be063-08eb-40cf-9201-5a9f62387726
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0265f06d589ea89b38f995f8a9616fd22bcf92ef
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67975259"
---
# <a name="setbinarystream-method-int-javaioinputstream-int"></a>Método setBinaryStream (int, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o fluxo de entrada especificado, que terá o número de bytes especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setBinaryStream(int n,  
                                  java.io.InputStream x,  
                                  int length)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *n*  
  
 Um **int** que indica o número do parâmetro.  
  
 *x*  
  
 Um objeto InputStream.  
  
 *length*  
  
 Um **int** que indica o número de bytes.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setBinaryStream é especificado pelo método setBinaryStream na interface java.sql.PreparedStatement.  
  
 Se o comprimento do fluxo for diferente do especificado no parâmetro *length*, o driver JDBC lançará uma exceção quando a linha for atualizada ou inserida.  
  
 Se o comprimento do fluxo for desconhecido, o parâmetro *length* poderá ser definido como -1 para indicar que o driver deve aceitar o fluxo independentemente do seu comprimento. Com sqljdbc4.jar, é recomendável usar o método [setBinaryStream Method &#40;int, java.io.InputStream&#41;](../../../connect/jdbc/reference/setbinarystream-method-int-java-io-inputstream.md) do JDBC 4.0 quando o aplicativo quiser atualizar a coluna de um fluxo cujo comprimento é desconhecido.  
  
## <a name="see-also"></a>Consulte Também  
 [Método setBinaryStream &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setbinarystream-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
