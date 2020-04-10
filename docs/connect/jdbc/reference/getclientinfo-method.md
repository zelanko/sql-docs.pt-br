---
title: Método getClientInfo () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b06a5ced-b760-4c78-b17e-854ce95a1a5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 678e28915faefafa832f4f9795b8e9b008681a3a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80907416"
---
# <a name="getclientinfo-method-"></a>Método getClientInfo ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma lista que contém o nome e o valor atual de cada propriedade de informações de cliente que tem o suporte do driver JDBC.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.util.Properties getClientInfo()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto Properties que contém o nome e o valor atual de cada propriedade de informações de cliente que tem o suporte do driver.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getClientInfo é especificado pelo método getClientInfo na interface java.sql.Connection.  
  
 O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] não é compatível com nenhuma propriedade de informações do cliente. Como resultado, esse método retorna um objeto Properties vazio.  
  
 Da mesma forma, os aplicativos podem usar o método [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) da classe [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) para recuperar uma lista das propriedades de informações do cliente para o qual o driver oferece suporte. Esse método [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) retorna um conjunto de resultados vazio.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getClientInfo &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
