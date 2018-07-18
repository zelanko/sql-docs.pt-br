---
title: Criptografar conexões ao SQL Server no Linux | Microsoft Docs
description: Este artigo descreve criptografando conexões com o SQL Server no Linux.
author: tmullaney
ms.date: 01/30/2018
ms.author: meetb
manager: craigg
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
helpviewer_keywords:
- Linux, encrypted connections
ms.openlocfilehash: f7b1dd57af300fc3e3fa61e469646211536b4653
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38001818"
---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>Criptografar conexões ao SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux é possível usar segurança de camada de transporte (TLS) para criptografar dados transmitidos em uma rede entre um aplicativo cliente e uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] oferece suporte os mesmos protocolos TLS no Windows e Linux: TLS 1.0, 1.1 e 1.2. No entanto, as etapas para configurar TLS são específicas para o sistema operacional no qual [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está em execução.  

## <a name="requirements-for-certificates"></a>Requisitos de certificados 
Antes de começar, você precisa certificar-se de que seus certificados siga estes requisitos:
- A hora atual do sistema deve ser posterior o válido de propriedade do certificado e antes do válido para a propriedade do certificado.
- O certificado deve ser significativo para a autenticação do servidor. Isso requer que a propriedade de uso avançado de chave do certificado para especificar a autenticação do servidor (1.3.6.1.5.5.7.3.1).
- O certificado deve ser criado usando a opção KeySpec de AT_KEYEXCHANGE. Normalmente, a propriedade de uso da chave do certificado (KEY_USAGE) também inclui codificação de chave (CERT_KEY_ENCIPHERMENT_KEY_USAGE).
- A propriedade da entidade do certificado deve indicar que o nome comum (CN) é o mesmo como o nome do host ou nome de domínio totalmente qualificado (FQDN) do computador servidor. Observação: certificados curinga têm suporte. 

## <a name="overview"></a>Visão geral
TLS é usado para criptografar conexões a partir de um aplicativo cliente para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Quando configurado corretamente, o TLS fornece privacidade e integridade dos dados para as comunicações entre o cliente e o servidor.  Conexões de TLS podem ser iniciada do cliente ou servidor iniciada. 


## <a name="client-initiated-encryption"></a>Criptografia iniciada pelo cliente 
- **Gerar certificado** (/CN deve corresponder ao seu nome de domínio totalmente qualificado do host do SQL Server)

> [!NOTE]
> Neste exemplo, podemos usar um certificado autoassinado, isso não deve ser usado para cenários de produção. Você deve usar certificados de autoridade de certificação. 

        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **Configurar o SQL Server**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0 

- **Registrar o certificado no computador cliente (Windows, Linux ou macOS)**

    -   Se você estiver usando um certificado de AC assinado, você precisa copiar o certificado de autoridade de certificação (CA) em vez do certificado de usuário para o computador cliente. 
    -   Se você estiver usando o certificado autoassinado, basta copiar o arquivo. PEM para as seguintes pastas respectivas a distribuição e execute os comandos para habilitá-los 
        - **Ubuntu**: cert de cópia para ```/usr/share/ca-certificates/``` renomeação de extensão para. crt usar certificados de AC de dpkg reconfigure para habilitá-lo como certificado de autoridade de certificação do sistema. 
        - **RHEL**: cert de cópia para ```/etc/pki/ca-trust/source/anchors/``` usar ```update-ca-trust``` para habilitá-lo como certificado de autoridade de certificação do sistema.
        - **SUSE**: cert de cópia para ```/usr/share/pki/trust/anchors/``` usar ```update-ca-certificates``` para habilitá-lo como certificado de autoridade de certificação do sistema.
        - **Windows**: importar o arquivo. PEM como um certificado de usuário atual -> confiável autoridades de certificação raiz -> certificados
        - **macOS**: 
           - Copie o certificado para ```/usr/local/etc/openssl/certs```
           - Execute o seguinte comando para obter o valor de hash: ```/usr/local/Cellar/openssql/1.0.2l/openssql x509 -hash -in mssql.pem -noout```
           - Renomeie o certificado para o valor. Por exemplo: ```mv mssql.pem dc2dd900.0```. Verifique se dc2dd900.0 está em ```/usr/local/etc/openssl/certs```
    
-   **Cadeias de conexão de exemplo** 

    - **[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]**   
  ![Caixa de diálogo de conexão de SSMS](media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "caixa de diálogo de conexão SSMS")  
  
    - **SQLCMD** 

            sqlcmd  -S <sqlhostname> -N -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=True; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=Yes; TrustServerCertificate=no;" 
    - **JDBC** 
    
            "encrypt=true; trustServerCertificate=false;" 

## <a name="server-initiated-encryption"></a>Criptografia iniciada pelo servidor 

- **Gerar certificado** (/CN deve corresponder ao seu nome de domínio totalmente qualificado do host do SQL Server)
        
        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **Configurar o SQL Server**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key 
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
> Definir **TrustServerCertificate** como True se o cliente não pode se conectar à autoridade de certificação para validar a autenticidade do certificado

## <a name="common-connection-errors"></a>Erros comuns de conexão  

|Mensagem de erro |Fix |
|--- |--- |
|A cadeia de certificado foi emitida por uma autoridade que não é confiável.  |Esse erro ocorre quando os clientes não conseguem verificar a assinatura no certificado apresentado pelo SQL Server durante o handshake TLS. Verifique se o cliente confia em qualquer um de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] certificado diretamente, ou a autoridade de certificação que assinou o certificado do SQL Server. |
|O nome da entidade de destino está incorreto.  |Certifique-se de que o campo de nome comum no certificado do SQL Server corresponde ao nome de servidor especificado na cadeia de conexão do cliente. |  
|Uma conexão existente foi fechada forçadamente pelo host remoto. |Esse erro pode ocorrer quando o cliente não dá suporte para a versão do protocolo TLS requerida pelo SQL Server. Por exemplo, se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está configurado para exigir o TLS 1.2, verifique se os clientes também suportam o protocolo TLS 1.2. |
| | |   
