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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 248213fed555ffc029162c44bdcccb656c311703
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67974289"
---
# <a name="setencrypt-method-sqlserverdatasource"></a>Método setEncrypt (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define um valor **booliano** que indica se a propriedade de criptografia está habilitada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setEncypt(boolean encrypt)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *encrypt*  
  
 **true** se a criptografia de protocolo SSL estiver habilitada entre o cliente e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Caso contrário, **false**.  
  
## <a name="remarks"></a>Comentários  
 Se a propriedade de criptografia estiver definida como **true**, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] garantirá que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] use a criptografia SSL para todos os dados enviados entre o cliente e o servidor se o servidor tiver um certificado instalado. O valor padrão é **false**.  
  
 O driver JDBC detecta que a Máquina Virtual Java (JVM) está em execução ao tentar estabelecer um handshake SSL.  
  
 Se a propriedade de criptografia for definida como **true**, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] usará o provedor de segurança JSSE padrão da JVM para negociar a criptografia SSL com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O provedor de segurança padrão pode não dar suporte a todos os recursos necessários para negociar a criptografia SSL com êxito. Por exemplo, o provedor de segurança padrão pode não ser compatível com o tamanho da chave pública RSA usada no certificado SSL do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Nesse caso, o provedor de segurança padrão pode gerar um erro que fará com que o driver JDBC encerre a conexão. Para resolver esse problema, siga um destes procedimentos:  
  
-   Configure o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com um certificado do servidor que tenha uma chave pública RSA menor  
  
-   Configure a JVM para usar um provedor de segurança JSSE diferente no arquivo de propriedades de segurança "\<java-home>/lib/security/java.security"  
  
-   Use uma JVM diferente  
  
 Se a propriedade de criptografia não for especificada nem estiver definida como **false**, o driver não exigirá que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dê suporte à criptografia SSL. Se a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não for configurada para forçar a criptografia SSL, será estabelecida uma conexão sem criptografia. Se a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] for configurada para forçar a criptografia SSL, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] habilitará a criptografia SSL automaticamente ao executar a JVM configurada adequadamente; caso contrário, a conexão será encerrada e o driver gerará um erro.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
