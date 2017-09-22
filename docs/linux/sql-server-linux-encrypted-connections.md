---
title: "Criptografar conexões ao SQL Server no Linux | Microsoft Docs"
description: "Este tópico descreve criptografando conexões com o SQL Server no Linux."
author: tmullaney
ms.date: 06/14/2017
ms.author: thmullan;rickbyh
manager: jhubbard
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
helpviewer_keywords:
- Linux, encrypted connections
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 47a15701730019aaf166743c47c606aa2059b7fe
ms.contentlocale: pt-br
ms.lasthandoff: 08/28/2017

---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>Criptografar conexões ao SQL Server no Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]no Linux pode usar segurança de camada de transporte (TLS) para criptografar dados transmitidos em uma rede entre um aplicativo cliente e uma instância de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]suporta os mesmos protocolos TLS no Windows e Linux: TLS 1.0, 1.1 e 1.2. No entanto, as etapas para configurar TLS são específicas para o sistema operacional no qual [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está em execução.  
 
## <a name="typical-scenario"></a>Cenário típico 
TLS é usado para criptografar conexões de um aplicativo cliente para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Quando configurado corretamente, o TLS fornece privacidade e integridade dos dados para as comunicações entre o cliente e o servidor.  
As etapas a seguir descrevem um cenário típico:  

1. Administrador de banco de dados gera uma chave privada e um certificado (CSR) da solicitação de assinatura. Nome comum do CSR deve corresponder ao nome do servidor especificado por clientes em sua cadeia de caracteres de conexão do SQL Server. Esse nome comum normalmente é o nome de domínio totalmente qualificado do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host. Para usar o mesmo certificado para vários servidores, você pode usar um caractere curinga no nome comum (por exemplo, `"*.contoso.com"` em vez de `"node1.contoso.com"`).   
2. O CSR é enviado para uma autoridade de certificação (CA). A autoridade de certificação deve ser confiável para todos os computadores cliente que se conectam ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A autoridade de certificação retornará um certificado autoassinado para o administrador de banco de dados.   
3. Configura o administrador de banco de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para usar a chave privada e certificado assinado para conexões TLS.   
4. Os clientes especificar `"Encrypt=True"` e `"TrustServerCertificate=False"` nas cadeias de conexão. (Os nomes de parâmetro específicos podem ser diferentes dependendo de qual driver está sendo usado). Clientes agora tentativa de criptografar conexões ao SQL Server e verificar a validade do certificado do SQL Server para impedir ataques man-in-the-middle.  
 
## <a name="configuring-tls-on-linux"></a>Configuração de TLS em Linux  

Use `mssql-conf` para configurar TLS para uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em execução no Linux. Há suporte para as seguintes opções:  

|Opção |Description |
|--- |--- |
|`network.forceencryption` |Se for 1, em seguida, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] força todas as conexões sejam criptografados. Por padrão, essa opção é 0. |  
|`network.tlscert` |O caminho absoluto para o certificado do arquivo que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa para TLS. Exemplo: `/etc/ssl/certs/mssql.pem` o arquivo de certificado deve ser acessível pela conta mssql. A Microsoft recomenda restringir o acesso ao arquivo usando `chown mssql:mssql <file>; chmod 400 <file>`. |  
|`network.tlskey` |O caminho absoluto para a chave privada do arquivo que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa para TLS. Exemplo: `/etc/ssl/private/mssql.key` o arquivo de certificado deve ser acessível pela conta mssql. A Microsoft recomenda restringir o acesso ao arquivo usando `chown mssql:mssql <file>; chmod 400 <file>`. | 
|`network.tlsprotocols` |Uma lista separada por vírgulas de quais TLS protocolos são permitidos pelo SQL Server. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]sempre tenta negociar o protocolo permitido mais forte. Se um cliente não oferece suporte a qualquer protocolo permitido, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] rejeitará a tentativa de conexão.  Para compatibilidade, todos os protocolos com suporte são permitidos por padrão (1.2, 1.1 e 1.0).  Se os clientes oferecem suporte a TLS 1.2, a Microsoft recomenda permitindo que apenas o protocolo TLS 1.2. |  
|`network.tlsciphers` |Especifica quais codificações são permitidas por [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para TLS. Essa cadeia de caracteres deve ser formatada por [formato de lista de codificação do OpenSSL](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html). Em geral, você não precisará alterar essa opção. <br /> Por padrão, as seguintes codificações são permitidas: <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |   
| | |
 
## <a name="example"></a>Exemplo 
Este exemplo usa um certificado autoassinado. Em cenários de produção normal, o certificado deve ser assinado por uma autoridade de certificação é confiável por todos os clientes.  
 
### <a name="step-1-generate-private-key-and-certificate"></a>Etapa 1: Gerar certificado e chave privada 
Abra um comando de terminal no computador Linux onde [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está em execução. Execute os seguintes comandos:  

- Gere um certificado autoassinado. Verifique se que o /CN corresponde a seu nome de domínio totalmente qualificado do host do SQL Server. Opcionalmente, você pode usar caracteres curinga, por exemplo `'/CN=*.contoso.com'`.    
   ```  
   openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
   ```  

- Restringir o acesso ao`mssql`  
   ```  
   sudo chown mssql:mssql mssql.pem mssql.key 
   sudo chmod 600 mssql.pem mssql.key 
   ```  
 
- Mover para diretórios do sistema SSL (opcionais)  
   ```  
   sudo mv mssql.pem /etc/ssl/certs/ 
   sudo mv mssql.key /etc/ssl/private/ 
   ```  
 
### <a name="step-2-configure--includessnoversionincludesssnoversion-mdmd"></a>Etapa 2: configurar[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
Use `mssql-conf` configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para usar o certificado e a chave de TLS. Para aumentar a segurança, você também pode definir TLS 1.2 como o único protocolo permitido e forçar todos os clientes para usar conexões criptografadas.  

```  
sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pem 
sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.key 
sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
sudo /opt/mssql/bin/mssql-conf set network.forceencryption 1 
```
 
### <a name="step-3-restart-includessnoversionincludesssnoversion-mdmd"></a>Etapa 3: reiniciar[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]deve ser reiniciado para que essas alterações entrem em vigor.  
`sudo systemctl restart mssql-server`  
 
### <a name="step-4-copy-self-signed-certificate-to-client-machines"></a>Etapa 4: Copie o certificado autoassinado para computadores cliente 
Como este exemplo usa um certificado autoassinado o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host, o certificado (não a chave privada) deve ser copiado e instalado como um certificado raiz confiável em todos os computadores cliente que se conectam ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se o certificado é assinado por uma autoridade de certificação que já é confiável por todos os clientes, esta etapa não é necessária. 
 
### <a name="step-5-connect-from-clients-using-tls"></a>Etapa 5: Conectar-se de clientes que usam o TLS 
Conecte-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de um cliente com a criptografia habilitada e `TrustServerCertificate` definida como `False` na cadeia de conexão. Aqui estão alguns exemplos de como especificar esses parâmetros usando drivers e ferramentas diferentes. 

sqlcmd  
`sqlcmd -N -C -S mssql.contoso.com -U sa -P '<YourPassword>'`  

[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]   
  ![Caixa de diálogo de conexão SSMS](media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "caixa de diálogo de conexão de SSMS")  
  
ADO.NET  
`"Encrypt=true; TrustServerCertificate=true;"`  

ODBC   
`"Encrypt=yes; TrustServerCertificate=no;"`  

JDBC  
`"encrypt=true; trustServerCertificate=false;" `

 
## <a name="common-connection-errors"></a>Erros comuns de conexão  

|Mensagem de erro |Fix |
|--- |--- |
|A cadeia de certificado foi emitida por uma autoridade que não é confiável.  |Esse erro ocorre quando os clientes não conseguem verificar a assinatura no certificado apresentado pelo SQL Server durante o handshake TLS. Verifique se o cliente confia no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] certificado diretamente, ou a autoridade de certificação que assinou o certificado do SQL Server. |
|O nome da entidade de destino está incorreto.  |Certifique-se de que o campo de nome comum no certificado do SQL Server coincide com o nome do servidor especificado na cadeia de conexão do cliente. |  
|Uma conexão existente foi fechada forçadamente pelo host remoto. |Esse erro pode ocorrer quando o cliente não oferece suporte para a versão do protocolo TLS exigida pelo SQL Server. Por exemplo, se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está configurado para exigir o protocolo TLS 1.2, assegure-se de que os clientes também dão suporte ao protocolo TLS 1.2. |
| | |   


