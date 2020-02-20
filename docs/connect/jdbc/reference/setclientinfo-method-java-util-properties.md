---
title: Método setClientInfo (java.util.Properties) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b2a8ec0b-40a2-44d1-90d9-a810d4132e56
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a332f42c8193c851a33036af214ac31366986023
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67974743"
---
# <a name="setclientinfo-method-javautilproperties"></a>Método setClientInfo (java.util.Properties)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o valor das propriedades de informações de cliente da conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setClientInfo (java.util.Properties properties)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *properties*  
  
 Um objeto Properties que contém a lista das propriedades information do cliente para definir.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setClientInfo é especificado pelo método setClientInfo na interface java.sql.Connection.  
  
 O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] não é compatível com nenhuma propriedade de informações do cliente. Esse método vai gerar avisos se o parâmetro de entrada *properties* não se referir a um conjunto vazio de propriedades. Em outras palavras, este método gerará avisos para as propriedades que o aplicativo quiser definir. Os aplicativos devem usar o método [getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md) da classe [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) para recuperar cada aviso.  
  
## <a name="see-also"></a>Consulte Também  
 [Método setClientInfo &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
