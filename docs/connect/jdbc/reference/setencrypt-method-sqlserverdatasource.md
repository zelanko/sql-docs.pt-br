---
title: Método setEncrypt (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setEncrypt Method (SQLServerDataSource)
apilocation:
- setEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 0c85a9c1-f27c-457e-8461-403cc03e2d17
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da0aa987f1ec773e2f61e738bc4045136c64859a
ms.sourcegitcommit: 54cfeb36c9caa51ec68fa8f4a1918e305db5e00a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219226"
---
# <a name="setencrypt-method-sqlserverdatasource"></a>Método setEncrypt (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define um valor **booliano** que indica se a propriedade de criptografia está habilitada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setEncypt(boolean encrypt)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *encrypt*  
  
 **true** se a criptografia TLS, anteriormente conhecida como SSL, estiver habilitada entre o cliente e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Caso contrário, **false**.  
  
## <a name="remarks"></a>Comentários  
 Se a propriedade de criptografia estiver definida como **true**, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] verificará se o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa a criptografia TLS para todos os dados enviados entre o cliente e o servidor se o servidor tiver um certificado instalado. O valor padrão é **false**.  
  
 O driver JDBC detecta que a JVM (Máquina Virtual Java) está em execução ao tentar estabelecer um handshake TLS.  
  
 Se a propriedade de criptografia for definida como **true**, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] usará o provedor de segurança JSSE padrão da JVM para negociar a criptografia TLS com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O provedor de segurança padrão pode não dar suporte a todos os recursos necessários para negociar a criptografia TLS com êxito. Por exemplo, o provedor de segurança padrão pode não dar suporte ao tamanho da chave pública RSA usada no certificado TLS/SSL do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Nesse caso, o provedor de segurança padrão pode gerar um erro que fará com que o driver JDBC encerre a conexão. Para resolver esse problema, siga um destes procedimentos:  
  
-   Configure o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com um certificado do servidor que tenha uma chave pública RSA menor  
  
-   Configure a JVM para usar um provedor de segurança JSSE diferente no arquivo de propriedades de segurança "\<java-home>/lib/security/java.security"  
  
-   Use uma JVM diferente  
  
 Se a propriedade de criptografia não for especificada ou for definida como **false**, o driver não exigirá que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dê suporte à criptografia TLS. Se a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não for configurada para forçar a criptografia TLS, será estabelecida uma conexão sem criptografia. Se a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] for configurada para forçar a criptografia TLS, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] habilitará a criptografia TLS automaticamente na execução em uma JVM configurada corretamente; caso contrário, a conexão será encerrada e o driver produzirá um erro.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
