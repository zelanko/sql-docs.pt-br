---
title: Método updateCharacterStream (java.lang.String, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8ec22a9-4bbd-4759-9f21-957304ef3a5e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 67a9078834f4d5a0c83eab42e305b02319ca49e0
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919946"
---
# <a name="updatecharacterstream-method-javalangstring-javaioreader"></a>Método updateCharacterStream (java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor de fluxo de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateCharacterStream(java.lang.String columnLabel,  
                                  java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *columnLabel*  
  
 Uma **Cadeia de Caracteres** que contém o rótulo da coluna.  
  
 *reader*  
  
 Um objeto Reader.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateCharacterStream é especificado pelo método updateCharacterStream na interface java.sql.ResultSet.  
  
 Este método passa caracteres Unicode de um objeto Reader para colunas de texto e binárias selecionadas. Isto inclui todas as colunas de texto e colunas **binary**, **varbinary**, **varbinary(max)** , **image** e **xml**, mas não **udt**.  
  
 O uso deste método nos tipos de dados **image**, **text** e **ntext** do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode afetar o desempenho.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateCharacterStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
