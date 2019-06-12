---
title: Método (lang) getClientInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e8e632c4-d6cc-4c5e-b6ad-873579343b19
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b9fd6139a7fc36033c33fa4fc5301f5f7d0a4f14
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66763929"
---
# <a name="getclientinfo-method-javalangstring"></a>Método getClientInfo (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor de uma propriedade de informações de cliente especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getClientInfo (java.lang.String name)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *name*  
  
 Uma String que contém o nome da propriedade information do cliente a ser recuperado.  
  
## <a name="return-value"></a>Valor retornado  
 Uma String que contém o valor da propriedade information do cliente a ser recuperado.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getClientInfo é especificado pelo método getClientInfo na interface do Connection.  
  
 O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] não oferece suporte às propriedades de informações do cliente. Consequentemente, esse método retorna um valor **null**.  
  
 Da mesma forma, os aplicativos podem usar o método [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) da classe [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) para recuperar uma lista das propriedades de informações do cliente para o qual o driver oferece suporte. Esse método [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) retorna um conjunto de resultados vazio.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getClientInfo &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
