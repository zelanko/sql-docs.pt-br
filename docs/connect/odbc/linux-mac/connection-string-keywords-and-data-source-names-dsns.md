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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d323481aaf3e12da9786a3b02f21f47c3c98f7cf
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924536"
---
# <a name="connecting-to-sql-server"></a>Conectar-se ao SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este tópico discute como você pode criar uma conexão com um banco de dados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="connection-properties"></a>Propriedades da conexão  

Consultar [DNS e palavras-chave e atributos da cadeia de conexão](../../../connect/odbc/dsn-connection-string-attribute.md) para ver todas as palavras-chave e atributos da cadeia de conexão compatíveis com Linux e Mac

> [!IMPORTANT]  
> Ao se conectar a um banco de dados que use o espelhamento de banco de dados (tem um parceiro de failover), não especifique o nome do banco de dados na cadeia de conexão. Em vez disso, envie um comando **use** _database_name_ para se conectar ao banco de dados antes de executar suas consultas.  
  
O valor passado para a palavra-chave **Driver** pode ser um dos seguintes:  
  
-   O nome usado quando você instalou o driver.

-   O caminho para a biblioteca de drivers, que foi especificada no arquivo .ini de modelo usado para instalar o driver.  

Para criar um DSN, gere (se necessário) e edite o arquivo **~/.odbc.ini** (`.odbc.ini` em seu diretório base) para um DSN de Usuário acessível somente ao usuário atual ou `/etc/odbc.ini` para um DSN de Sistema (requer privilégios administrativos). Veja abaixo um arquivo de exemplo que mostra as entradas mínimas necessárias para um DSN:  

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

Opcionalmente, você pode especificar o protocolo e a porta para se conectar ao servidor. Por exemplo, **Server = TCP:** _ServerName_ **, 12345**. Observe que o único protocolo compatível com os drivers do Linux e do macOS é o `tcp`.

Para se conectar a uma instância nomeada em uma porta estática, use <b>Server=</b>*servername*,**port_number**. Não há suporte para se conectar a uma porta dinâmica antes da versão 17.4.

Como alternativa, você pode adicionar as informações de DSN a um arquivo de modelo e executar o comando a seguir para adicioná-lo a `~/.odbc.ini`:
 - **odbcinst -i -s -f** _template_file_  
 
Você pode verificar se o driver está funcionando usando `isql` para testar a conexão ou pode usar o seguinte comando:
 - **bcp master.INFORMATION_SCHEMA.TABLES out OutFile.dat -S <server> -U <name> -P <password>**  

## <a name="using-secure-sockets-layer-ssl"></a>Usando o protocolo SSL (Secure Sockets Layer)  
Você pode usar o protocolo SSL para criptografar conexões com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O SSL protege nomes de usuário e senhas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na rede. O SSL também verifica a identidade do servidor para proteger contra ataques “man-in-the-middle” (MITM).  

Habilitar a criptografia aumenta a segurança, mas reduz o desempenho.

Para obter mais informações, confira [Criptografar conexões para o SQL Server](https://go.microsoft.com/fwlink/?LinkId=220900) e [Usar criptografia sem validação](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation).

Independentemente das configurações para **Encrypt** e **TrustServerCertificate**, as credenciais de logon do servidor (nome de usuário e senha) sempre são criptografadas. A tabela a seguir mostra o efeito das configurações de **Encrypt** e **TrustServerCertificate** .  

||**TrustServerCertificate=no**|**TrustServerCertificate=yes**|  
|-|-------------------------------------|------------------------------------|  
|**Encrypt=no**|O certificado do servidor não é verificado.<br /><br />Os dados enviados entre cliente e servidor não são criptografados.|O certificado do servidor não é verificado.<br /><br />Os dados enviados entre cliente e servidor não são criptografados.|  
|**Encrypt=yes**|O certificado do servidor é verificado.<br /><br />Os dados enviados entre cliente e servidor são criptografados.<br /><br />O nome (ou endereço IP) em um CN (nome comum) da entidade ou o SAN (nome alternativo da entidade) em um certificado SSL do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve corresponder exatamente ao nome do servidor (ou endereço IP) especificado na cadeia de conexão.|O certificado do servidor não é verificado.<br /><br />Os dados enviados entre cliente e servidor são criptografados.|  

Por padrão, conexões criptografadas sempre verificam o certificado do servidor. No entanto, se você se conectar a um servidor que tem um certificado autoassinado, adicione também a opção `TrustServerCertificate` para ignorar a verificação do certificado em relação à lista de autoridades de certificação confiáveis:  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
O SSL usa a biblioteca OpenSSL. A tabela a seguir mostra as versões mínimas com suporte do OpenSSL e os locais dos repositórios de confiança de certificado para cada plataforma:

|Plataforma|Versão mínima do OpenSSL|Local do repositório de confiança de certificado padrão|  
|------------|---------------------------|--------------------------------------------|
|Debian 10|1.1.1|/etc/ssl/certs|
|Debian 9|1.1.0|/etc/ssl/certs|
|Debian 8.71|1.0.1|/etc/ssl/certs|
|OS X 10.11, macOS 10.12, 10.13 e 10.14|1.0.2|/usr/local/etc/openssl/certs|
|Red Hat Enterprise Linux 8|1.1.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 7|1.0.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|
|SUSE Linux Enterprise 15|1.1.0|/etc/ssl/certs|
|SUSE Linux Enterprise 11, 12|1.0.1|/etc/ssl/certs|
|Ubuntu 18.10, 19.04|1.1.1|/etc/ssl/certs|
|Ubuntu 18.04|1.1.0|/etc/ssl/certs|
|Ubuntu 16.04, 16.10, 17.10|1.0.2|/etc/ssl/certs|
|Ubuntu 14.04|1.0.1|/etc/ssl/certs|

Você também poderá especificar a criptografia na cadeia de conexão usando a opção `Encrypt` ao empregar o **SQLDriverConnect** para se conectar.

## <a name="adjusting-the-tcp-keep-alive-settings"></a>Ajustando as configurações keep alive do TCP

Do driver ODBC 17.4 em diante, é possível configurar a frequência com que o driver envia pacotes keep alive e os retransmite quando uma resposta não é recebida.
Para configurar, adicione as configurações a seguir à seção do driver em `odbcinst.ini` ou à seção do DSN em `odbc.ini`. Ao se conectar com um DSN, o driver usará as configurações da seção do DSN, se existente; caso contrário ou se estiver se conectando somente com uma cadeia de conexão, usará as configurações da seção do driver em `odbcinst.ini`. Se a configuração não estiver presente em nenhuma das localizações, o driver usará o valor padrão.

- `KeepAlive=<integer>` controla a frequência com que o TCP tenta verificar se uma conexão ociosa ainda está intacta enviando um pacote keep alive. O padrão é **30** segundos.

- `KeepAliveInterval=<integer>` determina o intervalo que separa cada retransmissão keep alive até que uma resposta seja recebida.  O padrão é **1** segundo.

## <a name="see-also"></a>Consulte Também

- [Como instalar o Microsoft ODBC Driver for SQL Server em Linux](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [Como instalar o Microsoft ODBC Driver for SQL Server no macOS](../../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md)
- [Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md)
