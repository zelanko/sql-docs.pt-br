---
title: Perguntas frequentes sobre o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/29/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cbc0e397-ecf2-4494-87b2-a492609bceae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1055b9b0422073d7b9875c748dcfe889af053dc2
ms.sourcegitcommit: 4b2c9d648b7a7bdf9c3052ebfeef182e2f9d66af
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/04/2020
ms.locfileid: "77004630"
---
# <a name="frequently-asked-questions-faq-for-jdbc-driver"></a>Perguntas frequentes sobre o JDBC Driver

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Esta página fornece respostas para as perguntas frequentes sobre o Microsoft JDBC Driver para SQL Server.

## <a name="frequently-asked-questions"></a>Perguntas frequentes

**Como posso ajudar a melhorar o JDBC Driver?**  
O JDBC Driver é um software livre, e o código-fonte pode ser encontrado no [GitHub](https://github.com/microsoft/mssql-jdbc). Você pode ajudar a melhorar o driver comunicando problemas e contribuindo com a base de código.

**Quais versões do SQL Server e do Java são compatíveis com o driver?**  
Confira mais detalhes na página [Matriz de suporte do Microsoft JDBC Driver para SQL Server](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md).

**Qual é a diferença entre os pacotes do JDBC Driver disponíveis no Centro de Download da Microsoft e o JDBC Driver disponível no GitHub?**  
Os arquivos do JDBC Driver que estão disponíveis no repositório do GitHub para o Microsoft JDBC Driver são a essência do JDBC Driver e estão sob a licença de software livre, listada no repositório. Os pacotes de driver disponíveis no Centro de Download da Microsoft incluem bibliotecas adicionais para a autenticação integrada no Windows e para habilitar transações XA com o JDBC Driver. Essas bibliotecas adicionais estão sob a licença incluída com o pacote que pode ser baixado.

**O que devo saber ao atualizar meu driver?**  
O Microsoft JDBC Driver 8.2 é compatível com as especificações JDBC 4.2 e 4.3 (parcialmente) e inclui três bibliotecas de classe JAR no pacote de instalação da seguinte maneira:

| JAR                        | Especificação do JDBC            | Versão do JDK |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-8.2.0.jre13.jar | JDBC 4.3 (parcialmente) e 4.2 | JDK 13.0    |
| mssql-jdbc-8.2.0.jre11.jar | JDBC 4.3 (parcialmente) e 4.2 | JDK 11.0    |
| mssql-jdbc-8.2.0.jre8.jar  | JDBC 4.2                      | JDK 8.0     |
| &nbsp;                     | &nbsp;                        | &nbsp;      |

O Microsoft JDBC Driver 7.4 dá suporte às especificações JDBC 4.2 e 4.3 (parcialmente) e inclui três bibliotecas de classes JAR no pacote de instalação, da seguinte forma:

| JAR                        | Especificação do JDBC            | Versão do JDK |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.4.1.jre12.jar | JDBC 4.3 (parcialmente) e 4.2 | JDK 12.0    |
| mssql-jdbc-7.4.1.jre11.jar | JDBC 4.3 (parcialmente) e 4.2 | JDK 11.0    |
| mssql-jdbc-7.4.1.jre8.jar  | JDBC 4.2                      | JDK 8.0     |
| &nbsp;                     | &nbsp;                        | &nbsp;      |

O Microsoft JDBC Driver 7.2 dá suporte às especificações JDBC 4.2 e JDBC 4.3 (parcialmente) e inclui duas bibliotecas de classes JAR no pacote de instalação, da seguinte forma:

| JAR                        | Especificação do JDBC            | Versão do JDK |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.2.2.jre11.jar | JDBC 4.3 (parcialmente) e 4.2 | JDK 11.0    |
| mssql-jdbc-7.2.2.jre8.jar  | JDBC 4.2                      | JDK 8.0     |
| &nbsp;                     | &nbsp;                        | &nbsp;      |

O Microsoft JDBC Driver 7.0 dá suporte às especificações JDBC 4.2 e JDBC 4.3 (parcialmente) e inclui duas bibliotecas de classes JAR no pacote de instalação, da seguinte forma:

| JAR                        | Especificação do JDBC            | Versão do JDK |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.0.0.jre10.jar | JDBC 4.3 (parcialmente) e 4.2 | JDK 10.0    |
| mssql-jdbc-7.0.0.jre8.jar  | JDBC 4.2                      | JDK 8.0     |
| &nbsp;                     | &nbsp;                        | &nbsp;      |

O Microsoft JDBC Driver 6.4 dá suporte às especificações JDBC 4.1, 4.2 e 4.3 (parcialmente) e inclui três bibliotecas de classes JAR no pacote de instalação, da seguinte forma:

| JAR                       | Especificação do JDBC                 | Versão do JDK |
| ------------------------- | ---------------------------------- | ----------- |
| mssql-jdbc-6.4.0.jre9.jar | JDBC 4.3 (parcialmente), 4.2 e 4.1 | JDK 9.0     |
| mssql-jdbc-6.4.0.jre8.jar | JDBC 4.2 e 4.1                  | JDK 8.0     |
| mssql-jdbc-6.4.0.jre7.jar | JDBC 4.1                           | JDK 7.0     |
| &nbsp;                    | &nbsp;                             | &nbsp;      |

O Microsoft JDBC Driver 6.2 dá suporte às especificações JDBC 4.0, 4.1 e 4.2 e inclui duas bibliotecas de classes JAR no pacote de instalação, da seguinte forma:

| JAR                       | Especificação do JDBC     | Versão do JDK |
| ------------------------- | ---------------------- | ----------- |
| mssql-jdbc-6.2.2.jre8.jar | JDBC 4.2, 4.1 e 4.0 | JDK 8.0     |
| mssql-jdbc-6.2.2.jre7.jar | JDBC 4.1 e 4.0       | JDK 7.0     |
| &nbsp;                    | &nbsp;                 | &nbsp;      |

O Microsoft JDBC Driver 6.0 e 4.2 para SQL Server dão suporte às especificações JDBC 4.0, 4.1 e 4.2 e incluem duas bibliotecas de classes JAR no pacote de instalação, da seguinte forma:

| JAR           | Especificação do JDBC     | Versão do JDK |
| ------------- | ---------------------- | ----------- |
| sqljdbc42.jar | JDBC 4.2, 4.1 e 4.0 | JDK 8.0     |
| sqljdbc41.jar | JDBC 4.1 e 4.0       | JDK 7.0     |
| &nbsp;        | &nbsp;                 | &nbsp;      |

O Microsoft JDBC Driver 4.1 para SQL Server dá suporte à especificação JDBC 4.0 e inclui uma biblioteca de classes JAR no pacote de instalação, da seguinte forma:

| JAR           | Especificação do JDBC | Versão do JDK     |
| ------------- | ------------------ | --------------- |
| sqljdbc41.jar | JDBC 4.0           | JDK 7.0 e 6.0 |
| &nbsp;        | &nbsp;             | &nbsp;      |

**É necessário fazer alterações de código no meu aplicativo para usar o driver mais recente com a minha versão atual do SQL Server?**  
Normalmente, o driver é criado para incluir compatibilidade com versões anteriores para que você não precise alterar seus aplicativos atuais após atualizar o driver. Se uma nova versão do driver apresentar uma alteração significativa, a seção [Notas sobre a versão do JDBC Driver](../../connect/jdbc/release-notes-for-the-jdbc-driver.md) fornecerá detalhes claros sobre a alteração e o impacto dela nos aplicativos existentes. Além disso, você pode revisar as notas de versão incluídas com o driver para obter uma lista de erros corrigidos e problemas conhecidos nessa versão.

**Quanto custa o driver?**  
O Microsoft JDBC Driver para SQL Server está disponível sem custo adicional.

**Posso redistribuir o driver?**  
Os JDBC Drivers 6.0, 6.2, 6.4 e 7.0 são redistribuíveis. Consulte a cláusula sobre “Código Distribuível” nos contratos de licença.

**Posso usar o driver para acessar o Microsoft SQL Server de um computador Linux?**  
Sim! Você pode usar o driver para acessar o SQL Server no Linux, Unix e outras plataformas não Windows. Para saber mais, confira a [matriz de suporte do Microsoft JDBC Driver para SQL Server](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md).

**O driver dá suporte à criptografia do protocolo SSL?**  
A partir da versão 1.2, o driver dá suporte à criptografia Secure Sockets Layer (SSL). Confira mais informações em [Como usar a criptografia SSL](../../connect/jdbc/using-ssl-encryption.md).

**Quais tipos de autenticação são compatíveis com o Microsoft JDBC Driver para SQL Server?**  
A tabela a seguir lista as opções de autenticação disponíveis. Uma autenticação Kerberos em Java puro está disponível a partir da versão 4.0 do driver.

| Plataforma    | Autenticação                        |
| ----------- | ------------------------------------- |
| Não Windows | Kerberos Java puro                    |
| Não Windows | SQL Server                            |
| Não Windows | Autenticação do Azure Active Directory |
| Windows     | Kerberos Java puro                    |
| Windows     | SQL Server                            |
| Windows     | Kerberos com backup NTLM             |
| Windows     | NTLM                                  |
| Windows     | Autenticação do Azure Active Directory |
| &nbsp;      | &nbsp;                                |

**O driver dá suporte a endereços IP versão 6 (IPv6)?**  
Sim. O driver dá suporte ao uso de endereços IPv6. Use a coleção de propriedades de conexão e a propriedade de cadeia de conexão serverName. Confira mais informações em [Como construir a URL de conexão](../../connect/jdbc/building-the-connection-url.md).

**O que é o buffer adaptável?**  
O buffer adaptável foi introduzido a partir do JDBC Driver versão 1.2 para Microsoft SQL Server 2005. Ele é criado para recuperar qualquer tipo de dados de valor grande sem a sobrecarga de cursores de servidor. O recurso de buffer adaptável do Microsoft SQL Server JDBC Driver oferece uma propriedade de cadeia de caracteres de conexão, responseBuffering, que pode ser definida como "adaptive" ou "full". Na versão 1.2, o modo de buffer é "cheio" por padrão e o aplicativo deve configurar o modo de buffer adaptável explicitamente. A partir do driver JDBC versão 2.0, o comportamento padrão do driver é "adaptive". Além disso, o aplicativo não precisa solicitar o comportamento adaptável explicitamente para obter o comportamento de buffer adaptável. Para obter mais informações, confira [Usando um buffer adaptável](../../connect/jdbc/using-adaptive-buffering.md) e o blog [What is adaptive response buffering and why should I use it?](https://go.microsoft.com/fwlink/?LinkId=111575) (O que é o buffer de resposta adaptável e por que devo usá-lo?).

**O driver dá suporte ao pool de conexões?**  
O driver dá suporte ao pool de conexões da Plataforma Java, Edição Enterprise 5 (Java EE 5). O driver JDBC implementa as interfaces do JDBC 3.0 necessárias para permitir que o driver participe de qualquer implementação de pool de conexões disponibilizada pelos fornecedores de servidores de aplicativos em middleware. O driver participa das conexões em pool nesses ambientes. Confira mais informações em [Como usar o pool de conexões](../../connect/jdbc/using-connection-pooling.md). O driver não fornece sua própria implementação do pool. Em vez disso, ele utiliza servidores de aplicativos Java de terceiros.

**O driver tem suporte disponível?**  
Há diversas opções de suporte disponíveis. Você pode postar sua dúvida ou problema no [repositório do GitHub](https://github.com/microsoft/mssql-jdbc) que é monitorado pela Microsoft. Os [fóruns](https://go.microsoft.com/fwlink/?LinkID=246673) são monitorados pela Microsoft, MVPs e pela comunidade. Entre em contato com o Suporte ao Cliente Microsoft. A equipe de desenvolvimento pode pedir que você reproduza o problema fora de qualquer servidor de aplicativos de terceiros. Se o problema não puder ser reproduzido fora do ambiente de hospedagem do contêiner Java, você precisará acionar os terceiros envolvidos para que a equipe possa continuar a ajudá-lo. A equipe também poderá pedir que você reproduza o problema em um sistema operacional como o Windows para que seja possível oferecer o melhor suporte.

**O driver é certificado para uso com qualquer servidor de aplicativos de terceiros?**  
O driver foi testado com todos os principais servidores de aplicativos, inclusive IBM WebSphere e SAP NetWeaver.

**Como habilitar o rastreamento?**  
O driver dá suporte ao uso de rastreamento (ou registro em log) para ajudar a resolver problemas com o driver JDBC usado em seu aplicativo. Para habilitar o uso de rastreamento do JAR do lado do cliente, o driver JDBC usa as APIs de registro em log em java.util.logging. Para obter mais informações, veja [Rastreamento de operação do driver](../../connect/jdbc/tracing-driver-operation.md). Para o rastreamento XA do lado do servidor, consulte [Rastreamento do acesso a dados no SQL Server](https://go.microsoft.com/fwlink/?LinkId=248705).

**Onde posso baixar as versões mais antigas do driver, como o driver SQL Server 2000 JDBC driver, o driver 2005 e o driver 1.0, 1.1 ou 1.2?**  
Essas versões de driver não estão disponíveis para download, pois não têm mais suporte. Estamos aperfeiçoando continuamente o suporte à conectividade com Java. Portanto, é altamente recomendável que você trabalhe com a versão mais recente do Microsoft JDBC driver.

**Estou usando o JRE 1.4. Qual driver é compatível com o JRE 1.4?**  
Os clientes que estão usando produtos SAP e precisam do suporte ao JRE 1.4 podem entrar em contato com o [SAPService Marketplace](https://service.sap.com/) para obter o Microsoft JDBC Driver 1.2.

**O driver pode se comunicar usando algoritmos validados pelos FIPS?**  
O Microsoft JDBC Driver não contém nenhum algoritmo de criptografia. Se o cliente utilizar sistema operacional, aplicativos e algoritmos JVM considerados aceitáveis de acordo com os Federal Information Processing Standards (FIPS) e configurar o driver para usar esses algoritmos, o driver usa somente os algoritmos designados para comunicação.

## <a name="see-also"></a>Confira também

[Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)
