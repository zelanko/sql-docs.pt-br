---
description: Método setTrustServerCertificate (SQLServerDataSource)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1fb76148ae8c63dd30bd1532ec74d545bcc3388d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88355092"
---
# <a name="settrustservercertificate-method-sqlserverdatasource"></a>Método setTrustServerCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define um valor **Booliano** que indica se a propriedade trustServerCertificate está habilitada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setTrustServerCertificate(boolean trustServerCertificate)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *trustServerCertificate*  
  
 **true** se o certificado TLS, anteriormente conhecido como SSL, do servidor precisar ser automaticamente confiável quando a camada de comunicação for criptografada com TLS. Caso contrário, **false**.  
  
## <a name="remarks"></a>Comentários  
 Se a propriedade trustServerCertificate estiver definida como **true**, o certificado TLS/SSL do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será automaticamente confiável quando a camada de comunicação for criptografada com TLS. Em outras palavras, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] não validará o certificado TLS/SSL do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O valor padrão é **false**.  
  
 Se a propriedade trustServerCertificate estiver definida como **false**, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] validará o certificado TLS/SSL do servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
