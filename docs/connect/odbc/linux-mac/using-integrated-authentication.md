---
title: Usando a autenticação integrada | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- integrated authentication
ms.assetid: 9499ffdf-e0ee-4d3c-8bca-605371eb52d9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 24fce778851f514d680a2701cc9c4dcc9ccb277c
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52419067"
---
# <a name="using-integrated-authentication"></a>Como usar a autenticação integrada
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

O [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Linux e macOS é compatível com conexões que usam a autenticação integrada Kerberos. Ele é compatível com o KDC (centro de distribuição de chaves) do MIT Kerberos e funciona com as bibliotecas do Kerberos v5 e GSSAPI (Interface de Programação de Aplicativo de Serviços Genéricos de Segurança).
  
## <a name="using-integrated-authentication-to-connect-to-includessnoversionincludesssnoversion-mdmd-from-an-odbc-application"></a>Uso de autenticação integrada para se conectar ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de um aplicativo ODBC  

Você pode habilitar a autenticação integrada do Kerberos especificando **Trusted_Connection=yes** na cadeia de conexão do **SQLDriverConnect** ou do **SQLConnect**. Por exemplo:  

```
Driver='ODBC Driver 13 for SQL Server';Server=your_server;Trusted_Connection=yes  
```
  
Ao se conectar com um DSN, você também pode adicionar **Trusted_Connection = yes** para a entrada DSN em `odbc.ini`.
  
O `-E` opção de `sqlcmd` e o `-T` opção dos `bcp` também pode ser usado para especificar a autenticação integrada; consulte [conectando com **sqlcmd** ](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md) e [ Conectar-se com **bcp** ](../../../connect/odbc/linux-mac/connecting-with-bcp.md) para obter mais informações.

Verifique se a entidade de segurança do cliente que vai se conectar ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] já está autenticada com o KDC do Kerberos.
  
Não há suporte para**ServerSPN** e **FailoverPartnerSPN** .  
  
## <a name="deploying-a-linux-or-macos-odbc-driver-application-designed-to-run-as-a-service"></a>Implantando o Linux ou macOS ODBC Driver aplicativo desenvolvido para execução como um serviço

Um administrador do sistema pode implantar um aplicativo para ser executado como um serviço que usa a Autenticação Kerberos para se conectar ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
Você precisa primeiro configurar o Kerberos no cliente e então verificar se o aplicativo pode usar a credencial Kerberos da entidade de segurança padrão.

Verifique se está usando o `kinit` ou PAM (módulo de autenticação conectável) para obter e armazenar em cache o TGT para a entidade de segurança que a conexão usa por meio de um dos seguintes métodos:  
  
-   Execute `kinit`, passando um nome da entidade de segurança e uma senha.  
  
-   Execute o `kinit`, passando um nome da entidade de segurança e um local de um arquivo keytab contendo a chave da entidade de segurança criada pelo `ktutil`.  
  
-   Verifique se o logon no sistema foi feito usando o PAM (módulo de autenticação conectável) do Kerberos.

Quando um aplicativo é executado como um serviço, porque as credenciais do Kerberos expiram por padrão, renove as credenciais para garantir a disponibilidade contínua do serviço. O driver ODBC não renova as credenciais em si; Verifique se há um `cron` trabalho ou script executado periodicamente para renovar as credenciais antes da expiração. Para evitar a exigência de senha para cada renovação, você pode usar um arquivo keytab.  
  
Detalhes sobre formas de aplicar o Kerberos em serviços no Linux são fornecidos em[Kerberos Configuration and Use](https://commons.oreilly.com/wiki/index.php/Linux_in_a_Windows_World/Centralized_Authentication_Tools/Kerberos_Configuration_and_Use) .
  
## <a name="tracking-access-to-a-database"></a>Acompanhando o acesso a um banco de dados

Um administrador de banco de dados pode criar uma trilha de auditoria de acesso a um banco de dados usando contas do sistema para acessar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a Autenticação Integrada.  
  
O logon no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa a conta do sistema e não há nenhuma funcionalidade no Linux para representar o contexto de segurança. Portanto, é necessário mais que isso para determinar o usuário.
  
Para auditar atividades no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em nome dos usuários além da conta do sistema, o aplicativo deve usar [!INCLUDE[tsql](../../../includes/tsql-md.md)] **EXECUTE AS**.  
  
Para melhorar o desempenho do aplicativo, um aplicativo pode usar o pool de conexões com Autenticação Integrada e auditoria. No entanto, a combinação do pool de conexões, da Autenticação Integrada e da auditoria gera um risco de segurança, pois o gerenciador do driver unixODBC permite que diferentes usuários reutilizem conexões em pool. Para obter mais informações, consulte [ODBC Connection Pooling](https://www.unixodbc.org/doc/conn_pool.html).  

Antes da reutilização, um aplicativo deve redefinir conexões em pool executando `sp_reset_connection`.  

## <a name="using-active-directory-to-manage-user-identities"></a>Usando o Active Directory para gerenciar identidades de usuário

Um administrador de sistema do aplicativo não precisa gerenciar conjuntos separados de credenciais de logon para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. É possível configurar o Active Directory como um centro de distribuição de chaves (KDC) para Autenticação Integrada. Ver [Microsoft Kerberos](/windows/desktop/SecAuthN/microsoft-kerberos) para obter mais informações.

## <a name="using-linked-server-and-distributed-queries"></a>Usando servidor vinculado e consultas distribuídas

Os desenvolvedores podem implantar um aplicativo que usa um servidor vinculado ou consultas distribuídas sem um administrador de banco de dados que mantenha conjuntos separados de credenciais SQL. Nessa situação, um desenvolvedor deve configurar um aplicativo para usar a autenticação integrada:  
  
-   O usuário faz logon em um computador cliente e se autentica no servidor de aplicativos.  
  
-   O servidor de aplicativos é autenticado como um banco de dados diferente e se conecta ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se autentica como um usuário de banco de dados para outro banco de dados ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]).  
  
