---
title: Home page da programação do cliente SQL | Microsoft Docs
description: Página de hub com anotado links para downloads e documentação para várias combinações de linguagens e sistemas operacionais, para conectar-se ao SQL Server ou banco de dados de SQL do Azure.
author: MightyPen
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-daveng
ms.author: genemi
ms.openlocfilehash: d773e05a3ed953e5210c0ade3226b4a32e82aeab
ms.sourcegitcommit: 8cc38f14ec72f6f420479dc1b15eba64b1a58041
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/08/2018
ms.locfileid: "51289896"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Home page da programação para Microsoft SQL Server do cliente


Bem-vindo à nossa home page sobre programação para interagir com o Microsoft SQL Server e banco de dados SQL Azure na nuvem do cliente. Este artigo fornece as seguintes informações:

- Lista e descreve as combinações de idioma e o driver disponíveis.
    - Informações são fornecidas para os sistemas operacionais do Windows, MacOS e Linux (Ubuntu e outros).
- Fornece links para a documentação detalhada de cada combinação.
- Exibe as áreas e subáreas da documentação hierárquica para determinados idiomas, quando apropriado.


#### <a name="azure-sql-database"></a>Banco de dados SQL do Azure

Em qualquer idioma, o código que se conecta ao SQL Server é quase idêntico ao código para se conectar ao banco de dados SQL.

Para obter detalhes sobre as cadeias de caracteres de conexão para se conectar ao banco de dados SQL, consulte:

