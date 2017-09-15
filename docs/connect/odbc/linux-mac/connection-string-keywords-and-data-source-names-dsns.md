---
title: "Palavras-chave de cadeia de caracteres de Conexão e fonte de dados (DSNs) de nomes | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data source names
- connection string keywords
- DSNs
ms.assetid: f95cdbce-e7c2-4e56-a9f7-8fa3a920a125
caps.latest.revision: 41
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 508fcb62b7cf9ccd78c04b869add7acccb14f258
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="connection-string-keywords-and-data-source-names-dsns"></a>Palavras-chave de cadeia de conexão e nomes de fontes de dados (DSNs)
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este tópico discute como você pode criar uma conexão para um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] banco de dados.  
  
## <a name="connection-properties"></a>Propriedades da conexão  
Para esta versão do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] o Driver ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] em Linux ou macOS, você pode usar as seguintes palavras-chave da conexão:  
  
||||||  
|-|-|-|-|-|  
|`Addr`|`Address`|`ApplicationIntent`|`AutoTranslate`|`Database`|
|`Driver`|`DSN`|`Encrypt`|`FileDSN`|`MARS_Connection`|  
|`MultiSubnetFailover`|`PWD`|`Server`|`Trusted_Connection`|`TrustServerCertificate`|  
|`UID`|`WSID`|`ColumnEncryption`|`TransparentNetworkIPResolution`||  

> [!IMPORTANT]  
> Ao se conectar a um banco de dados que use o espelhamento de banco de dados (tem um parceiro de failover), não especifique o nome do banco de dados na cadeia de conexão. Em vez disso, enviam um **usar** *database_name* comando para se conectar ao banco de dados antes de executar suas consultas.  
  
Para obter mais informações sobre essas palavras-chave, consulte a seção sobre ODBC de [Usando palavras-chave da cadeia de conexão com o SQL Server Native Client](http://go.microsoft.com/fwlink/?LinkID=126696).  
  
O valor passado para o **Driver** palavra-chave pode ser um dos seguintes:  
  
-   O nome usado quando você instalou o driver.

-   O caminho para a biblioteca do driver, que foi especificado no arquivo. ini de modelo usado para instalar o driver.  

Para criar um DSN, crie (se necessário) e edite o arquivo **~/.odbc.ini** (`.odbc.ini` em seu diretório base) para um DSN de usuário somente é acessível para o usuário atual, ou `/etc/odbc.ini` para um DSN de sistema (privilégios administrativos necessários.) Este é um arquivo de exemplo que mostra as entradas necessárias mínimas para um DSN:  

```  
[MSSQLTest]  
Driver = ODBC Driver 13 for SQL Server  
Server = [protocol:]server[,port]  
#   
# Note:  
# Port is not a valid keyword in the odbc.ini file  
# for the Microsoft ODBC driver on Linux or macOS
#  
```  

Opcionalmente, você pode especificar o protocolo e a porta para se conectar ao servidor. Por exemplo, **Server = tcp:***servername***, 12345**. Observe que é o único protocolo com suporte dos drivers de Linux e macOS `tcp`.

Para se conectar a uma instância nomeada em uma porta estática, use <b>Server =</b>*servername*,**port_number**. Não há suporte para a conexão com uma porta dinâmica.  

Como alternativa, você pode adicionar as informações de DSN para um arquivo de modelo e execute o seguinte comando para adicionar ao `~/.odbc.ini` :
 - **Odbcinst -i -s -f** *template_file*  
 
Você pode verificar se o driver está funcionando usando `isql` testar a conexão, ou você pode usar este comando:
 - **master.INFORMATION_SCHEMA.TABLES BCP out OutFile.dat -S <server> - U <name> - P<password>**  

## <a name="using-secure-sockets-layer-ssl"></a>Usando o protocolo SSL (Secure Sockets Layer)  
Você pode usar o protocolo (SSL) para criptografar conexões para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. SSL protege [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] nomes de usuário e senhas pela rede. O SSL também verifica a identidade do servidor para proteger contra ataques “man-in-the-middle” (MITM).  

Habilitar a criptografia aumenta a segurança, mas reduz o desempenho.

Para obter mais informações, consulte [criptografando conexões com o SQL Server](http://go.microsoft.com/fwlink/?LinkId=220900) e [usando criptografia sem validação](https://docs.microsoft.com/en-us/sql/relational-databases/native-client/features/using-encryption-without-validation).

Independentemente das configurações para **Encrypt** e **TrustServerCertificate**, as credenciais de logon do servidor (nome de usuário e senha) sempre são criptografadas. A tabela a seguir mostra o efeito das configurações de **Encrypt** e **TrustServerCertificate** .  

||**TrustServerCertificate = não**|**TrustServerCertificate = yes**|  
|-|-------------------------------------|------------------------------------|  
|**Criptografar = não**|O certificado do servidor não é verificado.<br /><br />Os dados enviados entre cliente e servidor não são criptografados.|O certificado do servidor não é verificado.<br /><br />Os dados enviados entre cliente e servidor não são criptografados.|  
|**Criptografar = Sim**|O certificado do servidor é verificado.<br /><br />Os dados enviados entre cliente e servidor são criptografados.<br /><br />O nome (ou endereço IP) em uma entidade CN (nome comum) ou assunto SAN (nome alternativo) em um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] certificado SSL deve corresponder exatamente, o servidor nome (ou endereço IP) especificado na cadeia de conexão.|O certificado do servidor não é verificado.<br /><br />Os dados enviados entre cliente e servidor são criptografados.|  

Por padrão, conexões criptografadas sempre verificam o certificado do servidor. No entanto, se você se conectar a um servidor que tenha um certificado autoassinado, adicione também a `TrustServerCertificate` opção para ignorar a verificação do certificado com a lista de autoridades de certificação confiáveis:  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
O SSL usa a biblioteca OpenSSL. A tabela a seguir mostra as versões mínimas com suporte do OpenSSL e os locais dos repositórios de confiança de certificado para cada plataforma:

|Plataforma|Versão mínima do OpenSSL|Local do repositório de confiança de certificado padrão|  
|------------|---------------------------|--------------------------------------------|
|Debian 8.71 |1.0.1T|/etc/ssl/certs|
|macOS 10.12|1.0.2k|/usr/local/etc/OpenSSL/certs|
|OS X 10.11|1.0.2J|/usr/local/etc/OpenSSL/certs|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|  
|Red Hat Enterprise Linux 7|1.0.1E|/etc/pki/tls/cert.pem|
|SuSE Linux Enterprise 12 |1.0.1I|/etc/ssl/certs|
|Ubuntu 15.10 |1.0.2D|/etc/ssl/certs|
|Ubuntu 16.04 |1.0.2G|/etc/ssl/certs|
|Ubuntu 16.10 |1.0.2G|/etc/ssl/certs|
  
Você também pode especificar criptografia na cadeia de conexão usando o `Encrypt` ao usar a opção **SQLDriverConnect** para se conectar.

## <a name="see-also"></a>Consulte também  
[Instalando o Microsoft ODBC Driver for SQL Server no Linux e macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)  
[Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md)

