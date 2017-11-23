---
title: "Método setCharacterStream (Java, Java.IO. Reader, long) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 54fb2f13-f8d8-47b5-bec1-4a5af3e86a84
caps.latest.revision: "19"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 11788cf04694341635c078ba42d11eb1bf4fc4f8
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="setcharacterstream-method-javalangstring-javaioreader-long"></a>Método setCharacterStream (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o objeto Java.IO. Reader especificado, que é o número especificado de caracteres de comprimento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setCharacterStream(java.lang.String parameterName  
                        java.io.Reader reader,  
                        long length)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *nome do parâmetro*  
  
 Um **cadeia de caracteres** que contém o nome do parâmetro.  
  
 *leitor*  
  
 Um objeto do leitor que contém os dados Unicode.  
  
 *length*  
  
 Um **longo** que indica o número de caracteres no fluxo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setCharacterStream é especificado pelo método setCharacterStream na interface do CallableStatement.  
  
 Se o comprimento do fluxo for diferente do especificado no *comprimento* parâmetro, o driver JDBC lançará uma exceção quando a linha for atualizada ou inserida.  
  
 Se o comprimento do fluxo for desconhecido, o *comprimento* parâmetro pode ser definido como -1 para indicar que o driver deve aceitar o fluxo independentemente de seu tamanho. Com sqljdbc4.jar, é recomendável que você use o método do JDBC 4.0 [método setCharacterStream (Java, Java.IO. Reader)](../../../connect/jdbc/reference/setcharacterstream-method-java-lang-string-java-io-reader.md) quando o aplicativo quiser atualizar a coluna de um fluxo cujo comprimento é desconhecido.  
  
## <a name="see-also"></a>Consulte também  
 [Método setCharacterStream &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/setcharacterstream-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
