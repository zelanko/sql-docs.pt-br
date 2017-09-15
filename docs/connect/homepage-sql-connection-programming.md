---
title: "Home page para programação do cliente SQL | Microsoft Docs"
description: "Página de hub com anotado links para downloads e documentação para várias combinações de idiomas e sistemas operacionais, para conectar-se ao SQL Server ou para o banco de dados do SQL Azure."
author: MightyPen
ms.date: 09/13/2017
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.topic: article
ms.reviewer: meetb
ms.author: genemi
ms.translationtype: MT
ms.sourcegitcommit: 71ca2fac0a6b9f087f9d434c5a701f5656889b9e
ms.openlocfilehash: 000325a2e2c53e36f7a74a725962b8dd3be98988
ms.contentlocale: pt-br
ms.lasthandoff: 09/13/2017

---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Home page do cliente de programação para o Microsoft SQL Server


Bem-vindo à nossa página inicial sobre o cliente de programação para interagir com o Microsoft SQL Server e com o banco de dados SQL Azure na nuvem. Este artigo fornece as seguintes informações:

- Lista e descreve as combinações de idioma e drivers disponíveis.
    - Informações são fornecidas para os sistemas operacionais do Windows, Linux (Ubuntu e outros) e MacOS.
- Fornece links para a documentação detalhada para cada combinação.
- Exibe as áreas e subáreas da documentação hierárquica para determinados idiomas, quando apropriado.


#### <a name="azure-sql-database"></a>Banco de dados SQL do Azure

Em qualquer idioma, o código que se conecta ao SQL Server é quase idêntico ao código para se conectar ao banco de dados do SQL Azure.

Para obter detalhes sobre as cadeias de caracteres de conexão para se conectar ao banco de dados do SQL Azure, consulte:

