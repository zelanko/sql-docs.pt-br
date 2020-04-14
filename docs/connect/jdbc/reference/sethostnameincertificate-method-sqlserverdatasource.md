---
title: Método setHostNameInCertificate (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- setHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 2bcf4f2e-a103-4374-abc4-ffad4ce8e3c0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 418e9aea8d44d3be23bc21c5a8950c5788e7c07a
ms.sourcegitcommit: 54cfeb36c9caa51ec68fa8f4a1918e305db5e00a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219278"
---
# <a name="sethostnameincertificate-method-sqlserverdatasource"></a>Método setHostNameInCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o nome do host a ser usado na validação do certificado TLS, anteriormente conhecido como SSL, do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setHostNameInCertificate(java.lang.String hostNameInCertificate)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *hostNameInCertificate*  
  
 Uma **String** que contém o nome do host.  
  
## <a name="remarks"></a>Comentários  
 O valor de hostNameInCertificate é usado para validar o certificado TLS/SSL do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando a camada de comunicação é criptografada com TLS. O valor padrão é nulo.  
  
 Se a propriedade hostNameInCertificate for definida como nula ou não for especificada, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] usará o valor da propriedade serverName para a validação no certificado TLS/SSL do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se a propriedade hostNameInCertificate for definida como uma cadeia de caracteres ou uma cadeia de caracteres vazia "", o driver usará esse valor para validar o certificado TLS/SSL do servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
