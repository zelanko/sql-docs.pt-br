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
ms.openlocfilehash: 486d26dd3afeb91cb43181875e22592fb482af5f
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702801"
---
# <a name="connecting-to-sql-server"></a>Conectar-se ao SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este tópico discute como você pode criar uma conexão com um banco de dados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="connection-properties"></a>Propriedades da conexão  

Consulte o [DSN e as palavras-chave da cadeia de conexão e os atributos](../../../connect/odbc/dsn-connection-string-attribute.md) para todas as palavras-chave da cadeia de conexão e os atributos com suporte no Linux e no Mac

> [!IMPORTANT]  
> Ao se conectar a um banco de dados que use o espelhamento de banco de dados (tem um parceiro de failover), não especifique o nome do banco de dados na cadeia de conexão. Em vez disso, envie um comando **use** _database_name_ para se conectar ao banco de dados antes de executar suas consultas.  
  
O valor passado para a palavra-chave do **Driver** pode ser um dos seguintes:  
  
-   O nome usado quando você instalou o driver.

-   O caminho para a biblioteca de drivers, que foi especificada no arquivo .ini de modelo usado para instalar o driver.  

Para criar um DSN, crie (se necessário) e edite o arquivo **~/.ODBC.ini** (`.odbc.ini` em seu diretório base) para que um DSN de usuário seja acessível somente para o `/etc/odbc.ini` usuário atual ou para um DSN de sistema (privilégios administrativos necessários). Este é um arquivo de exemplo que mostra as entradas necessárias para um DSN:  

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

Opcionalmente, você pode especificar o protocolo e a porta para se conectar ao servidor. Por exemplo, **Server = TCP:** _nomedoservidor_ **, 12345**. Observe que o único protocolo suportado pelos drivers Linux e macOS é `tcp`.

Para se conectar a uma instância nomeada em uma porta estática, use <b>Server=</b>*servername*,**port_number**. Não há suporte para se conectar a uma porta dinâmica antes da versão 17.4.

Como alternativa, você pode adicionar as informações de DSN a um arquivo de modelo e executar o comando a seguir para adicioná-lo a `~/.odbc.ini`:
 - **odbcinst -i -s -f** _template_file_  
 
Você pode verificar se o driver está funcionando usando `isql` o para testar a conexão ou pode usar este comando:
 - **bcp master.INFORMATION_SCHEMA.TABLES out OutFile.dat -S <server> -U <name> -P <password>**  

## <a name="using-secure-sockets-layer-ssl"></a>Usando o protocolo SSL (Secure Sockets Layer)  
Você pode usar o protocolo SSL para criptografar conexões com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O SSL protege nomes de usuário e senhas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na rede. O SSL também verifica a identidade do servidor para proteger contra ataques “man-in-the-middle” (MITM).  

Habilitar a criptografia aumenta a segurança, mas reduz o desempenho.

Para obter mais informações, consulte [Criptografando conexões para SQL Server](https://go.microsoft.com/fwlink/?LinkId=220900) e [usando criptografia sem validação](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation).

Independentemente das configurações para **Encrypt** e **TrustServerCertificate**, as credenciais de logon do servidor (nome de usuário e senha) sempre são criptografadas. A tabela a seguir mostra o efeito das configurações de **Encrypt** e **TrustServerCertificate** .  

||**TrustServerCertificate=no**|**TrustServerCertificate=yes**|  
|-|-------------------------------------|------------------------------------|  
|**Encrypt=no**|O certificado do servidor não é verificado.<br /><br />Os dados enviados entre cliente e servidor não são criptografados.|O certificado do servidor não é verificado.<br /><br />Os dados enviados entre cliente e servidor não são criptografados.|  
|**Encrypt=yes**|O certificado do servidor é verificado.<br /><br />Os dados enviados entre cliente e servidor são criptografados.<br /><br />O nome (ou endereço IP) em um Nome Comum da Entidade (CN) ou o Nome Alternativo da Entidade (SAN) em um certificado SSL do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve corresponder exatamente ao nome do servidor (ou endereço IP) especificado na cadeia de conexão. Subject Common Name|O certificado do servidor não é verificado.<br /><br />Os dados enviados entre cliente e servidor são criptografados.|  

Por padrão, conexões criptografadas sempre verificam o certificado do servidor. No entanto, se você se conectar a um servidor que tem um certificado autoassinado, adicione `TrustServerCertificate` também a opção para ignorar a verificação do certificado em relação à lista de autoridades de certificação confiáveis:  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
O SSL usa a biblioteca OpenSSL. A tabela a seguir mostra as versões mínimas com suporte do OpenSSL e os locais dos repositórios de confiança de certificado para cada plataforma:

|Plataforma|Versão mínima do OpenSSL|Local do repositório de confiança de certificado padrão|  
|------------|---------------------------|--------------------------------------------|
|Debian 10|1.1.1|/etc/ssl/certs|
|Debian 9|1.1.0|/etc/ssl/certs|
|Debian 8.71|1.0.1|/etc/ssl/certs|
|OS X 10,11, macOS 10,12, 10,13, 10,14|1.0.2|/usr/local/etc/openssl/certs|
|Red Hat Enterprise Linux 8|1.1.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 7|1.0.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|
|SuSE Linux Enterprise 15|1.1.0|/etc/ssl/certs|
|SuSE Linux Enterprise 11, 12|1.0.1|/etc/ssl/certs|
|Ubuntu 18.10, 19.04|1.1.1|/etc/ssl/certs|
|Ubuntu 18.04|1.1.0|/etc/ssl/certs|
|Ubuntu 16.04, 16.10, 17.10|1.0.2|/etc/ssl/certs|
|Ubuntu 14.04|1.0.1|/etc/ssl/certs|

Você também pode especificar a criptografia na cadeia de conexão usando `Encrypt` a opção ao usar o **SQLDriverConnect** para se conectar.

## <a name="adjusting-the-tcp-keep-alive-settings"></a>Ajustando as configurações de Keep-Alive TCP

A partir do driver ODBC 17,4, com que frequência o driver envia pacotes Keep-Alive e os retransmite quando uma resposta não é recebida é configurável.
Para configurar o, adicione as seguintes configurações à seção do driver no `odbcinst.ini`ou na seção do DSN em. `odbc.ini` Ao se conectar com um DSN, o driver usará as configurações na seção do DSN, se presente; caso contrário, ou se estiver se conectando apenas a uma cadeia de conexão, ela usará as configurações na `odbcinst.ini`seção do driver em. Se a configuração não estiver presente em qualquer local, o driver usará o valor padrão.

- `KeepAlive=<integer>`controla com que frequência o TCP tenta verificar se uma conexão ociosa ainda está intacta enviando um pacote keep-alive. O padrão é **30** segundos.

- `KeepAliveInterval=<integer>`determina o intervalo que separa as retransmissões de Keep-Alive até que uma resposta seja recebida.  O padrão é **1** segundo.


## <a name="see-also"></a>Consulte Também  
[Instalando o Microsoft ODBC Driver for SQL Server em Linux e macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)  
[Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md)
