---
title: Home page para programação do cliente SQL | Microsoft Docs
description: Página com links anotados para downloads e documentação para diferentes linguagens e sistemas operacionais, para se conectar ao SQL Server ou ao Banco de Dados SQL do Azure.
author: David-Engel
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-daveng
ms.author: v-daenge
ms.openlocfilehash: 561cb6e02ac26db3c1d5c9a61fcf689bcca5360d
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725514"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Home page da programação do cliente para Microsoft SQL Server


Bem-vindo à nossa home page sobre programação do cliente para interagir com Microsoft SQL Server e com o Banco de Dados SQL do Azure na nuvem. Este artigo fornece as seguintes informações:

- Lista e descreve as combinações de linguagem e driver disponíveis.
  - As informações são fornecidas para os sistemas operacionais Linux (Ubuntu e outros), macOS e Windows.
- Fornece links para a documentação detalhada de cada combinação.
- Exibe as áreas e subáreas da documentação hierárquica para determinadas linguagens, quando apropriado.


#### <a name="azure-sql-database"></a>Banco de Dados SQL do Azure

Em qualquer idioma, o código que se conecta ao SQL Server é quase idêntico ao código para se conectar ao Banco de Dados SQL do Azure.

Para obter detalhes sobre as cadeias de conexão para se conectar ao Banco de Dados SQL do Azure, confira:

