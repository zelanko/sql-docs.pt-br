---
title: Criptografar conexões com o SQL Server em Linux
description: Este artigo descreve como Criptografar conexões para o SQL Server em Linux.
ms.date: 01/30/2018
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
helpviewer_keywords:
- Linux, encrypted connections
ms.openlocfilehash: 975a312988a7df4bdb4fb2858d7b0fcbe95cea33
ms.sourcegitcommit: 6413b7495313830ad1ae5aefe0c09e8e7a284b07
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016860"
---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>Criptografar conexões com o SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux pode usar o protocolo TLS para criptografar os dados transmitidos por uma rede entre um aplicativo cliente e uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é compatível com os mesmos protocolos TLS no Windows e no Linux: TLS 1.2, 1.1 e 1.0. No entanto, as etapas para configurar o TLS são específicas para o sistema operacional no qual o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está em execução.  

## <a name="requirements-for-certificates"></a>Requisitos para Certificados 
Antes de começar, você precisa verificar se os certificados seguem estes requisitos:
- A hora do sistema atual deve ser posterior à propriedade Válido de do certificado e anterior à propriedade Válido para do certificado.
- O certificado deve ser significativo para a autenticação do servidor. Isso exige a propriedade Uso Avançado de Chave do certificado para especificar a Autenticação do Servidor (1.3.6.1.5.5.7.3.1).
- O certificado deve ser criado usando a opção KeySpec de AT_KEYEXCHANGE. Normalmente, a propriedade de uso de chave do certificado (KEY_USAGE) também inclui a codificação de chaves (CERT_KEY_ENCIPHERMENT_KEY_USAGE).
- A propriedade Assunto do certificado deve indicar que o nome comum (CN) é igual ao nome do host ou ao nome de domínio totalmente qualificado (FQDN) do computador servidor. Observação: Há suporte para certificados curinga.

## <a name="configuring-the-openssl-libraries-for-use-optional"></a>Como configurar bibliotecas OpenSSL para uso (opcional)
Você pode criar links simbólicos no diretório `/opt/mssql/lib/` que fazem referência a quais bibliotecas `libcrypto.so` e `libssl.so` devem ser usadas para criptografia. Isso será útil se você quiser forçar o SQL Server a usar uma versão específica do OpenSSL diferente da versão padrão fornecida pelo sistema. Se esses links simbólicos não estiverem presentes, o SQL Server carregará as bibliotecas do OpenSSL padrão configuradas no sistema.

Esses links simbólicos devem se chamar `libcrypto.so` e `libssl.so` e ser colocados no diretório `/opt/mssql/lib/`.

## <a name="overview"></a>Visão geral
O TLS é usado para criptografar conexões de um aplicativo cliente para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Quando configurado corretamente, o TLS fornece privacidade e integridade de dados para comunicações entre o cliente e o servidor.  As conexões TLS podem ser iniciadas pelo cliente ou iniciadas pelo servidor. 

## <a name="client-initiated-encryption"></a>Criptografia Iniciada pelo Cliente 
- **Gerar certificado** (/CN deve corresponder ao nome de domínio totalmente qualificado do host do SQL Server)

> [!NOTE]
> Para este exemplo, usamos um certificado autoassinado, o que não deve ser usado para cenários de produção. Você deve usar certificados de autoridade de certificação. 

        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **Configurar o SQL Server**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0 

- **Registrar o certificado no computador cliente (Windows, Linux ou macOS)**

    -   Se você estiver usando um certificado assinado por AC, precisará copiar o certificado de AC (Autoridade de Certificação), em vez do certificado do usuário para o computador cliente. 
    -   Se você estiver usando o certificado autoassinado, bastará copiar o arquivo .pem para as pastas a seguir respectivas à distribuição e executar os comandos para habilitá-lo 
        - **Ubuntu**: Copie o certificado ```/usr/share/ca-certificates/``` para alterar o nome da extensão para .CRT; use dpkg-reconfigure ca-certificates para habilitá-la como um Certificado de Autoridade de Certificação do sistema. 
        - **RHEL**: Copie o certificado para ```/etc/pki/ca-trust/source/anchors/``` e use ```update-ca-trust``` para habilitá-lo como Certificado de Autoridade de Certificação do sistema.
        - **SUSE**: Copie o certificado para ```/usr/share/pki/trust/anchors/``` e use ```update-ca-certificates``` para habilitá-lo como Certificado de Autoridade de Certificação do sistema.
        - **Windows**:  Importar o arquivo .pem como um certificado sob o usuário atual-> autoridades de certificação raiz confiáveis -> certificados
        - **macOS**: 
           - Copie o certificado para ```/usr/local/etc/openssl/certs```
           - Execute o seguinte comando para obter o valor de hash: ```/usr/local/Cellar/openssl/1.0.2l/openssl x509 -hash -in mssql.pem -noout```
           - Altere o nome do certificado para o valor. Por exemplo: ```mv mssql.pem dc2dd900.0```. Verifique se dc2dd900.0 está em ```/usr/local/etc/openssl/certs```
    
-   **Cadeias de conexão de exemplo** 

    - **[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]**   
  ![Caixa de diálogo de conexão SSMS](media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "Caixa de diálogo de conexão SSMS")  
  
    - **SQLCMD** 

            sqlcmd  -S <sqlhostname> -N -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=True; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=Yes; TrustServerCertificate=no;" 
    - **JDBC** 
    
            "encrypt=true; trustServerCertificate=false;" 

## <a name="server-initiated-encryption"></a>Criptografia Iniciada pelo Servidor 

- **Gerar certificado** (/CN deve corresponder ao nome de domínio totalmente qualificado do host do SQL Server)
        
        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **Configurar o SQL Server**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 1 
        
-   **Cadeias de conexão de exemplo** 

    - **SQLCMD**

            sqlcmd  -S <sqlhostname> -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=False; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=no; TrustServerCertificate=no;"  
    - **JDBC** 
    
            "encrypt=false; trustServerCertificate=false;" 
            
> [!NOTE]
> Defina **TrustServerCertificate** como true se o cliente não puder se conectar à AC para validar a autenticidade do certificado

## <a name="common-connection-errors"></a>Erros de conexão comuns  

|Mensagem de erro |Fix |
|--- |--- |
|A cadeia de certificados foi emitida por uma autoridade que não é confiável.  |Esse erro ocorre quando os clientes não conseguem verificar a assinatura no certificado apresentado por SQL Server durante o handshake de TLS. Verifique se o cliente confia no certificado [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] diretamente ou na AC que assinou o certificado do SQL Server. |
|O nome da entidade de destino está incorreto.  |Verifique se o campo nome comum no certificado do SQL Server corresponde ao nome do servidor especificado na cadeia de conexão do cliente. |  
|uma conexão existente foi fechada forçadamente pelo host remoto. |Esse erro pode ocorrer quando o cliente não é compatível com a versão do protocolo TLS exigida pelo SQL Server. Por exemplo, se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] estiver configurado para exigir o TLS 1.2, verifique se os clientes também são compatíveis com o protocolo TLS 1.2. |
| | |   
