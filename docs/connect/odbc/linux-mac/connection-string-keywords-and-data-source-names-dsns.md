---
title: Conexão ao SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data source names
- connection string keywords
- DSNs
ms.assetid: f95cdbce-e7c2-4e56-a9f7-8fa3a920a125
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09422214ac33ed7179d66a46aed9db09f2ef6039
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47805304"
---
# <a name="connecting-to-sql-server"></a>Conectar-se ao SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este tópico discute como você pode criar uma conexão com um banco de dados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="connection-properties"></a>Propriedades da conexão  

Ver [DSN e palavras-chave de cadeia de caracteres de Conexão e atributos](../../../connect/odbc/dsn-connection-string-attribute.md) para todas as palavras-chave de cadeia de caracteres de conexão e atributos que têm suportados no Linux e Mac

> [!IMPORTANT]  
> Ao se conectar a um banco de dados que use o espelhamento de banco de dados (tem um parceiro de failover), não especifique o nome do banco de dados na cadeia de conexão. Em vez disso, envie um comando **use** *database_name* para se conectar ao banco de dados antes de executar suas consultas.  
  
O valor passado para o **Driver** palavra-chave pode ser um dos seguintes:  
  
-   O nome usado quando você instalou o driver.

-   O caminho para a biblioteca de drivers, que foi especificada no arquivo .ini de modelo usado para instalar o driver.  

Para criar um DSN, crie (se necessário) e edite o arquivo **~/.odbc.ini** (`.odbc.ini` em seu diretório base) para um DSN de usuário somente é acessível para o usuário atual, ou `/etc/odbc.ini` para um DSN de sistema (privilégios administrativos necessários.) Este é um arquivo de exemplo que mostra as entradas necessárias para um DSN:  

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

Opcionalmente, você pode especificar o protocolo e a porta para se conectar ao servidor. Por exemplo, **Server = tcp:***nome_do_servidor***, 12345**. Observe que é o único protocolo com suporte pelos drivers de Linux e macOS `tcp`.

Para se conectar a uma instância nomeada em uma porta estática, use <b>Server=</b>*servername*,**port_number**. Não há suporte para se conectar a uma porta dinâmica.  

Como alternativa, você pode adicionar as informações de DSN a um arquivo de modelo e executar o comando a seguir para adicioná-lo a `~/.odbc.ini`:
 - **Odbcinst -i -s -f** *template_file*  
 
Você pode verificar se o driver está funcionando usando `isql` testar a conexão, ou você pode usar este comando:
 - **master.INFORMATION_SCHEMA.TABLES BCP out outfile -S <server> - U <name> - P <password>**  

## <a name="using-secure-sockets-layer-ssl"></a>Usando o protocolo SSL (Secure Sockets Layer)  
Você pode usar o protocolo SSL para criptografar conexões com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O SSL protege nomes de usuário e senhas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na rede. O SSL também verifica a identidade do servidor para proteger contra ataques “man-in-the-middle” (MITM).  

Habilitar a criptografia aumenta a segurança, mas reduz o desempenho.

Para obter mais informações, consulte [criptografando conexões com o SQL Server](http://go.microsoft.com/fwlink/?LinkId=220900) e [usando criptografia sem validação](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation).

Independentemente das configurações para **Encrypt** e **TrustServerCertificate**, as credenciais de logon do servidor (nome de usuário e senha) sempre são criptografadas. A tabela a seguir mostra o efeito das configurações de **Encrypt** e **TrustServerCertificate** .  

||**TrustServerCertificate = não**|**TrustServerCertificate = yes**|  
|-|-------------------------------------|------------------------------------|  
|**Encrypt=no**|O certificado do servidor não é verificado.<br /><br />Os dados enviados entre cliente e servidor não são criptografados.|O certificado do servidor não é verificado.<br /><br />Os dados enviados entre cliente e servidor não são criptografados.|  
|**Encrypt=yes**|O certificado do servidor é verificado.<br /><br />Os dados enviados entre cliente e servidor são criptografados.<br /><br />O nome (ou endereço IP) em um CN (nome comum) da entidade ou o SAN (nome alternativo da entidade) em um certificado SSL do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve corresponder exatamente ao nome do servidor (ou endereço IP) especificado na cadeia de conexão.|O certificado do servidor não é verificado.<br /><br />Os dados enviados entre cliente e servidor são criptografados.|  

Por padrão, conexões criptografadas sempre verificam o certificado do servidor. No entanto, se você se conectar a um servidor que tenha um certificado autoassinado, também adicionar o `TrustServerCertificate` opção para ignorar a verificação do certificado em relação à lista de autoridades de certificação confiável:  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
O SSL usa a biblioteca OpenSSL. A tabela a seguir mostra as versões mínimas com suporte do OpenSSL e os locais dos repositórios de confiança de certificado para cada plataforma:

|Plataforma|Versão mínima do OpenSSL|Local do repositório de confiança de certificado padrão|  
|------------|---------------------------|--------------------------------------------|
|Debian 9|1.1.0|/etc/ssl/certs|
|Debian 8.71 |1.0.1|/etc/ssl/certs|
|macOS 10.13|1.0.2|/usr/local/etc/OpenSSL/certs|
|macOS 10.12|1.0.2|/usr/local/etc/OpenSSL/certs|
|OS X 10.11|1.0.2|/usr/local/etc/OpenSSL/certs|
|Red Hat Enterprise Linux 7|1.0.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|
|SuSE Linux Enterprise 12 |1.0.1|/etc/ssl/certs|
|SuSE Linux Enterprise 11 |0.9.8|/etc/ssl/certs|
|Ubuntu 17.10 |1.0.2|/etc/ssl/certs|
|Ubuntu 16.10 |1.0.2|/etc/ssl/certs|
|Ubuntu 16.04 |1.0.2|/etc/ssl/certs|
  
Você também pode especificar a criptografia na cadeia de conexão usando o `Encrypt` ao usar a opção **SQLDriverConnect** para se conectar.

## <a name="see-also"></a>Consulte Também  
[Instalando o Microsoft ODBC Driver for SQL Server em Linux e macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)  
[Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md)
