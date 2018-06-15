---
title: Usando a autenticação integrada | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- integrated authentication
ms.assetid: 9499ffdf-e0ee-4d3c-8bca-605371eb52d9
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c70de16565cd90c3ca594fffcbbcc82bae89b90e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853171"
---
# <a name="using-integrated-authentication"></a>Como usar a autenticação integrada
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

O [!INCLUDE[msCoName](../../../includes/msconame_md.md)] o Driver ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no Linux e macOS suporta as conexões que usam Kerberos de autenticação integrada. Ele dá suporte ao centro de distribuição de chaves (KDC) do MIT Kerberos e funciona com bibliotecas de v5 genérico serviços de aplicativo programa Interface GSSAPI (segurança) e Kerberos.
  
## <a name="using-integrated-authentication-to-connect-to-includessnoversionincludesssnoversionmdmd-from-an-odbc-application"></a>Usando a autenticação integrada para se conectar ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] de um aplicativo ODBC  

Você pode habilitar a autenticação integrada Kerberos especificando **Trusted_Connection = yes** na cadeia de conexão do **SQLDriverConnect** ou **SQLConnect**. Por exemplo:  

```
Driver='ODBC Driver 13 for SQL Server';Server=your_server;Trusted_Connection=yes  
```
  
Ao se conectar com um DSN, você também pode adicionar **Trusted_Connection = yes** para a entrada do DSN em `odbc.ini`.
  
O `-E` opção de `sqlcmd` e `-T` opção de `bcp` também pode ser usado para especificar a autenticação integrada, consulte [conectando com **sqlcmd** ](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md) e [ Conectando com **bcp** ](../../../connect/odbc/linux-mac/connecting-with-bcp.md) para obter mais informações.

Certifique-se de que a entidade de segurança de cliente que irá se conectar ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] já está autenticado com o KDC do Kerberos.
  
Não há suporte para**ServerSPN** e **FailoverPartnerSPN** .  
  
## <a name="deploying-a-linux-or-macos-odbc-driver-application-designed-to-run-as-a-service"></a>Implantando um Linux ou macOS ODBC Driver aplicativo projetado para execução como um serviço

Um administrador de sistema pode implantar um aplicativo para ser executado como um serviço que usa a autenticação Kerberos para se conectar ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
Você precisa primeiro configurar o Kerberos no cliente e, em seguida, certifique-se de que o aplicativo pode usar a credencial Kerberos da entidade de segurança padrão.

Certifique-se de que você use `kinit` ou PAM (módulo de autenticação conectável) para obter e armazenar em cache o TGT para a entidade de segurança que usa a conexão, por meio de um dos seguintes métodos:  
  
-   Executar `kinit`, passando um nome e uma senha.  
  
-   Executar `kinit`, passando um nome de entidade e um local de um arquivo keytab que contém a chave da entidade criada por `ktutil`.  
  
-   Certifique-se de que o logon para o sistema foi feito usando o Kerberos do PAM (módulo de autenticação conectável).

Quando um aplicativo é executado como um serviço, porque as credenciais do Kerberos expiram, renove as credenciais para garantir a disponibilidade contínua do serviço. O driver ODBC não renova as credenciais em si; Verifique se há um `cron` trabalho ou script executado periodicamente para renovar as credenciais antes da expiração. Para evitar a exigência de senha para cada renovação, você pode usar um arquivo keytab.  
  
Detalhes sobre formas de aplicar o Kerberos em serviços no Linux são fornecidos em[Kerberos Configuration and Use](http://commons.oreilly.com/wiki/index.php/Linux_in_a_Windows_World/Centralized_Authentication_Tools/Kerberos_Configuration_and_Use) .
  
## <a name="tracking-access-to-a-database"></a>Acompanhando o acesso a um banco de dados

Um administrador de banco de dados pode criar uma trilha de auditoria de acesso a um banco de dados ao usar contas de sistema para acessar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] usando a autenticação integrada.  
  
Fazer logon no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] usa a conta do sistema e não há nenhuma funcionalidade no Linux para representar o contexto de segurança. Portanto, é necessário mais que isso para determinar o usuário.
  
Para auditar atividades no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] em nome dos usuários que não seja a conta do sistema, o aplicativo deve usar [!INCLUDE[tsql](../../../includes/tsql_md.md)] **EXECUTE AS**.  
  
