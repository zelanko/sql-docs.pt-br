---
description: Método setNCharacterStream para o objeto java.io.Reader – long
title: Método setNCharacterStream para o objeto java.io.Reader – long | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36396dc9-f109-4da0-bd64-726704046bbf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d5baf0107e4c641782d2808e0fc62be9e1dbc3e5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431668"
---
# <a name="setncharacterstream-method-int-javaioreader-long"></a>Método setNCharacterStream (int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o objeto Reader especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setNCharacterStream(int parameterIndex,  
                                                  java.io.Reader value,  
                                                                long length)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *parameterIndex*  
  
 Um **int** que indica o índice do parâmetro.  
  
 *value*  
  
 Um objeto Reader que contém o valor do parâmetro.  
  
 *length*  
  
 Um **long** que indica o número de caracteres no valor do parâmetro.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setNCharacterStream é especificado pelo método setNCharacterStream na interface java.sql.PreparedStatement.  
  
 Esse método deve ser usado para tipos de dados **NCHAR**, **NVARCHAR**, **NTEXT** e **XML**.  
  
 Se o comprimento do fluxo for diferente do especificado no parâmetro *length*, o driver JDBC lançará uma exceção quando a linha for atualizada ou inserida.  
  
 Se o comprimento do fluxo for desconhecido, o parâmetro *length* poderá ser definido como -1 para indicar que o driver deve aceitar o fluxo independentemente do seu comprimento. Com sqljdbc4.jar, é recomendável usar o [Método setNCharacterStream &#40;int, java.io.Reader&#41;](../../../connect/jdbc/reference/setncharacterstream-method-int-java-io-reader.md) do JDBC 4.0 quando o aplicativo quiser atualizar a coluna de um fluxo cujo comprimento é desconhecido.  
  
## <a name="see-also"></a>Consulte Também  
 [Método setNCharacterStream &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