- [Usar o .NET Core (c#) para consultar um banco de dados SQL do Azure](/azure/sql-database/sql-database-connect-query-dotnet-core).
- Outro banco de dados SQL que estão próximos o artigo anterior na tabela de conteúdo, sobre outras linguagens. Por exemplo, consulte [usar PHP para consultar um banco de dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php).


#### <a name="build-an-app-webpages"></a>Páginas de compilação um aplicativo da Web

Nossos *Build um aplicativo* páginas da Web apresentam exemplos de código, juntamente com informações de configuração, em um formato alternativo. Para obter mais informações, consulte mais adiante neste artigo a [seção rotulada *site do Build um aplicativo*](#an-204-aka-ms-sqldev).



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>Idiomas e drivers para programas cliente


Na tabela a seguir, cada imagem de idioma é um link para detalhes sobre como usar a linguagem com o SQL Server. Cada link salta para uma seção mais adiante neste artigo.

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| &nbsp; [![Logotipo do c#][image-ref-320-csharp]](#an-110-ado-net-docu) | &nbsp; [![Estrutura de entidades ORM do .NET Framework][image-ref-333-ef]](#an-116-csharp-ef-orm) | &nbsp; [![Logotipo do Java][image-ref-330-java]](#an-130-jdbc-docu) |
| &nbsp; [![Logotipo do Node. js][image-ref-340-node]](#an-140-node-js-docu) | &nbsp; [**`ODBC for C++`**](#an-160-odbc-cpp-docu)<br/>[![CPP big plus][image-ref-322-cpp]](#an-160-odbc-cpp-docu) | &nbsp; [![Logotipo do PHP][image-ref-360-php]](#an-170-php-docu) |
| &nbsp; [![Logotipo do Python][image-ref-370-python]](#an-180-python-docu) | &nbsp; [![Logotipo do Ruby][image-ref-380-ruby]](#an-190-ruby-docu) | &nbsp;... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>Baixa e instala

O artigo a seguir é dedicado para o download e instalar vários drivers de conexão do SQL, para uso por linguagens de programação:

- [Drivers do SQL Server](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![Logotipo do c#][image-ref-320-csharp] Em C# usando o ADO.NET

As linguagens do .NET gerenciados, como c# e Visual Basic, são os usuários mais comuns do ADO.NET. *ADO.NET* é um nome casual para um subconjunto de classes do .NET Framework.

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Prova de conceito da conexão ao SQL usando ADO.NET](./ado-net/step-3-proof-of-concept-connecting-to-sql-using-ado-net.md) | Um exemplo de código pequeno voltadas para se conectar e consultar o SQL Server. |
| [Conectar-se de forma resiliente ao SQL com ADO.NET](./ado-net/step-4-connect-resiliently-to-sql-with-ado-net.md) | Lógica de repetição em um exemplo de código, porque as conexões podem ocasionalmente sofrer momentos de perda de conectividade.<br /><br />A lógica de repetição se aplica também a conexões mantidas por meio da internet em qualquer banco de dados de nuvem, como o banco de dados do Azure SQL. |
| [Banco de dados SQL do Azure: Demonstração como usar o .NET Core no Windows/Linux/macOS para criar um programa em C#, conectar e consultar](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Exemplo de banco de dados SQL do Azure. |
| [Construir um aplicativo: C#, ADO.NET, Windows](https://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | Informações de configuração, junto com exemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentação

|||
| :-- | :-- |
| [Em C# usando o ADO.NET](./ado-net/index.md)| Raiz de nossa documentação. |
| [Namespace: System. Data](https://docs.microsoft.com/dotnet/api/system.data) | Um conjunto de classes usadas para o ADO.NET. |
| [Namespace: System.Data.SqlClient](https://docs.microsoft.com/dotnet/api/system.data.SqlClient) | O conjunto de classes que são mais diretamente o centro do ADO.NET. |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Logotipo do Entity Framework][image-ref-333-ef] Entity Framework (EF) com C&#x23;

Entity Framework (EF) fornece um mapeamento relacional de objeto (ORM). ORM torna mais fácil para seu código-fonte Object-Oriented Programming (OOP) manipular os dados que foi recuperados de um banco de dados relacional do SQL.

O EF tem relações diretas ou indiretas com as seguintes tecnologias:

- .NET Framework
- [LINQ to SQL](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/), ou [LINQ to Entities](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- Aprimoramentos da sintaxe de linguagem, tais como o **=>** operador em c#.
- Programas úteis, que geram o código-fonte para classes que são mapeados para as tabelas no banco de dados SQL. Por exemplo, [EdmGen.exe](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe).


#### <a name="original-ef-and-new-ef"></a>EF original e novo EF

O [página inicial para o Entity Framework](https://docs.microsoft.com/ef/) apresenta EF com uma descrição semelhante à seguinte:

- Entity Framework é um mapeador relacional de objeto (O/RM) que permite que os desenvolvedores de .NET trabalhar com um banco de dados usando objetos .NET. Ele elimina a necessidade para a maioria do código-fonte acesso a dados que os desenvolvedores geralmente precisam escrever.

*Entity Framework* é um nome compartilhado por duas ramificações de código de origem separado. Uma ramificação do EF é mais antiga, e seu código-fonte agora pode ser mantido pelo público. O EF outro é novo. O duas EFs é descrito a seguir:

|     |     |
| :-- | :-- |
| [O EF 6.x](https://docs.microsoft.com/ef/ef6/) | Primeiro, a Microsoft lançou o EF em agosto de 2008. Em março de 2015, a Microsoft anunciou que o EF 6.x foi a versão final que a Microsoft desenvolve. A Microsoft lançou o código-fonte para o domínio público.<br /><br />Inicialmente, o EF era parte do .NET Framework. Mas o EF 6.x foi removido do .NET Framework.<br /><br />[Código do EF 6.x-fonte no Github, no repositório *aspnet/EntityFramework6*](https://github.com/aspnet/EntityFramework6) |
| [O EF Core](https://docs.microsoft.com/ef/core/) | A Microsoft lançou o EF Core recém-desenvolvido em junho de 2016. EF Core foi projetado para melhorar a flexibilidade e portabilidade. O EF Core pode executar em sistemas operacionais além de apenas o Microsoft Windows. E o EF Core pode interagir com outros bancos de dados relacionais e bancos de dados além de apenas o Microsoft SQL Server.<br /><br />**C&#x23; exemplos de código:**<br />[Introdução ao Entity Framework Core](https://docs.microsoft.com/ef/core/get-started/index)<br />[Introdução ao EF Core no .NET Framework com um banco de dados existente](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF e as tecnologias relacionadas são poderosas e são muito a aprender para desenvolvedores que queiram toda a área do mestre.

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Logotipo do Java][image-ref-330-java] Java e JDBC

Microsoft fornece um driver de conectividade de banco de dados Java (JDBC) para uso com o SQL Server (ou com o banco de dados SQL, obviamente). É um driver JDBC Tipo 4 que fornece conectividade de banco de dados por meio das APIs (interfaces de programa aplicativo) JDBC padrão.

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Exemplos de código](./jdbc/code-samples/index.md) | Exemplos de código que ensinam sobre tipos de dados, conjuntos de resultados e dados grandes. |
| [Exemplo de URL de conexão](./jdbc/connection-url-sample.md) | Descreve como usar uma URL de conexão para se conectar ao SQL Server. Em seguida, usá-lo para usar uma instrução SQL para recuperar dados. |
| [Exemplo de fonte de dados](./jdbc/data-source-sample.md) | Descreve como usar uma fonte de dados para se conectar ao SQL Server. Em seguida, use um procedimento armazenado para recuperar dados. |
| [Use o Java para consultar um banco de dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Exemplo de banco de dados SQL do Azure. |
| [Criar aplicativos Java usando o SQL Server no Ubuntu](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | Informações de configuração, junto com exemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentação

A documentação do JDBC inclui as principais áreas a seguir:

|||
| :-- | :-- |
| [Java Database Connectivity (JDBC)](./jdbc/index.md) | Raiz de nossa documentação do JDBC. |
| [Referência](./jdbc/reference/index.md) | Interfaces, classes e membros. |
| [Guia de programação para o driver SQL JDBC](./jdbc/programming-guide-for-jdbc-sql-driver.md) | Informações de configuração, junto com exemplos de código. |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Logotipo do Node. js][image-ref-340-node] Node.js

Com o Node. js você pode conectar-se ao SQL Server do Windows, Linux ou Mac. É a raiz da nossa documentação do Node. js [aqui](./node-js/index.md).

O driver de conexão Node. js para SQL Server é implementado em JavaScript. O driver usa o protocolo TDS, que é compatível com todas as versões atuais do SQL Server. O driver é um projeto de código-fonte aberto [disponível no Github](https://tediousjs.github.io/tedious/).

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Prova de conceito da conexão ao SQL usando o Node.js](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | Básica o código para conectar-se ao SQL Server e executar uma consulta de origem. |
| [Banco de dados SQL do Azure: usar Node. js à consulta](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | Exemplo de banco de dados SQL Azure na nuvem. |
| [Criar aplicativos Node. js para usar o SQL Server no macOS](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) | Informações de configuração, junto com exemplos de código. |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>ODBC para C++ 

![Logotipo do ODBC][image-ref-350-odbc] ![CPP big plus][image-ref-322-cpp]

Conectividade de banco de dados aberto (ODBC) foi desenvolvida na década de 1990, e ele antecede o .NET Framework. ODBC é projetado para ser independente de qualquer sistema de banco de dados específico e independente do sistema operacional.

Ao longo dos anos vários drivers ODBC foram criados e lançados por grupos de dentro e fora da Microsoft. O intervalo de drivers envolvem várias linguagens de programação do cliente. A lista de destinos de dados vai muito além do SQL Server.

Alguns outros drivers de conectividade usam ODBC internamente.

#### <a name="code-example"></a>Exemplo de código

- [Exemplo de código C++, usando o ODBC](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>Estrutura de tópicos da documentação

O conteúdo do ODBC nesta seção se concentra em acessar o SQL Server ou banco de dados SQL Azure, do C++. A tabela a seguir lista um esboço aproximado da principal documentação do ODBC.


| Área | Subárea | Descrição |
| :--- | :------ | :---------- |
| [ODBC para C++](./odbc/index.md) | Raiz de nossa documentação. |
| [Mac-Linux](./odbc/linux-mac/index.md) | &nbsp; | Informações sobre como usar o ODBC nos sistemas operacionais Linux ou MacOS. |
| [Windows](./odbc/windows/index.md)     | &nbsp; | Informações sobre como usar o ODBC no sistema operacional Windows. |
| [Administração](../odbc/admin/index.md) | &nbsp; | A ferramenta administrativa para gerenciar fontes de dados ODBC. |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | Vários drivers ODBC que são criados e fornecidos pela Microsoft. |
| [Conceitual e referência](../odbc/reference/index.md) | &nbsp; | Informações conceituais sobre a interface ODBC, além de referência tradicional. |
| &nbsp; " | [Apêndices](../odbc/reference/appendixes/index.md)    | Tabelas de transição de estado, biblioteca de cursores ODBC e muito mais. |
| &nbsp; " | [Desenvolver um aplicativo](../odbc/reference/develop-app/index.md)  | Funções, identificadores e muito mais. |
| &nbsp; " | [Desenvolver um driver](../odbc/reference/develop-driver/index.md) | Como desenvolver seu próprio driver ODBC, se você tiver uma fonte de dados especializados. |
| &nbsp; " | [Instalar](../odbc/reference/install/index.md) | Instalação do ODBC, subchaves e muito mais. |
| &nbsp; " | [Sintaxe](../odbc/reference/syntax/index.md)   | APIs para acesso a dados, instalador, conversão e a instalação. |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![Logotipo do PHP][image-ref-360-php] PHP

Você pode usar PHP para interagir com o SQL Server. É a raiz da nossa documentação sobre PHP [aqui](./php/index.md).

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Prova de conceito da conexão ao SQL usando PHP](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | Um exemplo de código pequeno voltadas para se conectar e consultar o SQL Server. |
| [Conectar-se de forma resiliente ao SQL com PHP](./php/step-4-connect-resiliently-to-sql-with-php.md) | Lógica de repetição em um exemplo de código, porque as conexões através da Internet e a nuvem podem ocasionalmente sofrer momentos de perda de conectividade. |
| [Banco de dados SQL do Azure: Use PHP para consulta](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Exemplo de banco de dados SQL do Azure. |
| [Crie aplicativos PHP para usar o SQL Server no RHEL](https://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | Informações de configuração, junto com exemplos de código. |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Logotipo do Python][image-ref-370-python] Python


Você pode usar o Python para interagir com o SQL Server.

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Prova de conceito da conexão ao SQL com Python usando pyodbc](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | Um exemplo de código pequeno voltadas para se conectar e consultar o SQL Server. |
| [Banco de dados SQL do Azure: usar Python para consulta](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Exemplo de banco de dados SQL do Azure. |
| [Crie aplicativos PHP para usar o SQL Server em SLES](https://www.microsoft.com/sql-server/developer-get-started/python/sles/) | Informações de configuração, junto com exemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentação

| Área | Descrição |
| :--- | :---------- |
| [Python para o SQL Server](./python/index.md) | Raiz de nossa documentação. |
| [driver pymssql](./python/pymssql/index.md) | A Microsoft não manter ou teste o driver pymssql.<br /><br />O driver de conexão pymssql é uma interface simples para bancos de dados SQL, para uso em programas do Python. Pymssql se baseia na FreeTDS para fornecer uma interface de DB – API do Python (PEP 249) ao Microsoft SQL Server. |
| [driver pyodbc](./python/pyodbc/index.md)   | O driver de conexão de pyodbc é um módulo de Python de software livre que simplifica o acesso aos bancos de dados ODBC. Ele implementa a especificação de DB API 2.0, mas é fornecido com a conveniência de Pythonic ainda mais. |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Logotipo do Ruby][image-ref-380-ruby] Ruby

Você pode usar o Ruby para interagir com o SQL Server. É a raiz da nossa documentação do Ruby [aqui](./ruby/index.md).

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Prova de conceito da conexão ao SQL usando Ruby](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | Um exemplo de código pequeno voltadas para se conectar e consultar o SQL Server. |
| [Banco de dados SQL do Azure: usar Ruby para consulta](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Exemplo de banco de dados SQL do Azure. |
| [Criar aplicativos Ruby para usar o SQL Server no MacOS](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | Informações de configuração, junto com exemplos de código. |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpswwwmicrosoftcomsql-serverdeveloper-get-started"></a>[Site de compilação um aplicativo, para desenvolvimento de cliente do SQL](https://www.microsoft.com/sql-server/developer-get-started/)


No nosso [ *Build-um-app* ](https://www.microsoft.com/sql-server/developer-get-started/) páginas da Web, você pode escolher entre uma longa lista de linguagens para se conectar ao SQL Server de programação. E o programa cliente pode executar uma variedade de sistemas operacionais.

*Construir um aplicativo* enfatiza a simplicidade e integridade para o desenvolvedor que está apenas começando. As etapas explicam as seguintes tarefas:

1. Como instalar o Microsoft SQL Server
2. Como baixar e instalar as ferramentas e drivers.
3. Como fazer todas as configurações necessárias, conforme apropriado para seu sistema operacional escolhido.
4. Como compilar o código-fonte fornecido.
5. Como executar o programa.

Em seguida, estão algumas estruturas de tópicos aproximadas dos detalhes fornecidos no site da:

#### <a name="java-on-ubuntu"></a>Java no Ubuntu:

1. Configurar seu ambiente
    - Etapa 1.1 Instalar o SQL Server
    - Etapa 1.2 instalar Java
    - Etapa 1.3 instalar o Java Development Kit (JDK)
    - Etapa 1.4 instalar Maven
2. Criar um aplicativo Java com o SQL Server
    - Etapa 2.1: criar um aplicativo Java que se conecta ao SQL Server e executa consultas
    - Etapa 2.2: criar um aplicativo Java que se conecta ao SQL Server usando a estrutura popular Hibernar
3. Tornar seu aplicativo Java até 100 vezes mais rápido
    - Etapa 3.1: criar um aplicativo Java para demonstrar os índices Columnstore

#### <a name="python-on-windows"></a>Python no Windows:

1. Configurar seu ambiente
    - Etapa 1.1 Instalar o SQL Server
    - Etapa 1.2 instalar Python
    - Etapa 1.3 instalar o Driver ODBC e o utilitário de linha de comando SQL para SQL Server
2. Criar aplicativo Python com o SQL Server
    - Etapa 2.1 instalar o driver Python para SQL Server
    - Etapa 2.2: criar um banco de dados para seu aplicativo
    - Etapa 2.3: criar um aplicativo Python que se conecta ao SQL Server e executa consultas
3. Tornar seu aplicativo Python até 100 vezes mais rápido
    - Etapa 3.1: criar uma nova tabela com 5 milhões usando o sqlcmd
    - Etapa 3.2: criar um aplicativo Python que consulta esta tabela e mede o tempo gasto
    - Etapa 3.3 medir quanto tempo leva para executar a consulta
    - Etapa 3.4 adicionar um índice columnstore para sua tabela
    - Etapa 3.5 medir quanto tempo leva para executar a consulta com um índice columnstore

As capturas de tela a seguir lhe dar uma ideia da aparência de nosso site de documentação de desenvolvimento do SQL.

#### <a name="choose-a-language"></a>Escolha um idioma:

![Site de desenvolvimento do SQL, Introdução][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>Escolha um sistema operacional:

![Site de desenvolvimento do SQL, Ubuntu do Java][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>Outro desenvolvimento


Esta seção fornece links sobre outras opções de desenvolvimento. Essas opções incluem usar esses mesmos idiomas para desenvolvimento do Azure em geral. As informações vai além de direcionar apenas o banco de dados SQL e o Microsoft SQL Server.

#### <a name="developer-hub-for-azure"></a>Hub do desenvolvedor do Azure

- [Hub do desenvolvedor do Azure](https://docs.microsoft.com/azure/)
- [Azure para desenvolvedores .NET](https://docs.microsoft.com/dotnet/azure/)
- [Azure para desenvolvedores de Java](https://docs.microsoft.com/java/azure/)
- [Azure para desenvolvedores do Node. js](https://docs.microsoft.com/nodejs/azure/)
- [Azure para desenvolvedores do Python](https://docs.microsoft.com/python/azure/)
- [Criar um aplicativo web PHP no Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>Outros idiomas

- [Crie aplicativos Go usando o SQL Server no Windows](https://www.microsoft.com/sql-server/developer-get-started/go/windows/)



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

