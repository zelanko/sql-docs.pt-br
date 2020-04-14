---
title: Método getHostNameInCertificate (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- getHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 45ea04e2-9ea5-4171-9136-d09f8a95e128
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5f35af25109bc68a36560c6496cf5f5268bd9319
ms.sourcegitcommit: 54cfeb36c9caa51ec68fa8f4a1918e305db5e00a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219255"
---
# <a name="gethostnameincertificate-method-sqlserverdatasource"></a>Método getHostNameInCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o nome do host usado na validação do certificado TLS, anteriormente conhecido como SSL, do SQL Server.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getHostNameInCertificate()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Uma **String** que contém o nome do host ou o valor nulo se nenhum valor tiver sido definido.  
  
## <a name="remarks"></a>Comentários  
 O nome do host é usado para validar o valor do certificado TLS/SSL do SQL Server quando a camada de comunicação é criptografada com TLS/SSL.  
  
 Se o nome do host não for definido, o método [getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md) retornará nulo.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
