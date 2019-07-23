---
title: Segurança do aplicativo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 940879b4-aa0f-41ce-a369-6cfc0e78e01d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aa7681890b09647cb554ef6c80e8646fb69c9f42
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957461"
---
# <a name="application-security"></a>Segurança do aplicativo
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Ao usar o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], é importante tomar precauções para garantir a segurança de seu aplicativo. As seções a seguir fornecem informações referentes a etapas que você pode realizar para ajudar a proteger seu aplicativo.  
  
## <a name="using-java-policy-permissions"></a>Usando permissões de política de Java  
 Ao usar o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], é importante especificar as permissões de política de Java exigidas pelo driver JDBC. O Java Runtime Environment (JRE) fornece um modelo de segurança extensivo que você pode usar em tempo de execução para determinar se um thread tem acesso a um recurso. Os arquivos de política de Segurança podem controlar este acesso. Os próprios arquivos de política são gerenciados pelo implantador e pelo sysadmin para o contêiner, mas as permissões listadas neste tópico são as que afetam o funcionamento do driver JDBC.  
  
 Uma permissão típica no arquivo de política se parece com o seguinte.  
  
```  
// Example policy file entry.  
grant [signedBy <signer>,] [codeBase <code source>] {  
   permission  <class>  [<name> [, <action list>]];  
};  
```  
  
 A base de código a seguir deve ser restrita à base de código do driver JDBC para garantir que você conceda a menor quantidade de privilégios.  
  
```  
grant codeBase "file:/install_dir/lib/-" {  
  
// Grant access to data source.  
permission java.util.PropertyPermission "java.naming.*", "read,write";  
  
// Specify which hosts can be connected to.  
permission java.net.socketPermission "host:port", "connect";  
  
// Logger permission to take advantage of logging.  
permission java.util.logging.LoggingPermission;  
  
// Grant listen/connect/accept permissions to the driver if   
// connecting to a named instance as the client driver.   
// This connects to a udp service and listens for a response.  
permission java.net.SocketPermission "*", "listen, connect, accept";   
};   
```  
  
> [!NOTE]  
>  O código "file:/install_dir/lib/-" refere-se ao diretório de instalação do driver JDBC.  
  
## <a name="protecting-server-communication"></a>Protegendo a comunicação do servidor  
 Ao usar o driver JDBC para se comunicar com um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode proteger o canal de comunicação usando o Protocolo IPSEC (Internet Protocol Security) ou o Protocolo SSL (Secure Sockets Layer); ou pode usar ambos.  
  
 O suporte ao SSL pode ser usado para fornecer um nível adicional de proteção além do IPSEC. Para obter mais informações sobre como usar SSL, consulte [usando criptografia SSL](../../connect/jdbc/using-ssl-encryption.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Protegendo aplicativos do JDBC Driver](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
