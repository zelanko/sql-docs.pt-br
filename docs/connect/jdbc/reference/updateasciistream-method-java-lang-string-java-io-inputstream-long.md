---
title: Método updateAsciiStream (java.io.InputStream, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d426e8b9-62b7-49f8-9863-8697fd3a7085
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 33a0686a891a592f37a8ebd57f341df35db48894
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925563"
---
# <a name="updateasciistream-method-javalangstring-javaioinputstream-long"></a>Método updateAsciiStream (java.lang.String, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor de fluxo ASCII que terá o número de bytes especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateAsciiStream(java.lang.String columnName,  
                              java.io.InputStream streamValue,  
                              long length)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *columnName*  
  
 Uma **Cadeia de Caracteres** que contém o nome da coluna.  
  
 *streamValue*  
  
 Um objeto InputStream.  
  
 *length*  
  
 O comprimento do fluxo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateAsciiStream é especificado pelo método updateAsciiStream na interface java.sql.ResultSet.  
  
 Esse método passa caracteres ASCII (bytes) de um objeto InputStream para colunas de caracteres conversíveis, que são o intervalo ASCII [0x00 - 0x7F] do Unicode e as páginas de código 874, 932, 936, 949, 950 e 1250 a 1258. Esse método executa uma conversão na página de ordenação de destino. A tentativa de atualizar uma coluna de destino não conversível fará com que uma exceção seja lançada. Para colunas binárias, são passados bytes brutos.  
  
 Se o comprimento do fluxo for diferente do especificado no parâmetro *length*, o driver JDBC lançará uma exceção quando a linha for atualizada ou inserida.  
  
 Se o comprimento do fluxo for desconhecido, o parâmetro *length* poderá ser definido como -1 para indicar que o driver deve aceitar o fluxo independentemente do seu comprimento. Com sqljdbc4.jar, é recomendável usar o método [updateAsciiStream &#40;java.lang.String, java.io.InputStream&#41;](../../../connect/jdbc/reference/updateasciistream-method-java-lang-string-java-io-inputstream.md) do JDBC 4.0 quando o aplicativo deseja atualizar a coluna de um fluxo cujo comprimento é desconhecido.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateAsciiStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
