---
title: Método setNCharacterStream para o objeto Reader – long | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: af9a1ba8-7980-43fa-88e5-14f6cc5e897c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df5e8bf7e1d4bd1d8f355d7b324aab2537de4e34
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924930"
---
# <a name="setncharacterstream-method-javalangstring-javaioreader-long"></a>Método setNCharacterStream (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o objeto Reader especificado, que é o número especificado de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setNCharacterStream(java.lang.String parameterName,  
                     java.io.Reader value,  
                     long length)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *parameterName*  
  
 Uma **String** que indica o nome do parâmetro.  
  
 *value*  
  
 Um objeto Reader.  
  
 *length*  
  
 Um **long** que indica o número de caracteres no fluxo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setNCharacterStream é especificado pelo método setNCharacterStream na interface java.sql.CallableStatement.  
  
 Esse método deve ser usado para tipos de dados **NCHAR**, **NVARCHAR**, **NTEXT** e **XML**.  
  
 Se o comprimento do fluxo for diferente do especificado no parâmetro *length*, o driver JDBC lançará uma exceção quando a linha for atualizada ou inserida.  
  
 Se o comprimento do fluxo for desconhecido, o parâmetro *length* poderá ser definido como -1 para indicar que o driver deve aceitar o fluxo independentemente do seu comprimento. Com sqljdbc4.jar, é recomendável usar o Método [setNCharacterStream Method &#40;java.lang.String, java.io.Reader&#41;](../../../connect/jdbc/reference/setncharacterstream-method-java-lang-string-java-io-reader.md) do JDBC 4.0 quando o aplicativo quiser atualizar a coluna de um fluxo cujo comprimento é desconhecido.  
  
## <a name="see-also"></a>Consulte Também  
 [Método setNCharacterStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