- [Use o .NET Core (c#) para consultar um banco de dados do SQL Azure](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core).
- Outro banco de dados SQL que estão próximos o artigo anterior na tabela de conteúdo, outras linguagens. Por exemplo, consulte [PHP usado para consultar um banco de dados do SQL Azure](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php).


#### <a name="build-an-app-webpages"></a>Construir um aplicativo páginas da Web

Nosso *construir um aplicativo* páginas da Web apresentam exemplos de código, juntamente com informações de configuração em um formato alternativo. Para obter mais informações, consulte este artigo o [seção rotulada *site construir um aplicativo*](#an-204-aka-ms-sqldev).



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>Idiomas e os drivers para programas clientes


Na tabela a seguir, cada imagem de idioma é um link para detalhes sobre como usar o idioma com o SQL Server. Cada link salta para uma seção mais adiante neste artigo.

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| &nbsp;[! [C# logotipo] [imagem-ref-320-csharp]](#an-110-ado-net-docu) | &nbsp;[! [ORM do Entity Framework, do .NET Framework] [imagem-ref-333-ef]](#an-116-csharp-ef-orm) | &nbsp;[! [Logotipo de Java] [imagem-ref-330-java]](#an-130-jdbc-docu) |
| &nbsp;[! [Node. js logotipo] [-ref-340-nó de imagem]](#an-140-node-js-docu) | &nbsp; [**`ODBC for C++`**](#an-160-odbc-cpp-docu) | &nbsp;[! [Logotipo PHP] [imagem-ref-360-php]](#an-170-php-docu) |
| &nbsp;[! [Logotipo Python] [imagem-ref-370-python]](#an-180-python-docu) | &nbsp;[! [Ruby logotipo] [imagem-ref-380-ruby]](#an-190-ruby-docu) | &nbsp; ... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>Baixa e instala

O seguinte artigo é dedicada para o download e instalar vários drivers de conexão de SQL, para uso de linguagens de programação:

- [Drivers do SQL Server](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![Logotipo do c#][image-ref-320-csharp] C# usando o ADO.NET

Linguagens .NET gerenciados, como c# e Visual Basic, são os usuários mais comuns do ADO.NET. *ADO.NET* é um nome casual para um subconjunto de classes do .NET Framework.

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Prova de conceito se conectar ao SQL usando o ADO.NET](./ado-net/step-3-proof-of-concept-connecting-to-sql-using-ado-net.md) | Um exemplo de código pequeno voltada para se conectar e consultar o SQL Server. |
| [Atenda com flexibilidade conectar ao SQL com o ADO.NET](./ado-net/step-4-connect-resiliently-to-sql-with-ado-net.md) | Lógica de repetição em um exemplo de código, como conexões, ocasionalmente, podem experimentar momentos de perda de conectividade.<br /><br />Lógica de repetição se aplica também a conexões mantidas por meio da internet em qualquer banco de dados de nuvem, como o banco de dados do Azure SQL. |
| [Banco de dados SQL do Azure: A demonstração de como usar o .NET Core em Linux/Windows/macOS para criar um programa em c#, para se conectar e consultar](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Exemplo de banco de dados SQL do Azure. |
| [Construir um aplicativo: Windows c#, ADO.NET,](http://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | Informações de configuração, junto com exemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentação

|||
| :-- | :-- |
| [C# usando o ADO.NET](./ado-net/index.md)| Raiz de nossa documentação. |
| [Namespace: System. Data](http://docs.microsoft.com/dotnet/api/system.data) | Um conjunto de classes usadas para ADO.NET. |
| [Namespace: SqlClient](http://docs.microsoft.com/dotnet/api/system.data.SqlClient) | O conjunto de classes que são mais diretamente o centro do ADO.NET. |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Logotipo do Entity Framework][image-ref-333-ef] Entity Framework (EF) com C & #x x23;

Entity Framework (EF) fornece um mapeamento relacional de objeto (ORM). ORM torna mais fácil para seu código-fonte Oriented programação OOP () manipular os dados que foi recuperados de um banco de dados relacional do SQL.

EF não tem relação direta ou indireta com as seguintes tecnologias:

- .NET Framework
- [O LINQ to SQL](http://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/), ou [LINQ to Entities](http://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- Aprimoramentos da sintaxe de linguagem, como o ** => ** operador em c#.
- Programas útil geram código-fonte para classes que mapeiam para as tabelas no banco de dados SQL. Por exemplo, [EdmGen.exe](http://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe).


#### <a name="original-ef-and-new-ef"></a>EF original e a nova EF

O [página inicial para Entity Framework](http://docs.microsoft.com/ef/) apresenta EF com uma descrição semelhante à seguinte:

- Entity Framework é um mapeador relacional de objeto (O/RM) que permite que os desenvolvedores de .NET trabalhar com um banco de dados usando objetos do .NET Framework. Elimina a necessidade de mais do que os desenvolvedores geralmente precisam escrever código-fonte acesso a dados.

*Entity Framework* é um nome compartilhado por duas ramificações do código fonte separado. Uma ramificação EF é mais antiga e seu código-fonte agora pode ser mantido pelo público. O outros EF é novo. O dois EFs é descrito a seguir:

|     |     |
| :-- | :-- |
| [EF 6. x](http://docs.microsoft.com/ef/ef6/) | Primeiro, a Microsoft lançou EF em agosto de 2008. Em março de 2015, a Microsoft anunciou que EF 6. x foi a versão final que desenvolve Microsoft. A Microsoft lançou o código-fonte para o domínio público.<br /><br />Inicialmente EF fazia parte do .NET Framework. Mas EF 6. x foi removido do .NET Framework.<br /><br />[Código-fonte EF 6. x no Github no repositório *aspnet/EntityFramework6*](http://github.com/aspnet/EntityFramework6) |
| [Núcleo EF](http://docs.microsoft.com/ef/core/) | A Microsoft lançou o núcleo de EF recentemente desenvolvidos em junho de 2016. Núcleo EF destina-se a melhor flexibilidade e portabilidade. EF Core pode executar em sistemas operacionais além apenas o Microsoft Windows. E EF Core pode interagir com outros bancos de dados relacionais e bancos de dados além apenas o Microsoft SQL Server.<br /><br />**C & #x x23; exemplos de código:**<br />[Guia de Introdução do Entity Framework Core](https://docs.microsoft.com/ef/core/get-started/index)<br />[Guia de Introdução ao EF principal no .NET Framework com um banco de dados existente](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF e as tecnologias relacionadas são poderosas e são muito a aprender para o desenvolvedor que queira mestre toda a área.

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Logotipo de Java][image-ref-330-java] Java e JDBC

Microsoft fornece um driver Java Database Connectivity (JDBC) para uso com o SQL Server (ou com o Azure SQL Database, obviamente). É um driver JDBC tipo 4, e fornece conectividade de banco de dados por meio de interfaces de programa de aplicativo do JDBC de padrão (APIs).

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Exemplos de código](./jdbc/code-samples/index.md) | Exemplos de código que ensina sobre os tipos de dados, conjuntos de resultados e dados grandes. |
| [Exemplo de URL de conexão](./jdbc/connection-url-sample.md) | Descreve como usar uma URL de conexão para se conectar ao SQL Server. Em seguida, usá-lo para usar uma instrução SQL para recuperar dados. |
| [Exemplo de fonte de dados](./jdbc/data-source-sample.md) | Descreve como usar uma fonte de dados para se conectar ao SQL Server. Em seguida, use um procedimento armazenado para recuperar dados. |
| [Usar o Java para consultar um banco de dados do SQL Azure](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Exemplo de banco de dados SQL do Azure. |
| [Criação de aplicativos Java usando o SQL Server no Ubuntu](http://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | Informações de configuração, junto com exemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentação

A documentação do JDBC inclui as seguintes áreas principais:

|||
| :-- | :-- |
| [Java Database Connectivity (JDBC)](./jdbc/index.md) | Raiz de nossa documentação de JDBC. |
| [Referência](./jdbc/reference/index.md) | Interfaces, classes e membros. |
| [Guia de programação para o driver SQL JDBC](./jdbc/programming-guide-for-jdbc-sql-driver.md) | Informações de configuração, junto com exemplos de código. |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Logotipo do Node. js][image-ref-340-node] Node.js

Com Node. js você pode conectar-se ao SQL Server do Windows, Linux ou Mac. A raiz da nossa documentação Node. js é [aqui](./node-js/index.md).

O driver de conexão do Node.js para SQL Server é implementado em JavaScript. O driver usa o protocolo TDS, que tem suporte em todas as versões atuais do SQL Server. O driver é um projeto de código-fonte aberto, [disponível no Github](http://tediousjs.github.io/tedious/).

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Prova de conceito se conectar ao SQL usando o Node. js](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | Esqueleto de código para se conectar ao SQL Server e executar uma consulta de origem. |
| [Banco de dados SQL do Azure: Use Node. js para consulta](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | Exemplo de banco de dados SQL Azure na nuvem. |
| [Criar aplicativos do Node.js para usar o SQL Server em macOS](http://www.microsoft.com/sql-server/developer-get-started/node/mac/) | Informações de configuração, junto com exemplos de código. |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>ODBC para C++ 

![Logotipo do ODBC][image-ref-350-odbc]

Conectividade aberta de banco de dados (ODBC) foi desenvolvida na década de 1990 e ele antecede o .NET Framework. ODBC é projetado para ser independente de qualquer sistema de banco de dados específico e independente do sistema operacional.

Ao longo dos anos vários drivers ODBC foram criados e liberados por grupos dentro e fora da Microsoft. O intervalo de drivers envolvem várias linguagens de programação do cliente. A lista de destinos de dados vai muito além do SQL Server.

Alguns outros drivers de conectividade usam ODBC internamente.

#### <a name="code-example"></a>Exemplo de código

- [Exemplo de código C++, usando o ODBC](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>Estrutura de tópicos de documentação

O conteúdo ODBC nesta seção se concentra em acessar o SQL Server ou banco de dados SQL Azure, do C++. A tabela a seguir lista uma estrutura de tópicos aproximada da documentação principal para ODBC.


| Área | Subárea | Description |
| :--- | :------ | :---------- |
| [ODBC para C++](./odbc/index.md) | Raiz de nossa documentação. |
| [Mac Linux](./odbc/linux-mac/index.md) | &nbsp; | Informações sobre como usar o ODBC nos sistemas operacionais Linux ou MacOS. |
| [Windows](./odbc/windows/index.md)     | &nbsp; | Informações sobre como usar o ODBC no sistema operacional Windows. |
| [Administração](../odbc/admin/index.md) | &nbsp; | A ferramenta administrativa para gerenciar fontes de dados ODBC. |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | Vários drivers ODBC que são criados e fornecidos pela Microsoft. |
| [Conceitual e referência](../odbc/reference/index.md) | &nbsp; | Informações conceituais sobre a interface ODBC, além de referência tradicional. |
| &nbsp; " | [Apêndices](../odbc/reference/appendixes/index.md)    | Tabelas de transição de estado, biblioteca de cursores ODBC e muito mais. |
| &nbsp; " | [Desenvolvimento de aplicativo](../odbc/reference/develop-app/index.md)  | Funções, identificadores e muito mais. |
| &nbsp; " | [Desenvolvimento de driver](../odbc/reference/develop-driver/index.md) | Como desenvolver seu próprio driver ODBC, se você tiver uma fonte de dados especializado. |
| &nbsp; " | [Instalar](../odbc/reference/install/index.md) | Instalação do ODBC, subchaves e muito mais. |
| &nbsp; " | [Sintaxe](../odbc/reference/syntax/index.md)   | APIs de acesso a dados, instalador, conversão e a instalação. |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![Logotipo do PHP][image-ref-360-php] PHP

Você pode usar PHP para interagir com o SQL Server. A raiz da nossa documentação Node. js é [aqui](./php/index.md).

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Prova de conceito, conectar-se ao SQL usando PHP](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | Um exemplo de código pequeno voltada para se conectar e consultar o SQL Server. |
| [Atenda com flexibilidade conectar ao SQL com PHP](./php/step-4-connect-resiliently-to-sql-with-php.md) | Lógica de repetição em um exemplo de código, pois conexões por meio da Internet e na nuvem, ocasionalmente, podem ocorrer momentos de perda de conectividade. |
| [Banco de dados SQL do Azure: Use PHP para consulta](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Exemplo de banco de dados SQL do Azure. |
| [Criar aplicativos do PHP para usar o SQL Server em RHEL](http://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | Informações de configuração, junto com exemplos de código. |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Logotipo do Python][image-ref-370-python] Python


Você pode usar o Python para interagir com o SQL Server.

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Prova de conceito se conectar ao SQL com Python usando pyodbc](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | Um exemplo de código pequeno voltada para se conectar e consultar o SQL Server. |
| [Banco de dados SQL do Azure: Use Python para consulta](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Exemplo de banco de dados SQL do Azure. |
| [Criar aplicativos do PHP para usar o SQL Server em SLES](http://www.microsoft.com/sql-server/developer-get-started/python/sles/) | Informações de configuração, junto com exemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentação

| Área | Description |
| :--- | :---------- |
| [Python para o SQL Server](./python/index.md) | Raiz de nossa documentação. |
| [driver pymssql](./python/pymssql/index.md) | A Microsoft não manter ou teste o driver pymssql.<br /><br />O driver de conexão pymssql é uma interface simples para bancos de dados SQL, para uso em programas de Python. Pymssql se baseia nos FreeTDS para fornecer uma interface de Python API DB (PEP 249) para o Microsoft SQL Server. |
| [driver pyodbc](./python/pyodbc/index.md)   | O driver de conexão pyodbc é um módulo de Python de software livre que simplifica o acesso aos bancos de dados ODBC. Ele implementa a especificação de banco de dados API 2.0, mas é fornecido com a conveniência de Pythonic ainda mais. |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Logotipo do Ruby][image-ref-380-ruby] Ruby

Você pode usar o Ruby para interagir com o SQL Server. A raiz da nossa documentação Ruby é [aqui](./ruby/index.md).

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Prova de conceito se conectar ao SQL com Ruby](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | Um exemplo de código pequeno voltada para se conectar e consultar o SQL Server. |
| [Banco de dados SQL do Azure: Use Ruby para consulta](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Exemplo de banco de dados SQL do Azure. |
| [Criar aplicativos Ruby para usar o SQL Server em MacOS](http://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | Informações de configuração, junto com exemplos de código. |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpwwwmicrosoftcomsql-serverdeveloper-get-started"></a>[Site de construir um aplicativo, para desenvolvimento de cliente do SQL](http://www.microsoft.com/sql-server/developer-get-started/)


Em nosso [ *construir um aplicativo* ](https://www.microsoft.com/sql-server/developer-get-started/) páginas da Web, você pode escolher entre uma lista extensa de idiomas para se conectar ao SQL Server de programação. E o programa cliente pode executar uma variedade de sistemas operacionais.

*Construir um aplicativo* enfatiza a simplicidade e integridade para o desenvolvedor que está iniciando. As etapas explicam as seguintes tarefas:

1. Como instalar o Microsoft SQL Server
2. Como baixar e instalar as ferramentas e drivers.
3. Como fazer todas as configurações necessárias, conforme apropriado para seu sistema operacional escolhido.
4. Como compilar o código-fonte fornecido.
5. Como executar o programa.

Em seguida são algumas estruturas aproximadas os detalhes fornecidos no site:

#### <a name="java-on-ubuntu"></a>Java no Ubuntu:

1. Configurar seu ambiente
    - Etapa 1.1 instalar o SQL Server
    - A etapa 1.2 instalar Java
    - Etapa 1.3 instalar Java Development Kit (JDK)
    - Etapa 1.4 instalar Maven
2. Criar um aplicativo Java com o SQL Server
    - Etapa 2.1 criar um aplicativo Java que se conecta ao SQL Server e executa consultas
    - Etapa 2.2 criar um aplicativo Java que se conecta ao SQL Server usando a estrutura popular hibernação
3. Tornar seu aplicativo Java até 100 vezes mais rápido
    - Etapa 3.1: criar um aplicativo Java para demonstrar os índices Columnstore

#### <a name="python-on-windows"></a>Python no Windows:

1. Configurar seu ambiente
    - Etapa 1.1 instalar o SQL Server
    - A etapa 1.2 instalar Python
    - Etapa 1.3 instalar o Driver ODBC e o utilitário de linha de comando SQL para SQL Server
2. Criar aplicativo de Python com o SQL Server
    - Etapa 2.1 instalar o driver do Python para o SQL Server
    - Etapa 2.2 criar um banco de dados para seu aplicativo
    - Etapa 2.3: criar um aplicativo do Python que se conecta ao SQL Server e executa consultas
3. Tornar seu aplicativo de Python até 100 vezes mais rápido
    - Etapa 3.1: criar uma nova tabela com 5 milhões usando o sqlcmd
    - Etapa 3.2 criar um aplicativo do Python que consulta esta tabela e mede o tempo gasto
    - Etapa 3.3 medir quanto tempo leva para executar a consulta
    - Etapa 3.4 adicionar um índice columnstore para sua tabela
    - Etapa 3.5 medir quanto tempo leva para executar a consulta com um índice columnstore

As capturas de tela a seguir dão uma ideia da aparência de nosso site de documentação de desenvolvimento do SQL.

#### <a name="choose-a-language"></a>Escolha um idioma:

![Site de desenvolvimento do SQL, Introdução][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>Escolha um sistema operacional:

![Site de desenvolvimento do SQL, Ubuntu Java][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>Outro desenvolvimento


Esta seção fornece links sobre outras opções de desenvolvimento. Essas opções incluem usar esses mesmos idiomas do desenvolvimento do Azure em geral. As informações de ultrapassar direcionando apenas o banco de dados do SQL Azure e o Microsoft SQL Server.

#### <a name="developer-hub-for-azure"></a>Hub de desenvolvedor do Azure

- [Hub de desenvolvedor do Azure](http://docs.microsoft.com/azure/)
- [Azure para desenvolvedores do .NET](http://docs.microsoft.com/dotnet/azure/)
- [Azure para desenvolvedores de Java](http://docs.microsoft.com/java/azure/)
- [Azure para desenvolvedores de Node.js](http://docs.microsoft.com/nodejs/azure/)
- [Azure para desenvolvedores Python](http://docs.microsoft.com/python/azure/)
- [Criar um aplicativo web do PHP no Azure](http://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>Outros idiomas

- [Criar aplicativos Go usando o SQL Server no Windows](http://www.microsoft.com/sql-server/developer-get-started/go/windows/)



<!-- Image references. -->

[image-ref-310-ado-net]: ./media/homepage-sql-connection-drivers/gm-ado-net-an51.png
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