Depois que a autenticação integrada for configurada, as credenciais serão passadas para o servidor vinculado.  
  
## <a name="integrated-authentication-and-sqlcmd"></a>Autenticação integrada e sqlcmd
Para acessar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a autenticação integrada, use a opção `-E` de `sqlcmd`. Certifique-se de que a conta que executa `sqlcmd` é associado à entidade de cliente do Kerberos padrão.

## <a name="integrated-authentication-and-bcp"></a>Autenticação Integrada e bcp
Para acessar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a autenticação integrada, use a opção `-T` de `bcp`. Certifique-se de que a conta que executa `bcp` é associado à entidade de cliente do Kerberos padrão. 
  
É um erro usar `-T` com o `-U` ou `-P` opção.
  
## <a name="supported-syntax-for-an-spn-registered-by-includessnoversionincludesssnoversion-mdmd"></a>Sintaxe com suporte para um SPN registrado pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]

A sintaxe que os SPNs usam em cadeia de conexão ou atributos de conexão é a seguinte:  

|Sintaxe|Descrição|  
|----------|---------------|  
|MSSQLSvc/*fqdn*:*port*|O SPN padrão gerado pelo provedor quando o protocolo TCP é usado. *port* é um número de porta TCP. *fqdn* é um nome de domínio totalmente qualificado.|  
  
## <a name="authenticating-a-linux-or-macos-computer-with-active-directory"></a>Autenticando um computador Linux ou macOS com o Active Directory

Para configurar o Kerberos, inserir dados o `krb5.conf` arquivo. `krb5.conf` está na `/etc/` , mas você pode fazer referência a outro arquivo usando a sintaxe, por exemplo, `export KRB5_CONFIG=/home/dbapp/etc/krb5.conf`. A seguir, é mostrado um arquivo `krb5.conf` de exemplo:  
  
```  
[libdefaults]  
default_realm = YYYY.CORP.CONTOSO.COM  
dns_lookup_realm = false  
dns_lookup_kdc = true  
ticket_lifetime = 24h  
forwardable = yes  
  
[domain_realm]  
.yyyy.corp.contoso.com = YYYY.CORP.CONTOSO.COM  
.zzzz.corp.contoso.com = ZZZZ.CORP.CONTOSO.COM  
```  
  
Se o computador Linux ou macOS está configurado para usar a configuração de protocolo DHCP (Dynamic Host) com o servidor DHCP do Windows fornecendo os servidores DNS para usar, você pode usar **dns_lookup_kdc = true**. Agora, você pode usar o Kerberos para entrar no seu domínio emitindo o comando `kinit alias@YYYY.CORP.CONTOSO.COM`. Os parâmetros passados para `kinit` diferenciam maiusculas de minúsculas e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] configurado para estar no domínio do computador deve ter esse usuário `alias@YYYY.CORP.CONTOSO.COM` adicionado para logon. Agora você pode usar conexões confiáveis (**Trusted_Connection=YES** em uma cadeia de conexão, **bcp -T** ou **sqlcmd -E**).  
  
A hora no computador Linux ou macOS e a hora no Centro de distribuição de chaves para Kerberos (KDC) devem ser próximas. Verifique se a hora do seu sistema está definida corretamente, por exemplo, usando o protocolo NTP.  

Se a autenticação Kerberos falhar, o driver ODBC do Linux ou macOS não usará autenticação NTLM.  

Para obter mais informações sobre a autenticação de computadores Linux ou macOS com o Active Directory, consulte [autenticar clientes Linux com Active Directory](https://technet.microsoft.com/magazine/2008.12.linux.aspx#id0060048) e [as práticas recomendadas para integrar o OS X com o Active Directory](https://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf). Para obter mais informações sobre como configurar o Kerberos, consulte o [MIT Kerberos documentação](https://web.mit.edu/kerberos/krb5-1.12/doc/index.html).

## <a name="see-also"></a>Consulte Também  
[Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md)

[Notas de versão](../../../connect/odbc/linux-mac/release-notes.md)

[Como usar o Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md)
