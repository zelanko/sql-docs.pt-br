---
title: Perguntas frequentes (FAQ para o Driver JDBC) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cbc0e397-ecf2-4494-87b2-a492609bceae
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 508f8526ed13af3f7f92aa500b182e077f5bb23d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="frequently-asked-questions-faq-for-jdbc-driver"></a>Perguntas frequentes (FAQ para o Driver JDBC)
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Este artigo fornece respostas para as perguntas frequentes sobre o Microsoft JDBC Driver para SQL Server.  
  
## <a name="frequently-asked-questions"></a>Perguntas frequentes  
**Como ajudar a melhorar o Driver JDBC?**  
O Driver JDBC é o código-fonte aberto e o código-fonte pode ser encontrado em [GitHub](https://github.com/microsoft/mssql-jdbc). Você pode ajudar a melhorar o driver, problemas de arquivamento e que contribuem para a base de código.

**Quais versões do SQL Server e Java o driver dá suporte?**  
 Consulte o [Microsoft JDBC Driver para SQL Server Support Matrix](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md) página para obter detalhes.  
  
 **O que devo saber ao atualizar meu driver?**  
 O Microsoft JDBC Driver 6.2 oferece suporte às especificações JDBC 4.0, 4.1 e 4.2 e inclui duas bibliotecas de classes JAR no pacote de instalação da seguinte maneira:  
  
|JAR|Especificação do JDBC|Versão do JDK|  
|-|-|-|  
|MSSQL-jdbc-6.2.1.jre8.jar|JDBC 4.2, 4.1 e 4.0|JDK 8.0|  
|MSSQL-jdbc-6.2.1.jre7.jar|JDBC 4.1 e 4.0|JDK 7.0|  
 
 O Microsoft JDBC Drivers 6.0 e 4.2 para SQL Server dá suporte às especificações JDBC 4.0, 4.1 e 4.2 e inclui duas bibliotecas de classes JAR no pacote de instalação da seguinte maneira:  
  
|JAR|Especificação do JDBC|Versão do JDK|   
|-|-|-|  
|sqljdbc42.jar|JDBC 4.2, 4.1 e 4.0|JDK 8.0|  
|sqljdbc41.jar|JDBC 4.1 e 4.0|JDK 7.0|  
  
 O Microsoft JDBC Driver 4.1 para SQL Server oferece suporte à especificação do JDBC 4.0 e inclui uma biblioteca de classes JAR no pacote de instalação da seguinte maneira:  
  
|JAR|Especificação do JDBC|Versão do JDK|    
|-|-|-|  
|sqljdbc41.jar|JDBC 4.0|JDK 7.0 e 6.0|
  
 O Microsoft JDBC Driver 4.0 para SQL Server dá suporte às especificações JDBC 3.0 e JDBC 4.0 e inclui duas bibliotecas de classes JAR no pacote de instalação para cada especificação: sqljdbc.jar e sqljdbc4.jar, respectivamente.  
  
|JAR|Especificação do JDBC|Versão do JDK|   
|-|-|-|  
|sqljdbc4.jar|JDBC 4.0|JDK 6.0 e 5.0|  
|sqljdbc.jar|JDBC 3.0|JDK 6.0 e 5.0|  
  
 **É necessário fazer alterações de código no meu aplicativo para usar o driver mais recente com minha versão existente do SQL Server?**  
 Normalmente, criamos o driver incluindo compatibilidade com versões anteriores para que você não precise alterar seus aplicativos atuais após atualizar o driver. Se uma nova versão do driver apresenta uma alteração significativa, o [notas de versão do Driver JDBC](../../connect/jdbc/release-notes-for-the-jdbc-driver.md) seção fornecerá detalhes claros sobre a alteração e o impacto nos aplicativos existentes. Além disso, você pode revisar as notas de versão incluídas com o driver para obter uma lista de erros corrigidos e problemas conhecidos nessa versão.  
  
 **Quanto custa o driver?**  
 O Microsoft JDBC Driver para SQL Server está disponível sem custo adicional.  
  
 **Posso redistribuir o driver?** Os Drivers JDBC 4.1, 4.2, 6.0 e 6.2 são redistribuíveis. Analise a cláusula "Código distribuível" nos contratos de licença.
 
 O JDBC Driver 4.0 pode ser redistribuído sob uma licença de redistribuição separada que exige registro. Para registrar ou para obter mais informações, consulte nosso [redistribuir o Microsoft JDBC Driver](../../connect/jdbc/redistributing-the-microsoft-jdbc-driver.md). 
 
   
 **Pode usar o driver para acessar o Microsoft SQL Server de um computador Linux?** Sim! Você pode usar o driver para acessar o SQL Server no Linux, Unix e outras plataformas não Windows. Consulte nossa [Microsoft JDBC Driver para SQL Server Support Matrix](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md) para obter mais detalhes.  
  
 **O driver dá suporte à criptografia Secure Sockets Layer (SSL)?** A partir da versão 1.2, o driver dá suporte à criptografia Secure Sockets Layer (SSL). Para obter mais informações, consulte [usando a criptografia SSL](../../connect/jdbc/using-ssl-encryption.md).  
  
 **Os tipos de autenticação são compatíveis com o Microsoft JDBC Driver para SQL Server?**  
 A tabela a seguir lista as opções de autenticação disponíveis. Observe que a autenticação Kerberos em Java puro está disponível a partir da versão 4.0 do driver.  
  
|||  
|-|-|  
|Plataforma|Autenticação|  
|Não Windows|Kerberos Java puro|  
|Não Windows|SQL Server|  
|Windows|Kerberos Java puro|  
|Windows|SQL Server|  
|Windows|Kerberos com backup NTLM|  
|Windows|NTLM|  
  
**O driver suporta o protocolo de Internet versão 6 (IPv6) endereços?**  
 O driver JDBC dá suporte ao uso de endereços IPv6 com a coleção de propriedades de conexão e com a propriedade de cadeia de conexão serverName. Para obter mais informações, consulte [criar a URL de Conexão](../../connect/jdbc/building-the-connection-url.md).  
  
**O que é o buffer adaptável?**  
 O buffer adaptável foi introduzido a partir do Microsoft SQL Server 2005 JDBC Driver versão 1.2 e foi projetado para recuperar qualquer tipo de dados com valores grandes sem a sobrecarga de cursores de servidor. O recurso de buffer adaptável do Microsoft SQL Server JDBC Driver oferece uma propriedade de cadeia de caracteres de conexão, responseBuffering, que pode ser definida como "adaptive" ou "full". A partir do driver JDBC versão 2.0, o comportamento padrão do driver é "adaptive". Em outras palavras, para obter o comportamento de buffer adaptável, o aplicativo não precisa solicitar o comportamento adaptável explicitamente. No entanto, na versão 1.2 o modo padrão de buffer "full" e o aplicativo precisava solicitar explicitamente o modo de buffer adaptável. Para obter mais informações, consulte [usando buffer adaptável](../../connect/jdbc/using-adaptive-buffering.md) tópico e o blog do [que is Adaptive Response buffering e por que devo usar?](http://go.microsoft.com/fwlink/?LinkId=111575).  
  
**É o pool de conexão do driver suporte?**  
 O driver dá suporte ao pool de conexões da Plataforma Java, Edição Enterprise 5 (Java EE 5). O driver JDBC implementa as interfaces do JDBC 3.0 necessárias para permitir que o driver participe de qualquer implementação de pool de conexões disponibilizada pelos fornecedores de servidores de aplicativos em middleware. O driver participa das conexões em pool nesses ambientes. Para obter mais informações, consulte [Pooling de Conexão usando](../../connect/jdbc/using-connection-pooling.md). O driver não fornece sua própria implementação do pool. Em vez disso, ele utiliza servidores de aplicativos Java de terceiros.  
  
**O suporte está disponível para o driver?**  
 Há diversas opções de suporte disponíveis. Você pode postar a pergunta ou emitir para nosso [repositório GitHub](https://github.com/microsoft/mssql-jdbc) que é monitorado pela Microsoft. [Fóruns](http://go.microsoft.com/fwlink/?LinkID=246673) monitorados pela Microsoft, MVPS e pela comunidade. Entre em contato com o Suporte ao Cliente Microsoft. Podemos pedir que você reproduza o problema fora de qualquer servidor de aplicativos de terceiros. Se o problema não puder ser reproduzido fora do ambiente de hospedagem do contêiner Java, você precisará acionar os terceiros envolvidos para que possamos continuar a ajudá-lo. Para melhor ajudá-lo, podemos também pedir que você reproduza o problema em um sistema operacional como o Windows.  
  
**O driver é certificado para uso com qualquer servidor de aplicativos de terceiros?**
O driver foi testado com todos os principais servidores de aplicativos, inclusive IBM WebSphere e SAP NetWeaver.  
  
**Como habilitar o rastreamento?**  
 O driver dá suporte ao uso de rastreamento (ou registro em log) para ajudar a resolver problemas com o driver JDBC usado em seu aplicativo. Para habilitar o uso de rastreamento do JAR do lado do cliente, o driver JDBC usa as APIs de registro em log em java.util.logging. Para obter mais informações, consulte [a operação de rastreamento do Driver](../../connect/jdbc/tracing-driver-operation.md). Para o rastreamento XA do lado do servidor, consulte [Rastreamento do acesso a dados no SQL Server](http://go.microsoft.com/fwlink/?LinkId=248705).  
  
**Onde posso baixar as versões mais antigas do driver, como o driver JDBC do SQL Server 2000, 2005 driver, 1.0, 1.1 ou 1.2 do driver?**  
 Essas versões de driver não estão disponíveis para download, pois não têm mais suporte. Estamos aperfeiçoando continuamente nosso suporte à conectividade com Java. Portanto, é altamente recomendável que você trabalhe com a versão mais recente do nosso driver JDBC.  
  
 **Estou usando o JRE 1.4. Qual driver é compatível com o JRE 1.4** para os clientes estão usando produtos SAP e que precisam de suporte ao JRE 1.4, você poderá entrar em contato [SAPService Marketplace](http://service.sap.com/) para obter o Microsoft JDBC driver 1.2.  
  
**Pode o driver se comunicar usando algoritmos validados pelos FIPS?** O Microsoft JDBC Driver não contém nenhum algoritmo de criptografia. Se o cliente utilizar sistema operacional, aplicativos e algoritmos JVM considerados aceitáveis de acordo com os Federal Information Processing Standards (FIPS) e configurar o driver para usar esses algoritmos, o driver usará somente os algoritmos designados para comunicação.  
  
  

