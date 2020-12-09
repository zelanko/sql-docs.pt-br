---
title: Usando a autenticação NTLM para se conectar ao SQL Server
description: Saiba como estabelecer uma conexão de Banco de Dados SQL usando a autenticação NTLM com o driver JDBC.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: lilgreenbird
ms.author: v-susanh
manager: kenvh
ms.openlocfilehash: 31510c4fbe4291168753809c227650951592e1e6
ms.sourcegitcommit: 644223c40af7168f9d618526e9f4cd24e115d1db
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/30/2020
ms.locfileid: "96328036"
---
# <a name="using-ntlm-authentication-to-connect-to-sql-server"></a>Usando a autenticação NTLM para se conectar ao SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] permite que um aplicativo use a propriedade de conexão **authenticationScheme** para indicar que ele deseja se conectar a um banco de dados usando a Autenticação NTLM v2. 

As seguintes propriedades também são usadas para autenticação NTLM:

- **domínio = domainName** (opcional)
- **usuário = userName**
- **senha = password**
- **integratedSecurity = true**

Além do **domínio**, as outras propriedades são obrigatórias, o driver gerará um erro se alguma delas estiver ausente quando a propriedade authenticationScheme do **NTLM** for usada. 

Para obter mais informações sobre as propriedades de conexão, confira [Configuração das propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md). Para obter mais informações sobre o protocolo de autenticação NTLM da Microsoft, confira [Microsoft NTLM](/windows/desktop/SecAuthN/microsoft-ntlm).

## <a name="remarks"></a>Comentários

Confira [Segurança de rede: Nível de autenticação do LAN Manager](/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level) para encontrar a descrição das configurações do SQL Server, que controlam o comportamento da autenticação NTLM. 

## <a name="logging"></a>Registro em log

Um novo agente foi adicionado para dar suporte à autenticação NTLM: com.microsoft.sqlserver.jdbc.internals.NTLMAuthentication. Para obter mais informações, veja [Rastreamento de operação do driver](../../connect/jdbc/tracing-driver-operation.md).

## <a name="datasource"></a>DataSource

Ao usar uma fonte de fontes para criar conexões, as propriedades NTLM podem ser definidas de forma programática usando **setAuthenticationScheme**, **setdomain** e (opcionalmente) **setServerSpn**.

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(1433); // change if necessary
ds.setIntegratedSecurity(true);
ds.setAuthenticationScheme("NTLM");
ds.setDomain("<domainName>");
ds.setUser("<userName>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setServerSpn("<serverSpn");

try (Connection c = ds.getConnection(); Statement s = c.createStatement();
        ResultSet rs = s.executeQuery("select auth_scheme from sys.dm_exec_connections where session_id=@@spid")) {
    while (rs.next()) {
        System.out.println("Authentication Scheme: " + rs.getString(1));
    }
}
```

## <a name="service-principal-names"></a>Nomes de entidades de serviço

Um SPN (nome da entidade de serviço) é o nome pelo qual um cliente identifica exclusivamente uma instância de um serviço.

Você pode especificar o SPN usando a propriedade de conexão **serverSpn** ou deixar que o driver o crie para você (o padrão). Essa propriedade está no formato: "MSSQLSvc/fqdn:port\@REALM", em que fqdn é o nome de domínio totalmente qualificado, port é o número da porta e REALM é o realm do SQL Server em letras maiúsculas. A parte do realm dessa propriedade é opcional, pois o realm padrão é o mesmo que o do servidor.

Por exemplo, o SPN pode ser: "MSSQLSvc/some-server.zzz.corp.contoso.com:1433"

Para obter mais informações sobre SPNs (nomes de entidade de serviço), consulte:

- [Suporte a SPN (Nome da entidade de serviço) em conexões com o cliente](../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)

> [!NOTE]  
> O atributo de conexão serverSpn é compatível somente com os Microsoft JDBC Drivers 4.2 e superiores.

> Antes da versão 6.2 do driver JDBC, você precisa definir explicitamente o **serverSpn**. Começando com a versão 6.2, o driver poderia criar o **serverSpn** por padrão, embora seja possível usar o **serverSpn** explicitamente também.

## <a name="security-risks"></a>Riscos à segurança

O protocolo NTLM é um protocolo de autenticação antigo com várias vulnerabilidades, que representam um risco de segurança. Ele é baseado em um esquema criptográfico relativamente fraco e é vulnerável a vários ataques. Ele é substituído pelo Kerberos, que é muito mais seguro e recomendado. A autenticação NTLM deve ser usada apenas em um ambiente confiável seguro ou quando o Kerberos não pode ser usado.

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] é compatível apenas com NTLM v2, que tem alguns aprimoramentos de segurança em relação ao protocolo v1 original. Também é recomendado habilitar a Proteção Estendida ou usar a Criptografia SSL para aumentar a segurança. 

Para obter mais informações sobre como habilitar a Proteção Estendida, confira:

- [Conectar-se ao mecanismo de banco de dados usando proteção estendida](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)

Para obter mais informações sobre a conexão com a Criptografia SSL, confira:

- [Conectando-se com criptografia SSL](../../connect/jdbc/connecting-with-ssl-encryption.md)

> [!NOTE]
> Para a versão 7,4, não **há** suporte para a habilitação da proteção estendida e da criptografia.

## <a name="see-also"></a>Confira também

[Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
