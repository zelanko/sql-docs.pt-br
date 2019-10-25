---
title: Home Page para programação de cliente SQL | Microsoft Docs
description: Página de Hub com links anotados para downloads e documentação para várias combinações de idiomas e sistemas operacionais, para se conectar a SQL Server ou ao banco de dados SQL do Azure.
author: MightyPen
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-daveng
ms.author: genemi
ms.openlocfilehash: 6961f8c23b4acfd787958cc9a160faf88362b54c
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451856"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Home page da programação do cliente para Microsoft SQL Server


Bem-vindo à nossa home page sobre programação de cliente para interagir com Microsoft SQL Server e com o banco de dados SQL do Azure na nuvem. Este artigo fornece as seguintes informações:

- Lista e descreve as combinações de idioma e driver disponíveis.
    - As informações são fornecidas para os sistemas operacionais Linux (Ubuntu e outros), MacOS e Windows.
- Fornece links para a documentação detalhada de cada combinação.
- Exibe as áreas e subáreas da documentação hierárquica para determinados idiomas, quando apropriado.


#### <a name="azure-sql-database"></a>Banco de dados SQL do Azure

Em qualquer idioma específico, o código que se conecta a SQL Server é quase idêntico ao código para se conectar ao banco de dados SQL do Azure.

Para obter detalhes sobre as cadeias de conexão para conexão com o banco de dados SQL do Azure, consulte:

