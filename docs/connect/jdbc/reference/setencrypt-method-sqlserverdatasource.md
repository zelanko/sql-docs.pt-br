---
title: Método setEncrypt (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- setEncrypt Method (SQLServerDataSource)
apilocation:
- setEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 0c85a9c1-f27c-457e-8461-403cc03e2d17
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 723c5c5402fb32f0ad74bf303dd7c682b88d1c84
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32843201"
---
# <a name="setencrypt-method-sqlserverdatasource"></a>Método setEncrypt (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define uma **booliano** valor que indica se a propriedade encrypt está habilitada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setEncypt(boolean encrypt)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Criptografar*  
  
 **True** se a criptografia Secure Sockets Layer (SSL) estiver habilitada entre o cliente e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Caso contrário, **false**.  
  
## <a name="remarks"></a>Remarks  
 Se a propriedade de criptografia é definida como **true**, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] garante que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] usa criptografia SSL para todos os dados enviados entre cliente e servidor se o servidor tem um certificado instalado. O valor padrão é **false**.  
  
 O driver JDBC detecta que a Máquina Virtual Java (JVM) está em execução ao tentar estabelecer um handshake SSL.  
  
 Se a propriedade de criptografia é definida como **true**, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] usa o provedor de segurança JSSE de padrão da JVM para negociar a criptografia SSL com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. O provedor de segurança padrão pode não dar suporte a todos os recursos necessários para negociar a criptografia SSL com êxito. Por exemplo, o provedor de segurança padrão pode não suportar o tamanho da chave pública RSA usada no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] certificado SSL. Nesse caso, o provedor de segurança padrão pode gerar um erro que fará com que o driver JDBC encerre a conexão. Para resolver esse problema, siga um destes procedimentos:  
  
-   Configurar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] com um certificado de servidor que tenha uma chave pública RSA menor  
  
-   Configure a JVM para usar um provedor de segurança JSSE diferente no "\<java-home > / lib/security/java.security" arquivo de propriedades de segurança  
  
-   Use uma JVM diferente  
  
 Se a propriedade de criptografia é não especificada ou definida como **false**, o driver não forçará o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] para oferecer suporte à criptografia SSL. Se o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] instância não está configurada para forçar a criptografia SSL, é estabelecida uma conexão sem criptografia. Se o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] instância é configurada para forçar a criptografia SSL, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] automaticamente irá habilitar a criptografia SSL quando em execução corretamente em JVM configurada, caso contrário, a conexão será encerrada e o driver irá gerar um erro.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
