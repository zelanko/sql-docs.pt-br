---
title: Usando a autenticação NTLM para se conectar ao SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2019
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
ms.openlocfilehash: 11fe35e1dc90e32cac460b61fe8a6078c817b0ca
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68894098"
---
# <a name="using-ntlm-authentication-to-connect-to-sql-server"></a>Usando a autenticação NTLM para se conectar ao SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] permite que um aplicativo use a propriedade de conexão **AuthenticationScheme** para indicar que deseja se conectar a um banco de dados usando a autenticação NTLM v2. 

As propriedades a seguir também são usadas para autenticação NTLM:

- **domínio = nome_do_domínio** adicional
- **user = nome de usuário**
- **senha = password**
- **integratedSecurity = true**

Além do **domínio**, as outras propriedades são obrigatórias, o driver gerará um erro se algum estiver ausente quando a propriedade **NTLM** AuthenticationScheme for usada. 

Para obter mais informações sobre propriedades de conexão, consulte [definindo as propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md). Para obter mais informações sobre o protocolo de autenticação NTLM da Microsoft, consulte [Microsoft NTLM](https://docs.microsoft.com/windows/desktop/SecAuthN/microsoft-ntlm).

## <a name="remarks"></a>Remarks

Consulte [segurança de rede: nível de autenticação do LAN Manager](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level) para obter a descrição das configurações do SQL Server, que controlam o comportamento da autenticação NTLM. 

## <a name="logging"></a>Log

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

## <a name="service-principal-names"></a>Nomes de Entidade de Serviço

Um SPN (nome da entidade de serviço) é o nome pelo qual um cliente identifica exclusivamente uma instância de um serviço.

Você pode especificar o SPN usando a propriedade de conexão **serverSpn** ou deixar que o driver o crie para você (o padrão). Essa propriedade está no formato: "MSSQLSvc/fqdn:port\@REALM", em que fqdn é o nome de domínio totalmente qualificado, port é o número da porta e REALM é o realm do SQL Server em letras maiúsculas. A parte do Realm dessa propriedade é opcional, pois o realm padrão é o mesmo que o realm do servidor.

Por exemplo, seu SPN pode ser semelhante a: "MSSQLSvc/some-Server. zzz. Corp. contoso. com: 1433"

Para obter mais informações sobre SPNs (nomes de entidade de serviço), consulte:

- [Suporte a SPN (Nome da entidade de serviço) em conexões com o cliente](https://docs.microsoft.com/sql/relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections?view=sql-server-2017)

> [!NOTE]  
> O atributo de conexão serverSpn é compatível somente com os Microsoft JDBC Drivers 4.2 e superiores.

> Antes da versão 6,2 do driver JDBC, você precisaria definir explicitamente o **serverSpn**. A partir da versão 6,2, o driver poderá criar o **serverSpn** por padrão, embora também seja possível usar o **serverSpn** explicitamente.

## <a name="security-risks"></a>Riscos à segurança

O protocolo NTLM é um protocolo de autenticação antigo com várias vulnerabilidades, que representam um risco de segurança. Ele é baseado em um esquema criptográfico relativamente fraco e é vulnerável a vários ataques. Ele é substituído pelo Kerberos, que é muito mais seguro e recomendado. A autenticação NTLM só deve ser usada em um ambiente confiável seguro ou quando o Kerberos não pode ser usado.

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] só dá suporte a NTLM v2, que tem algumas melhorias de segurança em relação ao protocolo v1 original. O It'ss também é recomendado para habilitar a proteção estendida ou usar a criptografia SSL para aumentar a segurança. 

Para obter mais informações sobre como habilitar a proteção estendida e o, consulte:

- [Conectar-se ao mecanismo de banco de dados usando proteção estendida](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)

Para obter mais informações sobre como se conectar com a criptografia SSL, consulte:

- [Conectando-se com criptografia SSL](../../connect/jdbc/connecting-with-ssl-encryption.md)

> [!NOTE]
> Para a versão 7,4, não **há** suporte para a habilitação da proteção estendida e da criptografia.

## <a name="see-also"></a>Consulte Também

[Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
