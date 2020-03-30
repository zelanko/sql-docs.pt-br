---
title: Método setTrustServerCertificate (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- setTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 6c37b518-147e-4cd9-9eff-b48a3f5888c6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bd4059c3562d679e4f5f8bfdd133ca69a62c1fd2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67972214"
---
# <a name="settrustservercertificate-method-sqlserverdatasource"></a>Método setTrustServerCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define um valor **Booliano** que indica se a propriedade trustServerCertificate está habilitada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setTrustServerCertificate(boolean trustServerCertificate)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *trustServerCertificate*  
  
 **true** caso o certificado de protocolo SSL do servidor deva ser automaticamente confiável quando a camada de comunicação for criptografada com SSL. Caso contrário, **false**.  
  
## <a name="remarks"></a>Comentários  
 Se a propriedade trustServerCertificate estiver definida como **true**, o certificado SSL do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será automaticamente confiável quando a camada de comunicação for criptografada com SSL. Em outras palavras, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] não validará o certificado SSL do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O valor padrão é **false**.  
  
 Se a propriedade trustServerCertificate estiver definida como **false**, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] validará o certificado SSL do servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