Para melhorar o desempenho do aplicativo, um aplicativo pode usar o pool de conexões com Autenticação Integrada e auditoria. No entanto, a combinação de conexão do pool, a autenticação integrada e auditoria cria um risco de segurança porque o Gerenciador de driver unixODBC permite que diferentes usuários reutilizem conexões em pool. Para obter mais informações, consulte [ODBC Connection Pooling](http://www.unixodbc.org/doc/conn_pool.html).  

Antes de reutilização, um aplicativo deve redefinir conexões em pool executando `sp_reset_connection`.  

## <a name="using-active-directory-to-manage-user-identities"></a>Usando o Active Directory para gerenciar identidades de usuário

Um administrador de sistema do aplicativo não precisa gerenciar conjuntos separados de credenciais de logon para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. É possível configurar o Active Directory como um centro de distribuição de chaves (KDC) para Autenticação Integrada. Consulte [Microsoft Kerberos](https://msdn.microsoft.com/en-us/library/windows/desktop/aa378747(v=vs.85).aspx) para obter mais informações.

## <a name="using-linked-server-and-distributed-queries"></a>Usando servidor vinculado e consultas distribuídas

Os desenvolvedores podem implantar um aplicativo que usa um servidor vinculado ou consultas distribuídas sem um administrador de banco de dados que mantenha conjuntos separados de credenciais SQL. Nessa situação, um desenvolvedor deve configurar um aplicativo para usar a autenticação integrada:  
  
-   O usuário faz logon em um computador cliente e se autentica no servidor de aplicativos.  
  
-   O servidor de aplicativos é autenticado como um banco de dados diferente e se conecta ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] autentica como um usuário de banco de dados para outro banco de dados ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
Depois que a autenticação integrada for configurada, as credenciais serão passadas para o servidor vinculado.  
  
## <a name="integrated-authentication-and-sqlcmd"></a>Autenticação integrada e sqlcmd
Para acessar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] usando a autenticação integrada, use o `-E` opção de `sqlcmd`. Verifique se a conta que executa `sqlcmd` está associado à entidade de cliente do Kerberos padrão.

## <a name="integrated-authentication-and-bcp"></a>Autenticação Integrada e bcp
Para acessar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] usando a autenticação integrada, use o `-T` opção de `bcp`. Verifique se a conta que executa `bcp` está associado à entidade de cliente do Kerberos padrão. 
  
É um erro usar `-T` com o `-U` ou `-P` opção.
  
## <a name="supported-syntax-for-an-spn-registered-by-includessnoversionincludesssnoversionmdmd"></a>Sintaxe com suporte para um SPN registrado pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]

A sintaxe que os SPNs usam na cadeia de caracteres de conexão ou atributos de conexão é como segue:  

|Sintaxe|Description|  
|----------|---------------|  
|MSSQLSvc/*fqdn*:*port*|O SPN padrão gerado pelo provedor quando o protocolo TCP é usado. *port* é um número de porta TCP. *fqdn* é um nome de domínio totalmente qualificado.|  
  
## <a name="authenticating-a-linux-or-macos-computer-with-active-directory"></a>Autenticar um Linux ou macOS computador com o Active Directory

Para configurar o Kerberos, inserir dados de `krb5.conf` arquivo. `krb5.conf` está em `/etc/` , mas você pode fazer referência a outro arquivo usando a sintaxe, por exemplo, `export KRB5_CONFIG=/home/dbapp/etc/krb5.conf`. A seguir está um exemplo `krb5.conf` arquivo:  
  
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
  
Se o computador Linux ou macOS é configurado para usar o protocolo de configuração de Host dinâmico (DHCP) com um servidor DHCP do Windows fornece os servidores DNS para usar, você pode usar **dns_lookup_kdc = true**. Agora, você pode usar o Kerberos para entrar no seu domínio, emitindo o comando `kinit alias@YYYY.CORP.CONTOSO.COM`. Parâmetros passados para `kinit` diferenciam maiusculas de minúsculas e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] computador configurado para ser o domínio deve ter esse usuário `alias@YYYY.CORP.CONTOSO.COM` adicionado para logon. Agora, você pode usar conexões confiáveis (**Trusted_Connection = YES** em uma cadeia de caracteres de conexão, **bcp -T**, ou **sqlcmd -E**).  
  
A hora no computador Linux ou macOS e a hora no Centro de distribuição de chaves (KDC) do Kerberos devem ser próximas. Certifique-se de que a hora do sistema está definida corretamente, por exemplo, usando o protocolo NTP (Network Time).  

Se a autenticação Kerberos falhar, o driver ODBC no Linux ou macOS não usar a autenticação NTLM.  

Para obter mais informações sobre autenticação de computadores Linux ou macOS com o Active Directory, consulte [autenticar clientes Linux com Active Directory](http://technet.microsoft.com/magazine/2008.12.linux.aspx#id0060048) e [práticas recomendadas para integrar OS X com o Active Directory](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf). Para obter mais informações sobre como configurar o Kerberos, consulte o [MIT Kerberos documentação](https://web.mit.edu/kerberos/krb5-1.12/doc/index.html).

## <a name="see-also"></a>Consulte também  
[Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md)

[Notas de versão](../../../connect/odbc/linux-mac/release-notes.md)

[Usando o Active Directory do Azure](../../../connect/odbc/using-azure-active-directory.md)
