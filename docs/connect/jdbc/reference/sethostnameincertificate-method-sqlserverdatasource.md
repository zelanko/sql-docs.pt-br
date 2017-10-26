---
title: "Método setHostNameInCertificate (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- setHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- setHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 2bcf4f2e-a103-4374-abc4-ffad4ce8e3c0
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a498f6f14a5836637784b98a2f8bf82134f3de61
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sethostnameincertificate-method-sqlserverdatasource"></a>Método setHostNameInCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o nome de host a ser usado ao validar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] certificado Secure Sockets Layer (SSL).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setHostNameInCertificate(java.lang.String hostNameInCertificate)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *hostNameInCertificate*  
  
 Um **cadeia de caracteres** que contém o nome do host.  
  
## <a name="remarks"></a>Comentários  
 O valor de hostNameInCertificate é usado para validar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] certificado SSL quando a camada de comunicação é criptografada usando SSL. O valor padrão é nulo.  
  
 Se a propriedade hostNameInCertificate for definida como null ou não for especificada, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] usará o valor da propriedade serverName para validar em relação a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] certificado SSL. Se a propriedade hostNameInCertificate for definida como uma cadeia de caracteres ou uma cadeia de caracteres vazia "", o driver usará esse valor para validar o certificado SSL do servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

