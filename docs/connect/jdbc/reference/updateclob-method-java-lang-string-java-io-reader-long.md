---
title: Método updateClob (java.lang.String, java.io.Reader, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6b8f759a-ce5d-41b2-b6cc-24a3ab299f1f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 99c97a4d7e176e5f1eab0ebc1185df527e4fe15c
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919892"
---
# <a name="updateclob-method-javalangstring-javaioreader-long"></a>Método updateClob (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada usando o objeto Reader especificado, cujo tamanho tem um número de caracteres especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateClob(java.lang.String columnLabel,  
                        java.io.Reader reader,  
                        long length)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *columnLabel*  
  
 Uma **Cadeia de Caracteres** que contém o rótulo da coluna.  
  
 *reader*  
  
 Um objeto Reader.  
  
 *length*  
  
 O número de caracteres nos dados do parâmetro.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateClob é especificado pelo método updateClob na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateClob &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
