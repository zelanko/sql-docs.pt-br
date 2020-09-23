---
description: Método updateCharacterStream (java.lang.String, java.io.Reader, int)
title: Método updateCharacterStream (java.lang.String, java.io.Reader, int)
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateCharacterStream (java.lang.String, java.io.Reader, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 08cfc4e0-83f0-4f2f-ac55-b381f34fe67f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b792971c175a7e990d7579379b6a48deb2808dc6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88353732"
---
# <a name="updatecharacterstream-method-javalangstring-javaioreader-int"></a>Método updateCharacterStream (java.lang.String, java.io.Reader, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor de fluxo de caracteres que terá o número de caracteres especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateCharacterStream(java.lang.String columnName,  
                                  java.io.Reader readerValue,  
                                  int length)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Uma **Cadeia de Caracteres** que contém o nome da coluna.  
  
 *readerValue*  
  
 Um objeto Reader.  
  
 *length*  
  
 Um **int** que indica o comprimento do fluxo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateCharacterStream é especificado pelo método updateCharacterStream na interface java.sql.ResultSet.  
  
 Este método passa caracteres Unicode de um objeto Reader para colunas de texto e binárias selecionadas. Isto inclui todas as colunas de texto e colunas **binary**, **varbinary**, **varbinary(max)** , **image** e **xml**, mas não **udt**.  
  
 Se o comprimento do fluxo for diferente daquele especificado no parâmetro *length*, o driver JDBC lançará uma exceção quando a linha for atualizada ou inserida.  
  
 Se o comprimento do fluxo for desconhecido, o parâmetro *length* poderá ser definido como -1 para indicar que o driver deve aceitar o fluxo independentemente do seu comprimento. Com sqljdbc4.jar, é recomendável usar o [Método updateCharacterStream &#40;java.lang.String, java.io.Reader&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-java-lang-string-java-io-reader.md) do JDBC 4.0 quando o aplicativo quiser atualizar a coluna de um fluxo cujo comprimento é desconhecido.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateCharacterStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
