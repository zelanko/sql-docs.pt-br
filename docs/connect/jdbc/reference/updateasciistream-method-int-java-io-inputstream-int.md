---
description: Método updateAsciiStream (int, java.io.InputStream, int)
title: Método updateAsciiStream (int, java.io.InputStream, int)
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateAsciiStream (int, java.io.InputStream.int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d07944b8-7001-49b5-b3b3-0676f71e17cf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 162af3f276de47ed81b060316c983c0d6d148aa3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462345"
---
# <a name="updateasciistream-method-int-javaioinputstream-int"></a>Método updateAsciiStream (int, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor de fluxo ASCII que terá o número de bytes especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateAsciiStream(int index,  
                              java.io.InputStream x,  
                              int length)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *index*  
  
 Um **int** que indica o índice de coluna.  
  
 *x*  
  
 Um objeto InputStream.  
  
 *length*  
  
 Um **int** que indica o comprimento do fluxo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateAsciiStream é especificado pelo método updateAsciiStream na interface java.sql.ResultSet.  
  
 Esse método passa caracteres ASCII (bytes) de um objeto InputStream para colunas de caracteres conversíveis, que são o intervalo ASCII [0x00 - 0x7F] do Unicode e as páginas de código 874, 932, 936, 949, 950 e 1250 a 1258. Esse método executa uma conversão na página de ordenação de destino. A tentativa de atualizar uma coluna de destino não conversível fará com que uma exceção seja lançada. Para colunas binárias, são passados bytes brutos.  
  
 Se o comprimento do fluxo for diferente do especificado no parâmetro *length*, o driver JDBC lançará uma exceção quando a linha for atualizada ou inserida.  
  
 Se o comprimento do fluxo for desconhecido, o parâmetro *length* poderá ser definido como -1 para indicar que o driver deve aceitar o fluxo independentemente do seu comprimento. Com sqljdbc4.jar, é recomendável usar o [Método updateAsciiStream &#40;int, java.io.InputStream&#41;](../../../connect/jdbc/reference/updateasciistream-method-int-java-io-inputstream.md) do JDBC 4.0 quando o aplicativo quiser atualizar a coluna de um fluxo cujo comprimento é desconhecido.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateAsciiStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
