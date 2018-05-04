---
title: Perguntas frequentes (FAQ para o Driver JDBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cbc0e397-ecf2-4494-87b2-a492609bceae
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 282f71f49eba5ccece8bc9d50ef690fd0af3cb8c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="frequently-asked-questions-faq-for-jdbc-driver"></a>Perguntas frequentes (FAQ para o Driver JDBC)
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Este artigo fornece respostas para as perguntas frequentes sobre o Microsoft JDBC Driver para SQL Server.  
  
## <a name="frequently-asked-questions"></a>Perguntas frequentes  
**Como ajudar a melhorar o Driver JDBC?**  
O Driver JDBC é o código-fonte aberto e o código-fonte pode ser encontrado em [GitHub](https://github.com/microsoft/mssql-jdbc). Você pode ajudar a melhorar o driver, problemas de arquivamento e que contribuem para a base de código.

**Quais versões do SQL Server e Java driver suporta?**  
 Consulte o [Microsoft JDBC Driver para SQL Server Support Matrix](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md) página para obter detalhes.  
  
 **O que devo saber ao atualizar meu driver?**  
 O Microsoft JDBC Driver 6.4 oferece suporte a JDBC 4.1, 4.2, 4.3 (parcialmente), as especificações e inclui três bibliotecas de classes JAR no pacote de instalação da seguinte maneira:  
  
|JAR|Especificação do JDBC|Versão do JDK|  
|-|-|-|  
|mssql-jdbc-6.4.0.jre9.jar|JDBC 4.1 e 4.3 4.2 (parcialmente)|JDK 9.0|  
|mssql-jdbc-6.4.0.jre8.jar|JDBC 4.2 e 4.1|JDK 8.0|  
|mssql-jdbc-6.4.0.jre7.jar|JDBC 4.1|JDK 7.0|  

 O Microsoft JDBC Driver 6.2 oferece suporte às especificações JDBC 4.0, 4.1 e 4.2 e inclui duas bibliotecas de classes JAR no pacote de instalação da seguinte maneira:  
  
|JAR|Especificação do JDBC|Versão do JDK|  
|-|-|-|  
|mssql-jdbc-6.2.1.jre8.jar|JDBC 4.2, 4.1 e 4.0|JDK 8.0|  
|mssql-jdbc-6.2.1.jre7.jar|JDBC 4.1 e 4.0|JDK 7.0|  
 
 O Microsoft JDBC Drivers 6.0 e 4.2 para SQL Server dá suporte às especificações JDBC 4.0, 4.1 e 4.2 e inclui duas bibliotecas de classes JAR no pacote de instalação da seguinte maneira:  
  
|JAR|Especificação do JDBC|Versão do JDK|   
|-|-|-|  
|sqljdbc42.jar|JDBC 4.2, 4.1 e 4.0|JDK 8.0|  
|sqljdbc41.jar|JDBC 4.1 e 4.0|JDK 7.0|  
  
 O Microsoft JDBC Driver 4.1 para SQL Server oferece suporte à especificação do JDBC 4.0 e inclui uma biblioteca de classes JAR no pacote de instalação da seguinte maneira:  
  
|JAR|Especificação do JDBC|Versão do JDK|    
|-|-|-|  
|sqljdbc41.jar|JDBC 4.0|JDK 7.0 e 6.0|
  
 **É necessário fazer alterações de código no meu aplicativo para usar o driver mais recente com minha versão existente do SQL Server?**  
 Em geral, o driver é projetado para ser compatível com versões anteriores, para que você não precisa alterar seus aplicativos existentes ao atualizar o driver. Se uma nova versão do driver apresenta uma alteração significativa, o [notas de versão do Driver JDBC](../../connect/jdbc/release-notes-for-the-jdbc-driver.md) seção fornece detalhes claros sobre a alteração e o impacto nos aplicativos existentes. Além disso, você pode revisar as notas de versão incluídas com o driver para obter uma lista de erros corrigidos e problemas conhecidos nessa versão.  
  
 **Quanto custa o driver?**  
 O Microsoft JDBC Driver para SQL Server está disponível sem custo adicional.  
  
 **Posso redistribuir o driver?** Os Drivers JDBC 4.1, 4.2, 6.0, 6.2 e 6.4 são redistribuíveis. Examine a cláusula "Código distribuível" em contratos de licença. 
   
 **Pode usar o driver para acessar o Microsoft SQL Server de um computador Linux?** Sim! Você pode usar o driver para acessar o SQL Server no Linux, Unix e outras plataformas não Windows. Consulte [Microsoft JDBC Driver para SQL Server Support Matrix](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md) para obter mais detalhes.  
  
 **O driver dá suporte à criptografia Secure Sockets Layer (SSL)?** A partir da versão 1.2, o driver dá suporte à criptografia Secure Sockets Layer (SSL). Para obter mais informações, consulte [usando a criptografia SSL](../../connect/jdbc/using-ssl-encryption.md).  
  
 **Os tipos de autenticação são compatíveis com o Microsoft JDBC Driver para SQL Server?**  
 A tabela a seguir lista as opções de autenticação disponíveis. Observe que a autenticação Kerberos em Java puro está disponível a partir da versão 4.0 do driver.  
  
|||  
|-|-|  
|Plataforma|Autenticação|  
|Não Windows|Kerberos Java puro|  
|Não Windows|SQL Server|  
|Não Windows|Autenticação do Active Directory do Azure|
|Windows|Kerberos Java puro|  
|Windows|SQL Server|
|Windows|Kerberos com backup NTLM|  
|Windows|NTLM|  
|Windows|Autenticação do Active Directory do Azure|  
  
**O driver suporta o protocolo de Internet versão 6 (IPv6) endereços?**  
 O driver JDBC dá suporte ao uso de endereços IPv6 com a coleção de propriedades de conexão e com a propriedade de cadeia de conexão serverName. Para obter mais informações, consulte [criar a URL de Conexão](../../connect/jdbc/building-the-connection-url.md).  
  
**O que é o buffer adaptável?**  
 O buffer adaptável foi introduzido a partir do Microsoft SQL Server 2005 JDBC Driver versão 1.2 e foi projetado para recuperar qualquer tipo de dados com valores grandes sem a sobrecarga de cursores de servidor. O recurso de buffer adaptável do Microsoft SQL Server JDBC Driver oferece uma propriedade de cadeia de caracteres de conexão, responseBuffering, que pode ser definida como "adaptive" ou "full". A partir do driver JDBC versão 2.0, o comportamento padrão do driver é "adaptive". Em outras palavras, para obter o comportamento de buffer adaptável, o aplicativo não precisa solicitar o comportamento adaptável explicitamente. No entanto, na versão 1.2 o modo padrão de buffer "full" e o aplicativo precisava solicitar explicitamente o modo de buffer adaptável. Para obter mais informações, consulte [usando buffer adaptável](../../connect/jdbc/using-adaptive-buffering.md) tópico e o blog. [O que é Adaptive Response buffering e por que devo usar?](http://go.microsoft.com/fwlink/?LinkId=111575)  
  
**É o pool de conexão do driver suporte?**  
 O driver dá suporte ao pool de conexões da Plataforma Java, Edição Enterprise 5 (Java EE 5). O driver JDBC implementa as interfaces do JDBC 3.0 necessárias para permitir que o driver participe de qualquer implementação de pool de conexões disponibilizada pelos fornecedores de servidores de aplicativos em middleware. O driver participa das conexões em pool nesses ambientes. Para obter mais informações, consulte [Pooling de Conexão usando](../../connect/jdbc/using-connection-pooling.md). O driver não fornece sua própria implementação do pool. Em vez disso, ele utiliza servidores de aplicativos Java de terceiros.  
  
**O suporte está disponível para o driver?**  
 Há diversas opções de suporte disponíveis. Você pode postar a pergunta ou emitir para nosso [repositório GitHub](https://github.com/microsoft/mssql-jdbc) que é monitorado pela Microsoft. [Fóruns](http://go.microsoft.com/fwlink/?LinkID=246673) monitorados pela Microsoft, MVPs e pela comunidade. Entre em contato com o Suporte ao Cliente Microsoft. A equipe de desenvolvimento pode solicitar que você reproduza o problema fora de qualquer servidor de aplicativos de terceiros. Se o problema não pode ser reproduzido fora do ambiente de contêiner Java hospedagem, você precisará envolver o terceiros envolvidos para que a equipe possa continuar para ajudá-lo. A equipe também pode solicitar que você reproduza o problema em um sistema operacional como o Windows para que o problema pode ser melhor suporte.  
  
**O driver é certificado para uso com qualquer servidor de aplicativos de terceiros?**
O driver foi testado com todos os principais servidores de aplicativos, inclusive IBM WebSphere e SAP NetWeaver.  
  
**Como habilitar o rastreamento?**  
 O driver dá suporte ao uso de rastreamento (ou registro em log) para ajudar a resolver problemas com o driver JDBC usado em seu aplicativo. Para habilitar o uso de rastreamento do JAR do lado do cliente, o driver JDBC usa as APIs de registro em log em java.util.logging. Para obter mais informações, consulte [a operação de rastreamento do Driver](../../connect/jdbc/tracing-driver-operation.md). Para o rastreamento XA do lado do servidor, consulte [Rastreamento do acesso a dados no SQL Server](http://go.microsoft.com/fwlink/?LinkId=248705).  
  
**Onde posso baixar as versões mais antigas do driver, como o driver JDBC do SQL Server 2000, 2005 driver, 1.0, 1.1 ou 1.2 do driver?**  
 Essas versões de driver não estão disponíveis para download, pois não têm mais suporte. Estamos aperfeiçoando continuamente o suporte à conectividade de Java. Como tal, é altamente recomendável que trabalhar com a versão mais recente do Microsoft JDBC driver.  
  
**Estou usando o JRE 1.4. Qual driver é compatível com o JRE 1.4?**  
 Os clientes que estão usando produtos SAP e precisam do suporte ao JRE 1.4 podem entrar em contato com o [SAPService Marketplace](http://service.sap.com/) para obter o Microsoft JDBC Driver 1.2.  
  
**Pode o driver se comunicar usando algoritmos validados pelos FIPS?**  
 O Microsoft JDBC Driver não contém nenhum algoritmo de criptografia. Se o cliente utiliza o sistema operacional, aplicativo e algoritmos JVM considerados aceitáveis pelo FIPS Federal Information Processing Standards () e configura o driver para usar esses algoritmos, em seguida, o driver usa somente os algoritmos designados para comunicação.  
  
 ## <a name="see-also"></a>Consulte também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
