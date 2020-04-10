---
title: Método setAsciiStream (int, java.io.InputStream, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9dfa7781-d72f-407a-a8d4-1c78c9446d09
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e095e139cb4f37fe44c3107d4f3a8f30f038bf06
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920175"
---
# <a name="setasciistream-method-int-javaioinputstream-long"></a>Método setAsciiStream (int, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o número do parâmetro designado como o objeto java.io.InputStream especificado com o número de bytes especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setAsciiStream(int parameterIndex,  
                                 java.io.InputStream x,  
                                    long length)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *parameterIndex*  
  
 Um **int** que indica o número do parâmetro.  
  
 *x*  
  
 Um objeto java.io.InputStream.  
  
 *length*  
  
 Um **long** que indica o número de bytes.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setAsciiStream é especificado pelo método setAsciiStream na interface java.sql.PreparedStatement.  
  
 Se o comprimento do fluxo for diferente do especificado no parâmetro *length*, o driver JDBC lançará uma exceção quando a linha for atualizada ou inserida.  
  
 Se o comprimento do fluxo for desconhecido, o parâmetro *length* poderá ser definido como -1 para indicar que o driver deve aceitar o fluxo independentemente do seu comprimento. Com sqljdbc4.jar, é recomendável usar o método [setAsciiStream &#40;int, java.io.InputStream&#41;](../../../connect/jdbc/reference/setasciistream-method-int-java-io-inputstream.md) do JDBC 4.0 quando o aplicativo quiser atualizar a coluna de um fluxo cujo tamanho é desconhecido.  
  
## <a name="see-also"></a>Consulte Também  
 [Método setAsciiStream &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
