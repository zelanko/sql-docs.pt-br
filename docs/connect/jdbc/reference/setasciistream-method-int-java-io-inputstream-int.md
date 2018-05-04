---
title: Método setAsciiStream (int, Java.IO. InputStream, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setAsciiStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9436c39f-f1a1-484a-a75b-776a72ca70f4
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18d3dd269f8713305559994d15a76ab324a2c412
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setasciistream-method-int-javaioinputstream-int"></a>Método setAsciiStream (int, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o número do parâmetro designado como o objeto InputStream fornecido com o número de bytes fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setAsciiStream(int n,  
                                 java.io.InputStream x,  
                                 int length)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *n*  
  
 Um **int** que indica o número do parâmetro.  
  
 *x*  
  
 Um objeto InputStream.  
  
 *Comprimento*  
  
 O número de bytes.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setAsciiStream é especificado pelo método setAsciiStream na interface PreparedStatement.  
  
 Se o comprimento do fluxo for diferente do especificado no *comprimento* parâmetro, o driver JDBC lançará uma exceção quando a linha for atualizada ou inserida.  
  
 Se o comprimento do fluxo for desconhecido, o *comprimento* parâmetro pode ser definido como -1 para indicar que o driver deve aceitar o fluxo independentemente de seu tamanho. Com sqljdbc4.jar, é recomendável que você use o método do JDBC 4.0 [método setAsciiStream &#40;int, Java.IO. InputStream&#41; ](../../../connect/jdbc/reference/setasciistream-method-int-java-io-inputstream.md) quando o aplicativo quiser atualizar a coluna de um fluxo cujo comprimento é desconhecido.  
  
## <a name="see-also"></a>Consulte também  
 [Método setAsciiStream &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