- [Usar o .NET Core (C#) para consultar um Banco de Dados SQL do Azure](/azure/sql-database/sql-database-connect-query-dotnet-core).
- Outros artigos do Banco de Dados SQL do Azure que estão próximos ao artigo anterior no sumário, sobre outras linguagens. Por exemplo, confira [Usar PHP para consultar um Banco de Dados SQL do Azure](/azure/sql-database/sql-database-connect-query-php).


#### <a name="build-an-app-webpages"></a>Páginas da Web sobre criação de aplicativos

Nossas páginas da Web sobre *criação de aplicativos* apresentam exemplos de código, juntamente com as informações de configuração, em um formato alternativo. Para obter mais informações, confira mais adiante neste artigo a [seção rotulada *Site sobre criação de aplicativos*](#an-204-aka-ms-sqldev).



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>Idiomas e drivers para programas clientes


Na tabela a seguir, cada imagem de idioma é um link para detalhes sobre como usar o idioma com o SQL Server. Cada link leva a uma seção posterior neste artigo.

:::row:::
    :::column:::
        [![Logotipo do C#][image-ref-320-csharp]](#an-110-ado-net-docu)  

        [![Logotipo do Node.js][image-ref-340-node]](#an-140-node-js-docu)  

        [![Logotipo do Python][image-ref-370-python]](#an-180-python-docu)  
    :::column-end:::
    :::column:::
        [![Entity Framework de ORM, do .NET Framework][image-ref-333-ef]](#an-116-csharp-ef-orm)  

        [**`ODBC for C++`**](#an-160-odbc-cpp-docu)<br/>[![cpp-big-plus][image-ref-322-cpp]](#an-160-odbc-cpp-docu)  

        [![Logotipo do Ruby][image-ref-380-ruby]](#an-190-ruby-docu)  
    :::column-end:::
    :::column:::
        [![Logotipo do Java][image-ref-330-java]](#an-130-jdbc-docu)  

        [![Logotipo do PHP][image-ref-360-php]](#an-170-php-docu)  
    :::column-end:::
:::row-end:::

#### <a name="downloads-and-installs"></a>Downloads e instalações

O seguinte artigo é dedicado ao download e à instalação de vários drivers de conexão SQL, para uso por linguagens de programação:

- [Drivers do SQL Server](./sql-connection-libraries.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![Logotipo do C#][image-ref-320-csharp] C# usando ADO.NET

As linguagens gerenciadas pelo .NET, como C# e Visual Basic, são os usuários mais comuns do ADO.net. *ADO.NET* é um nome casual para um subconjunto de classes .NET Framework.

#### <a name="code-examples"></a>Exemplos de código

| Exemplo | Descrição |
| :-- | :-- |
| [Prova de conceito da conexão ao SQL usando ADO.NET](./ado-net/step-3-connect-sql-ado-net.md) | Um pequeno exemplo de código focado em conexão e consulta ao SQL Server. |
| [Conectar-se de forma resiliente ao SQL com ADO.NET](./ado-net/step-4-connect-resiliently-sql-ado-net.md) | Lógica de repetição em um exemplo de código, porque as conexões podem ocasionalmente sofrer tempo de perda de conectividade.<br /><br />A lógica de repetição se aplica bem às conexões mantidas pela Internet em qualquer banco de dados de nuvem, como no Banco de Dados SQL do Azure. |
| [Banco de Dados SQL do Azure: Demonstração de como usar o .NET Core no Windows/Linux/macOS para criar um programa em C#, para se conectar e consultar](/azure/sql-database/sql-database-connect-query-dotnet-core) | Exemplo de exportação do Banco de Dados SQL do Azure. |
| [Criação de aplicativos: C#, ADO.NET, Windows](https://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | Informações de configuração, com exemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentação

| Área | Descrição |
| :-- | :-- |
| [C# usando ADO.NET](./ado-net/microsoft-ado-net-sql-server.md)| Raiz da nossa documentação. |
| [Namespace: System.Data](/dotnet/api/system.data) | Um conjunto de classes usado para ADO.NET. |
| [Namespace: Microsoft.Data.SqlClient](/dotnet/api/microsoft.data.SqlClient) | O conjunto de classes usado para o Provedor de Dados Microsoft .NET para SQL Server |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Logotipo do Entity Framework][image-ref-333-ef] EF (Entity Framework) com C&#x23;

O EF (Entity Framework) fornece o ORM (Mapeamento Relacional de Objeto). O ORM torna mais fácil para o código-fonte OOP (Programação Orientada a Objeto) manipular dados que foram recuperados de um Banco de Dados SQL relacional.

O EF tem relações diretas ou indiretas com as seguintes tecnologias:

- .NET Framework
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/) ou [LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- Aprimoramentos de sintaxe de linguagem, como o operador **=>** em C#.
- Programas práticos que geram código-fonte para classes mapeadas para as tabelas no Banco de Dados SQL. Por exemplo, [EdmGen.exe](/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe).


#### <a name="original-ef-and-new-ef"></a>EF original e novo EF

A [página inicial do Entity Framework](/ef/) apresenta o EF com uma descrição semelhante à seguinte:

- O Entity Framework é um mapeador relacional de objeto (O/RM) que permite aos desenvolvedores do .NET trabalhar com um banco de dados usando objetos .NET. Com ele, não há a necessidade da maioria dos códigos-fonte de acesso a dados que os desenvolvedores geralmente precisam para escrever.

*Entity Framework* é um nome compartilhado por dois branches de código-fonte separadas. Um branch do EF é mais antigo e seu código-fonte agora pode ser mantido pelo público. O outro EF é novo. Os dois EFs são descritos abaixo:

| Versão | Descrição |
| :-- | :-- |
| [EF 6.x](/ef/ef6/) | A Microsoft lançou o EF primeiramente em agosto de 2008. Em março de 2015, a Microsoft anunciou que o EF 6. x foi a versão final que ela desenvolveria. A Microsoft lançou o código-fonte para o domínio público.<br /><br />Inicialmente, o EF era parte do .NET Framework. Mas o EF 6. x foi removido do .NET Framework.<br /><br />[Código-fonte do EF 6.x no GitHub, no repositório *aspnet/EntityFramework6*](https://github.com/aspnet/EntityFramework6) |
| [EF Core](/ef/core/) | A Microsoft lançou o EF Core recém-desenvolvido em junho de 2016. O EF Core foi criado para oferecer melhor flexibilidade e portabilidade. O EF Core pode ser executado em outros sistemas operacionais além do Microsoft Windows. E o EF Core pode interagir com outros bancos de dados além do Microsoft SQL Server e outros bancos de dados relacionais.<br /><br />**C&#x23; exemplos de código:**<br />[Introdução ao Entity Framework Core](/ef/core/get-started/index)<br />[Introdução ao EF Core no .NET Framework com um Banco de dados existente](/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

O EF e as tecnologias relacionadas são poderosas e são muito mais interessantes para o desenvolvedor que deseja dominar toda a área.

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Logotipo do Java][image-ref-330-java] Java e JDBC

A Microsoft fornece um driver JDBC (Java Database Connectivity) para usar com o SQL Server (ou com o Banco de Dados SQL do Azure). É um driver JDBC Tipo 4 que fornece conectividade de banco de dados por meio das APIs (interfaces de programa aplicativo) JDBC padrão.

#### <a name="code-examples"></a>Exemplos de código

| Exemplo | Descrição |
| :-- | :-- |
| [Exemplos de código](./jdbc/sample-jdbc-driver-applications.md) | Exemplos de código que ensinam sobre tipos de dados, conjuntos de resultados e dados grandes. |
| [Exemplo de URL de conexão](./jdbc/connection-url-sample.md) | Descreve como usar uma URL de conexão para se conectar ao SQL Server. Em seguida, use-o para utilizar uma instrução SQL para recuperar dados. |
| [Exemplo de fonte de dados](./jdbc/data-source-sample.md) | Descreve como usar uma fonte de dados para se conectar ao SQL Server. Então, use um procedimento armazenado para recuperar dados. |
| [Usar o Java para consultar um Banco de Dados SQL do Azure](/azure/sql-database/sql-database-connect-query-java) | Exemplo de exportação do Banco de Dados SQL do Azure. |
| [Criar aplicativos Java usando o SQL Server no Ubuntu](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | Informações de configuração, com exemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentação

A documentação do JDBC inclui as seguintes áreas principais:

| Área | Descrição |
| :-- | :-- |
| [JDBC (Java Database Connectivity)](./jdbc/microsoft-jdbc-driver-for-sql-server.md) | Raiz da nossa documentação do JDBC. |
| [Referência](./jdbc/reference/jdbc-driver-api-reference.md) | Interfaces, classes e membros. |
| [Guia de programação para o driver SQL JDBC](./jdbc/programming-guide-for-jdbc-sql-driver.md) | Informações de configuração, com exemplos de código. |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Logotipo do Node.js][image-ref-340-node] Node.js

Com o Node.js, você pode se conectar ao SQL Server do Windows, Linux ou macOS. A raiz da nossa documentação do Node.js está [aqui](./node-js/node-js-driver-for-sql-server.md).

O driver de conexão Node.js para SQL Server é implementado em JavaScript. O driver usa o protocolo TDS, que tem suporte em todas as versões atuais do SQL Server. O driver é um projeto de software livre [disponível no GitHub](https://tediousjs.github.io/tedious/).

#### <a name="code-examples"></a>Exemplos de código

| Exemplo | Descrição |
| :-- | :-- |
| [Prova de conceito da conexão ao SQL usando o Node.js](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | Código-fonte de funções básicas para se conectar ao SQL Server e executar uma consulta. |
| [Banco de Dados SQL do Azure: Usar o Node.js para consultar](/azure/sql-database/sql-database-connect-query-nodejs) | Exemplo de Banco de Dados SQL do Azure na nuvem. |
| [Criar aplicativos Node.js para usar o SQL Server no macOS](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) | Informações de configuração, com exemplos de código. |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>ODBC para C++

![Logotipo do ODBC][image-ref-350-odbc] ![cpp-big-plus][image-ref-322-cpp]

O ODBC (Open Database Connectivity) foi desenvolvido na década de 1990 e precede o .NET Framework. O ODBC foi criado para ser independente de qualquer sistema de banco de dados específico e sistema operacional.

Ao longo dos anos, vários drivers ODBC foram criados e lançados por grupos dentro e fora da Microsoft. A variedade de drivers envolve diversas linguagens de programação de cliente. A lista de destinos de dados vai muito além do SQL Server.

Alguns outros drivers de conectividade usam ODBC internamente.

#### <a name="code-example"></a>Exemplo de código

- [Exemplo de código C++ usando o ODBC](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>Estrutura de tópicos da documentação

O conteúdo ODBC nesta seção concentra-se em acessar o SQL Server ou o Banco de Dados SQL do Azure, de C++. A tabela a seguir lista uma estrutura de tópicos aproximada da documentação principal do ODBC.


| Área | Subárea | Descrição |
| :--- | :------ | :---------- |
| [ODBC para C++](./odbc/microsoft-odbc-driver-for-sql-server.md) | Raiz da nossa documentação. |
| [Linux-macOS](./odbc/linux-mac/system-requirements.md) | &nbsp; | Informações de uso do ODBC nos sistemas operacionais Linux ou macOS. |
| [Windows](./odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)     | &nbsp; | Informações de uso do ODBC no sistema operacional Windows. |
| [Administração](../odbc/admin/odbc-data-source-administrator.md) | &nbsp; | A ferramenta administrativa para gerenciar fontes de dados ODBC. |
| [Microsoft](../odbc/microsoft/microsoft-supplied-odbc-drivers.md)  | &nbsp; | Vários drivers ODBC que são criados e fornecidos pela Microsoft. |
| [Conceito e referência](../odbc/reference/introduction-to-odbc.md) | &nbsp; | Informações conceituais sobre a interface ODBC, além das referências tradicionais. |
| &nbsp; " | [Apêndices](../odbc/reference/appendixes/odbc-appendixes.md)    | Tabelas de transição de estado, biblioteca de cursores ODBC e mais. |
| &nbsp; " | [Aplicativo do desenvolver](../odbc/reference/develop-app/checking-feature-support-and-variability.md)  | Funções, identificadores e muito mais. |
| &nbsp; " | [Driver do desenvolvedor](../odbc/reference/develop-driver/developing-an-odbc-driver.md) | Como desenvolver um driver ODBC próprio, se você tiver uma fonte de dados especializada. |
| &nbsp; " | [Instalar](../odbc/reference/install/odbc-subkey.md) | Instalação do ODBC, subchaves e mais. |
| &nbsp; " | [Sintaxe](../odbc/reference/syntax/odbc-reference.md)   | APIs para instalação, instalador, tradução e acesso a dados. |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![Logotipo do PHP][image-ref-360-php] PHP

Você pode usar PHP para interagir com o SQL Server. A raiz da nossa documentação do PHP está [aqui](./php/microsoft-php-driver-for-sql-server.md).

#### <a name="code-examples"></a>Exemplos de código

| Exemplo | Descrição |
| :-- | :-- |
| [Prova de conceito da conexão ao SQL usando PHP](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | Um pequeno exemplo de código focado em conexão e consulta ao SQL Server. |
| [Conectar-se de forma resiliente ao SQL com PHP](./php/step-4-connect-resiliently-to-sql-with-php.md) | Lógica de repetição em um exemplo de código, porque as conexões por meio da Internet e da nuvem podem ocasionalmente sofrer tempo de perda de conectividade. |
| [Banco de Dados SQL do Azure: Usar PHP para consultar](/azure/sql-database/sql-database-connect-query-php) | Exemplo de exportação do Banco de Dados SQL do Azure. |
| [Criar aplicativos PHP para usar o SQL Server no RHEL](https://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | Informações de configuração, com exemplos de código. |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Logotipo do Python][image-ref-370-python] Python


Você pode usar Python para interagir com o SQL Server.

#### <a name="code-examples"></a>Exemplos de código

| Exemplo | Descrição |
| :-- | :-- |
| [Prova de conceito da conexão ao SQL com Python usando o pyodbc](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | Um pequeno exemplo de código focado em conexão e consulta ao SQL Server. |
| [Banco de Dados SQL do Azure: Usar Python para consultar](/azure/sql-database/sql-database-connect-query-python) | Exemplo de exportação do Banco de Dados SQL do Azure. |
| [Criar aplicativos PHP para usar o SQL Server no SLES](https://www.microsoft.com/sql-server/developer-get-started/python/sles/) | Informações de configuração, com exemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentação

| Área | Descrição |
| :--- | :---------- |
| [Python para SQL Server](./python/python-driver-for-sql-server.md) | Raiz da nossa documentação. |
| [pymssql driver](./python/pymssql/python-sql-driver-pymssql.md) | A Microsoft não mantém nem testa o driver pymssql.<br /><br />O driver de conexão pymssql é uma interface simples para bancos de dados SQL para uso em programas Python. O Pymssql compila na FreeTDS para fornecer uma interface Python DB-API (PEP-249) para o Microsoft SQL Server. |
| [driver pyodbc](./python/pyodbc/python-sql-driver-pyodbc.md)   | O driver de conexão pyodbc é um módulo Python de software livre que simplifica o acesso a bancos de dados ODBC. Ele implementa a especificação do DB API 2,0, mas é fornecido com maior conveniência de Python. |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Logotipo do Ruby][image-ref-380-ruby] Ruby

Você pode usar Ruby para interagir com o SQL Server. A raiz da nossa documentação do Ruby está [aqui](./ruby/ruby-driver-for-sql-server.md).

#### <a name="code-examples"></a>Exemplos de código

| Exemplo | Descrição |
| :-- | :-- |
| [Prova de conceito da conexão ao SQL usando Ruby](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | Um pequeno exemplo de código focado em conexão e consulta ao SQL Server. |
| [Banco de Dados SQL do Azure: Usar Ruby para consultar](/azure/sql-database/sql-database-connect-query-ruby) | Exemplo de exportação do Banco de Dados SQL do Azure. |
| [Criar aplicativos Ruby para usar o SQL Server no macOS](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | Informações de configuração, com exemplos de código. |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-development"></a>[Site sobre criação de aplicativos, para desenvolvimento de cliente SQL](https://www.microsoft.com/sql-server/developer-get-started/)


Em nossas páginas da Web sobre [*criação de aplicativos*](https://www.microsoft.com/sql-server/developer-get-started/), você pode escolher entre as opções de uma longa lista de linguagens de programação para se conectar ao SQL Server. E seu programa cliente pode executar uma variedade de sistemas operacionais.

O site sobre *criação de aplicativos* enfatiza a simplicidade e a integridade do desenvolvedor que está começando. As etapas explicam as seguintes tarefas:

1. Como instalar o Microsoft SQL Server
2. Como baixar e instalar ferramentas e drivers.
3. Como fazer as configurações necessárias, conforme apropriado para o sistema operacional escolhido.
4. Como compilar o código-fonte fornecido.
5. Como executar o programa.

Veja abaixo algumas estruturas de tópicos aproximadas dos detalhes fornecidos no site:

#### <a name="java-on-ubuntu"></a>Java no Ubuntu

1. Configure seu ambiente
    - Etapa 1.1 Instalar o SQL Server
    - Etapa 1.2 Instalar o Java
    - Etapa 1.3 Instalar o Java Development Kit (JDK)
    - Etapa 1.4 Instalar o Maven
2. Crie aplicativo Java com SQL Server
    - Etapa 2.1 Criar um aplicativo Java que se conecta ao SQL Server e executa consultas
    - Etapa 2.2 Criar um aplicativo Java que se conecta ao SQL Server usando a estrutura popular de hibernação
3. Torne seu aplicativo Java 100x mais rápido
    - Etapa 3.1 Criar um aplicativo Java para demonstrar índices Columnstore

#### <a name="python-on-windows"></a>Python no Windows

1. Configure seu ambiente
    - Etapa 1.1 Instalar o SQL Server
    - Etapa 1.2 Instalar o Python
    - Etapa 1.3 Instalar o driver ODBC e o utilitário de linha de comando do SQL para SQL Server
2. Crie um aplicativo Python com o SQL Server
    - Etapa 2.1 Instalar o driver do Python para SQL Server
    - Etapa 2.2 Criar um banco de dados para seu aplicativo
    - Etapa 2.3 Criar um aplicativo Python que se conecta ao SQL Server e executa consultas
3. Torne seu aplicativo Python 100x mais rápido
    - Etapa 3.1 Criar uma tabela com 5 milhões usando sqlcmd
    - Etapa 3.2 Criar um aplicativo Python que consulta essa tabela e mede o tempo gasto
    - Etapa 3.3 Medir quanto tempo demora para executar a consulta
    - Etapa 3.4 Adicionar um índice columnstore à sua tabela
    - Etapa 3.5 Medir quanto tempo demora para executar a consulta com um índice columnstore

As capturas de tela a seguir dão uma ideia sobre o nosso site de documentação de desenvolvimento do SQL.

#### <a name="choose-a-language"></a>Escolher um idioma

![Site de Desenvolvimento SQL, introdução][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>Escolher um sistema operacional

![Site SQL Dev, Java Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>Outro desenvolvimento


Esta seção fornece links sobre outras opções de desenvolvimento. Isso inclui o uso dessas mesmas linguagens para o desenvolvimento do Azure em geral. As informações vão além do direcionamento apenas ao Banco de Dados SQL do Azure e Microsoft SQL Server.

#### <a name="developer-hub-for-azure"></a>Hub de desenvolvedor para o Azure

- [Hub de desenvolvedor para o Azure](/azure/)
- [Azure para desenvolvedores .NET](/dotnet/azure/)
- [Azure para desenvolvedores Java](/java/azure/)
- [Azure para desenvolvedores Node.js](/nodejs/azure/)
- [Azure para desenvolvedores do Python](/python/azure/)
- [Criar um aplicativo Web do PHP no Azure](/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>Outros idiomas

- [Criar aplicativos Go usando o SQL Server no Windows](https://www.microsoft.com/sql-server/developer-get-started/go/windows/)



<!-- Image references. -->

[image-ref-322-cpp]: ./media/homepage-sql-connection-drivers/gm-cpp-4point-p61f.png
[image-ref-320-csharp]: ./media/homepage-sql-connection-drivers/gm-csharp-c10c.png
[image-ref-333-ef]: ./media/homepage-sql-connection-drivers/gm-entity-framework-ef20d.png
[image-ref-330-java]: ./media/homepage-sql-connection-drivers/gm-java-j18c.png
[image-ref-340-node]: ./media/homepage-sql-connection-drivers/gm-node-n30.png
[image-ref-350-odbc]: ./media/homepage-sql-connection-drivers/gm-odbc-ic55826-o35.png
[image-ref-360-php]: ./media/homepage-sql-connection-drivers/gm-php-php60.png
[image-ref-370-python]: ./media/homepage-sql-connection-drivers/gm-python-py72.png
[image-ref-380-ruby]: ./media/homepage-sql-connection-drivers/gm-ruby-un-r82.png
[image-ref-390-aka-ms-sqldev-choose-language]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-400-aka-ms-sqldev-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png