- [Use o .NET CoreC#() para consultar um banco de dados SQL do Azure](/azure/sql-database/sql-database-connect-query-dotnet-core).
- Outro banco de dados SQL do Azure que está próximo ao artigo anterior no sumário, sobre outros idiomas. Por exemplo, consulte [usar PHP para consultar um banco de dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php).


#### <a name="build-an-app-webpages"></a>Páginas da Web de Build-a-App

Nossas páginas da Web *Build-a-app* apresentam exemplos de código, juntamente com as informações de configuração, em um formato alternativo. Para obter mais informações, consulte mais adiante neste artigo a [seção chamada *site Build-a-app*](#an-204-aka-ms-sqldev).



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>Idiomas e drivers para programas cliente


Na tabela a seguir, cada imagem de idioma é um link para detalhes sobre como usar o idioma com SQL Server. Cada link salta para uma seção posterior neste artigo.

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| [logotipo doC# &nbsp; ![][image-ref-320-csharp]](#an-110-ado-net-docu) | &nbsp; [![ORM Entity Framework de .NET Framework][image-ref-333-ef]](#an-116-csharp-ef-orm) | &nbsp; [![Logotipo do Java][image-ref-330-java]](#an-130-jdbc-docu) |
| logotipo do &nbsp; [![Node. js][image-ref-340-node]](#an-140-node-js-docu) | &nbsp; [ **`ODBC for C++`** ](#an-160-odbc-cpp-docu)<br/>[![cpp-big-plus][image-ref-322-cpp]](#an-160-odbc-cpp-docu) | logotipo do &nbsp; [![PHP][image-ref-360-php]](#an-170-php-docu) |
| &nbsp; [![Logotipo do Python][image-ref-370-python]](#an-180-python-docu) | logotipo do &nbsp; [![Ruby][image-ref-380-ruby]](#an-190-ruby-docu) | &nbsp;... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>Downloads e instalações

O artigo a seguir é dedicado ao download e à instalação de vários drivers de conexão SQL, para uso por linguagens de programação:

- [Drivers do SQL Server](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![C#logotipo][image-ref-320-csharp] C#usando ADO.NET

As linguagens gerenciadas pelo .NET C# , como e Visual Basic, são os usuários mais comuns do ADO.net. *ADO.net* é um nome casual para um subconjunto de classes .NET Framework.

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Prova de conceito da conexão ao SQL usando ADO.NET](./ado-net/step-3-connect-sql-ado-net.md) | Um pequeno exemplo de código focado na conexão e na consulta de SQL Server. |
| [Conectar-se de forma resiliente ao SQL com ADO.NET](./ado-net/step-4-connect-resiliently-sql-ado-net.md) | Lógica de repetição em um exemplo de código, porque as conexões podem ocasionalmente sofrer tempo de perda de conectividade.<br /><br />A lógica de repetição se aplica bem às conexões mantidas pela Internet em qualquer banco de dados de nuvem, como no banco de dados SQL do Azure. |
| [Banco de dados SQL do Azure: demonstração de como usar o .NET Core no Windows/Linux/macOS C# para criar um programa, conectar-se e consultar](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Exemplo de banco de dados SQL do Azure. |
| [Build-a-App: C#, ADO.net, Windows](https://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | Informações de configuração, juntamente com exemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentação

|||
| :-- | :-- |
| [C#usando ADO.NET](./ado-net/index.md)| Raiz da nossa documentação. |
| [Namespace: System.Data](https://docs.microsoft.com/dotnet/api/system.data) | Um conjunto de classes usado para ADO.NET. |
| [Namespace: System.Data.SqlClient](https://docs.microsoft.com/dotnet/api/system.data.SqlClient) | O conjunto de classes que são mais diretamente o centro do ADO.NET. |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Logotipo do Entity Framework][image-ref-333-ef] Entity Framework (EF) com C&#x23;

Entity Framework (EF) fornece o mapeamento relacional de objeto (ORM). O ORM torna mais fácil para o código-fonte OOP (programação orientada a objeto) manipular dados que foram recuperados de um banco de dado SQL relacional.

O EF tem relações diretas ou indiretas com as seguintes tecnologias:

- .NET Framework
- [LINQ to SQL](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/)ou [LINQ to Entities](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- Aprimoramentos de sintaxe de linguagem, como o operador de C# **=>** no.
- Programas práticos que geram código-fonte para classes que são mapeadas para as tabelas no banco de dados SQL. Por exemplo, [EdmGen. exe](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe).


#### <a name="original-ef-and-new-ef"></a>EF original e novo EF

A [página inicial de Entity Framework](https://docs.microsoft.com/ef/) introduz o EF com uma descrição semelhante à seguinte:

- Entity Framework é um mapeador relacional de objeto (O/RM) que permite que os desenvolvedores do .NET trabalhem com um banco de dados usando objetos .NET. Ele elimina a necessidade da maior parte do código-fonte do acesso a dados que os desenvolvedores geralmente precisam escrever.

*Entity Framework* é um nome compartilhado por duas ramificações de código-fonte separadas. Uma ramificação do EF é mais antiga e seu código-fonte agora pode ser mantido pelo público. O outro EF é novo. Os dois EFs são descritos a seguir:

|     |     |
| :-- | :-- |
| [EF 6.x](https://docs.microsoft.com/ef/ef6/) | A Microsoft lançou primeiro o EF em agosto de 2008. Em março de 2015, a Microsoft anunciou que o EF 6. x foi a versão final que a Microsoft desenvolveria. A Microsoft liberou o código-fonte para o domínio público.<br /><br />Inicialmente, o EF era parte de .NET Framework. Mas o EF 6. x foi removido da .NET Framework.<br /><br />[Código-fonte do EF 6. x no GitHub, no repositório *ASPNET/EntityFramework6*](https://github.com/aspnet/EntityFramework6) |
| [EF Core](https://docs.microsoft.com/ef/core/) | A Microsoft lançou o EF Core desenvolvido recentemente em junho de 2016. O EF Core foi projetado para melhor flexibilidade e portabilidade. O EF Core pode ser executado em sistemas operacionais além do Microsoft Windows. E EF Core podem interagir com bancos de dados além de apenas Microsoft SQL Server e outros bancos de dados relacionais.<br /><br />**Exemplos&#x23; de código C:**<br />[Introdução com Entity Framework Core](https://docs.microsoft.com/ef/core/get-started/index)<br />[Introdução ao EF Core no .NET Framework com um banco de dados existente](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

O EF e as tecnologias relacionadas são poderosas e são muito mais atraentes para o desenvolvedor que deseja dominar toda a área.

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Logotipo do Java][image-ref-330-java] Java e JDBC

A Microsoft fornece um driver Java Database Connectivity (JDBC) para uso com SQL Server (ou com o banco de dados SQL do Azure, é claro). É um driver JDBC Tipo 4 que fornece conectividade de banco de dados por meio das APIs (interfaces de programa aplicativo) JDBC padrão.

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Exemplos de código](./jdbc/code-samples/index.md) | Exemplos de código que ensinam sobre tipos de dados, conjuntos de resultados e dados grandes. |
| [Exemplo de URL de conexão](./jdbc/connection-url-sample.md) | Descreve como usar uma URL de conexão para se conectar ao SQL Server. Em seguida, use-o para usar uma instrução SQL para recuperar dados. |
| [Exemplo de fonte de dados](./jdbc/data-source-sample.md) | Descreve como usar uma fonte de dados para se conectar a SQL Server. Em seguida, use um procedimento armazenado para recuperar dados. |
| [Usar o Java para consultar um banco de dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Exemplo de banco de dados SQL do Azure. |
| [Criar aplicativos Java usando o SQL Server no Ubuntu](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | Informações de configuração, juntamente com exemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentação

A documentação do JDBC inclui as seguintes áreas principais:

|||
| :-- | :-- |
| [Java Database Connectivity (JDBC)](./jdbc/index.md) | Raiz da nossa documentação do JDBC. |
| [Referência](./jdbc/reference/index.md) | Interfaces, classes e membros. |
| [Guia de programação para o driver SQL JDBC](./jdbc/programming-guide-for-jdbc-sql-driver.md) | Informações de configuração, juntamente com exemplos de código. |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Logotipo do node. js][image-ref-340-node] Node.js

Com o Node. js, você pode se conectar a SQL Server do Windows, Linux ou Mac. A raiz da nossa documentação do node. js está [aqui](./node-js/index.md).

O driver de conexão node. js para SQL Server é implementado em JavaScript. O driver usa o protocolo TDS, que é compatível com todas as versões modernas do SQL Server. O driver é um projeto de código-fonte aberto, [disponível no GitHub](https://tediousjs.github.io/tedious/).

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Prova de conceito da conexão ao SQL usando o Node.js](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | Código-fonte de Bones simples para se conectar a SQL Server e executar uma consulta. |
| [Banco de dados SQL do Azure: Use node. js para consultar](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | Exemplo de banco de dados SQL do Azure na nuvem. |
| [Criar aplicativos node. js para usar o SQL Server no macOS](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) | Informações de configuração, juntamente com exemplos de código. |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>ODBC paraC++ 

![Logotipo do ODBC][image-ref-350-odbc] ![cpp-big-plus][image-ref-322-cpp]

O ODBC (Open Database Connectivity) foi desenvolvido na década de 1990 e .NET Framework. O ODBC foi projetado para ser independente de qualquer sistema de banco de dados específico e independente do sistema operacional.

Ao longo dos anos, vários drivers ODBC foram criados e liberados por grupos dentro e fora da Microsoft. A variedade de drivers envolve várias linguagens de programação de cliente. A lista de destinos de dados vai muito além SQL Server.

Alguns outros drivers de conectividade usam o ODBC internamente.

#### <a name="code-example"></a>Exemplo de código

- [Exemplo de código C++ usando o ODBC](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>Estrutura de tópicos da documentação

O conteúdo ODBC nesta seção concentra-se em acessar o SQL Server ou o banco de dados SQL C++do Azure, de. A tabela a seguir lista um esboço aproximado da documentação principal do ODBC.


| Área | Subárea | Descrição |
| :--- | :------ | :---------- |
| [ODBC paraC++](./odbc/index.md) | Raiz da nossa documentação. |
| [Linux-Mac](./odbc/linux-mac/index.md) | &nbsp; | Informações sobre como usar o ODBC nos sistemas operacionais Linux ou MacOS. |
| [Windows](./odbc/windows/index.md)     | &nbsp; | Informações sobre como usar o ODBC no sistema operacional Windows. |
| [Administração](../odbc/admin/index.md) | &nbsp; | A ferramenta administrativa para gerenciar fontes de dados ODBC. |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | Vários drivers ODBC que são criados e fornecidos pela Microsoft. |
| [Conceitual e referência](../odbc/reference/index.md) | &nbsp; | Informações conceituais sobre a interface ODBC, além da referência tradicional. |
| &nbsp; " | [Apêndices](../odbc/reference/appendixes/index.md)    | Tabelas de transição de estado, biblioteca de cursores ODBC e muito mais. |
| &nbsp; " | [Desenvolver aplicativo](../odbc/reference/develop-app/index.md)  | Funções, identificadores e muito mais. |
| &nbsp; " | [Driver do desenvolvedor](../odbc/reference/develop-driver/index.md) | Como desenvolver seu próprio driver ODBC, se você tiver uma fonte de dados especializada. |
| &nbsp; " | [Instalar](../odbc/reference/install/index.md) | Instalação do ODBC, subchaves e muito mais. |
| &nbsp; " | [Sintaxe](../odbc/reference/syntax/index.md)   | APIs para instalação, instalador, tradução e acesso a dados. |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![Logotipo do PHP][image-ref-360-php] PHP

Você pode usar o PHP para interagir com SQL Server. A raiz de nossa documentação do PHP está [aqui](./php/index.md).

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Prova de conceito da conexão ao SQL usando PHP](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | Um pequeno exemplo de código focado na conexão e na consulta de SQL Server. |
| [Conectar-se de forma resiliente ao SQL com PHP](./php/step-4-connect-resiliently-to-sql-with-php.md) | Lógica de repetição em um exemplo de código, porque as conexões por meio da Internet e da nuvem podem ocasionalmente sofrer momentos de perda de conectividade. |
| [Banco de dados SQL do Azure: usar PHP para consultar](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Exemplo de banco de dados SQL do Azure. |
| [Criar aplicativos PHP para usar o SQL Server no RHEL](https://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | Informações de configuração, juntamente com exemplos de código. |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Logotipo do Python][image-ref-370-python] Python


Você pode usar o Python para interagir com SQL Server.

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Prova de conceito conectando-se ao SQL com Python usando o pyodbc](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | Um pequeno exemplo de código focado na conexão e na consulta de SQL Server. |
| [Banco de dados SQL do Azure: usar o Python para consultar](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Exemplo de banco de dados SQL do Azure. |
| [Criar aplicativos PHP para usar o SQL Server no SLES](https://www.microsoft.com/sql-server/developer-get-started/python/sles/) | Informações de configuração, juntamente com exemplos de código. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentação

| Área | Descrição |
| :--- | :---------- |
| [Python para SQL Server](./python/index.md) | Raiz da nossa documentação. |
| [pymssql driver](./python/pymssql/index.md) | A Microsoft não mantém nem testa o driver pymssql.<br /><br />O driver de conexão pymssql é uma interface simples para bancos de dados SQL, para uso em programas Python. O Pymssql baseia-se na FreeTDS para fornecer uma interface Python DB-API (PEP-249) para Microsoft SQL Server. |
| [driver pyodbc](./python/pyodbc/index.md)   | O driver de conexão pyodbc é um módulo python de software livre que torna o acesso a bancos de dados ODBC simples. Ele implementa a especificação do DB API 2,0, mas é fornecido com ainda mais conveniência Python. |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Logotipo do Ruby][image-ref-380-ruby] Ruby

Você pode usar o Ruby para interagir com SQL Server. A raiz de nossa documentação do Ruby está [aqui](./ruby/index.md).

#### <a name="code-examples"></a>Exemplos de código

|||
| :-- | :-- |
| [Prova de conceito da conexão ao SQL usando Ruby](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | Um pequeno exemplo de código focado na conexão e na consulta de SQL Server. |
| [Banco de dados SQL do Azure: usar Ruby para consultar](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Exemplo de banco de dados SQL do Azure. |
| [Criar aplicativos Ruby para usar o SQL Server no MacOS](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | Informações de configuração, juntamente com exemplos de código. |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpswwwmicrosoftcomsql-serverdeveloper-get-started"></a>[Site Build-a-App, para desenvolvimento de cliente SQL](https://www.microsoft.com/sql-server/developer-get-started/)


Em nossas páginas da Web [*Build-a-app*](https://www.microsoft.com/sql-server/developer-get-started/) , você pode escolher uma longa lista de linguagens de programação para se conectar a SQL Server. E seu programa cliente pode executar uma variedade de sistemas operacionais.

O *Build-a-app* enfatiza a simplicidade e a integridade do desenvolvedor que está começando a começar. As etapas explicam as seguintes tarefas:

1. Como instalar o Microsoft SQL Server
2. Como baixar e instalar ferramentas e drivers.
3. Como fazer as configurações necessárias, conforme apropriado para o sistema operacional escolhido.
4. Como compilar o código-fonte fornecido.
5. Como executar o programa.

A seguir estão algumas estruturas aproximadas dos detalhes fornecidos no site:

#### <a name="java-on-ubuntu"></a>Java no Ubuntu:

1. Configurar seu ambiente
    - Etapa 1.1 Instalar o SQL Server
    - Etapa 1,2 instalar o Java
    - Etapa 1,3 instalar o Java Development Kit (JDK)
    - Etapa 1,4 instalar o Maven
2. Criar aplicativo Java com SQL Server
    - Etapa 2,1 criar um aplicativo Java que se conecta ao SQL Server e executa consultas
    - Etapa 2,2 criar um aplicativo Java que se conecta a SQL Server usando a estrutura popular de hibernação
3. Torne seu aplicativo Java 100x mais rápido
    - Etapa 3,1 criar um aplicativo Java para demonstrar índices Columnstore

#### <a name="python-on-windows"></a>Python no Windows:

1. Configurar seu ambiente
    - Etapa 1.1 Instalar o SQL Server
    - Etapa 1,2 instalar Python
    - Etapa 1,3 instalar o driver ODBC e o utilitário de linha de comando do SQL para SQL Server
2. Criar um aplicativo Python com o SQL Server
    - Etapa 2,1 instalar o driver Python para SQL Server
    - Etapa 2,2 criar um banco de dados para seu aplicativo
    - Etapa 2,3 criar um aplicativo Python que se conecta ao SQL Server e executa consultas
3. Torne seu aplicativo Python 100x mais rápido
    - Etapa 3,1 criar uma nova tabela com 5 milhões usando sqlcmd
    - Etapa 3,2 criar um aplicativo Python que consulta essa tabela e mede o tempo gasto
    - Etapa 3,3 medir quanto tempo leva para executar a consulta
    - Etapa 3,4 adicionar um índice columnstore à sua tabela
    - Etapa 3,5 medir quanto tempo leva para executar a consulta com um índice columnstore

As capturas de tela a seguir dão uma ideia do que é o nosso site de documentação de desenvolvimento do SQL.

#### <a name="choose-a-language"></a>Escolha um idioma:

![Site de desenvolvimento do SQL, introdução][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>Escolha um sistema operacional:

![Site SQL Dev, Java Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>Outro desenvolvimento


Esta seção fornece links sobre outras opções de desenvolvimento. Isso inclui o uso dessas mesmas linguagens para o desenvolvimento do Azure em geral. As informações vão além do direcionamento apenas ao banco de dados SQL do Azure e Microsoft SQL Server.

#### <a name="developer-hub-for-azure"></a>Hub de desenvolvedor para o Azure

- [Hub de desenvolvedor para o Azure](https://docs.microsoft.com/azure/)
- [Azure para desenvolvedores do .NET](https://docs.microsoft.com/dotnet/azure/)
- [Azure para desenvolvedores Java](https://docs.microsoft.com/java/azure/)
- [Azure para desenvolvedores do node. js](https://docs.microsoft.com/nodejs/azure/)
- [Azure para desenvolvedores de Python](https://docs.microsoft.com/python/azure/)
- [Criar um aplicativo Web PHP no Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>Outros idiomas

- [Criar aplicativos go usando o SQL Server no Windows](https://www.microsoft.com/sql-server/developer-get-started/go/windows/)



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

