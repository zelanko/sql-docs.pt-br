---
title: Histórico do driver para Microsoft SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 05936a9555cacfc88c9219e19bc57772109ed047
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957519"
---
# <a name="driver-history-for-microsoft-sql-server"></a>Histórico do driver para Microsoft SQL Server

Esta página descreve as tecnologias de conexão de dados históricas da Microsoft para se conectar a SQL Server.

## <a name="odbc"></a>ODBC

Há três gerações distintas de drivers ODBC da Microsoft para SQL Server. O primeiro driver ODBC "SQL Server" ainda é fornecido como parte dos [componentes de acesso a dados do Windows](#microsoft-or-windows-data-access-components). Não é recomendável usar este driver para um novo desenvolvimento. A partir do SQL Server 2005, o [SQL Server Native Client](#sql-server-native-client) inclui uma interface ODBC e é o driver ODBC fornecido com SQL Server 2005 até SQL Server 2012. Não é recomendável usar este driver para um novo desenvolvimento. Após SQL Server 2012, o [Microsoft ODBC driver for SQL Server](#microsoft-odbc-driver-for-sql-server) é o driver que é atualizado com os recursos mais recentes do servidor no futuro.

### <a name="sql-server-native-client"></a>SQL Server Native Client

SQL Server Native Client é uma biblioteca autônoma que é usada para OLE DB e ODBC. SQL Server Native Client (frequentemente abreviado SNAC) foi incluído em SQL Server 2005 até 2012. SQL Server Native Client pode ser usado para aplicativos que precisam aproveitar os novos recursos introduzidos no SQL Server 2005 até SQL Server 2012. (Os componentes de acesso a dados do Microsoft/Windows não são atualizados para esses novos recursos no SQL Server.) Para novos recursos além do SQL Server 2012, o SQL Server Native Client não será atualizado. Alterne para o Microsoft ODBC Driver for SQL Server ou o driver do Microsoft OLE DB para SQL Server se você quiser aproveitar os novos recursos do SQL Server no futuro.

Para obter a documentação completa do SQL Server Native Client, consulte a [documentação do SQL Server Native Client](../relational-databases/native-client/sql-server-native-client-programming.md).

### <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

Após SQL Server 2012, o driver ODBC primário para SQL Server foi desenvolvido e liberado como o Microsoft ODBC Driver for SQL Server. Para obter mais informações, consulte a [documentação do Microsoft ODBC driver for SQL Server](./odbc/microsoft-odbc-driver-for-sql-server.md).

## <a name="ole-db"></a>OLE DB

Há três gerações distintas de provedores Microsoft OLE DB para SQL Server. O primeiro "Microsoft OLE DB Provider para SQL Server" (SQLOLEDB) ainda é fornecido como parte do [Windows Data Access Components](#microsoft-or-windows-data-access-components). Este provedor não será atualizado com novos recursos e não é recomendável usar este driver para um novo desenvolvimento. A partir do SQL Server 2005, a [SQL Server Native Client](#sql-server-native-client) inclui uma interface de provedor de OLE DB (sqlncli) e é o provedor de OLE DB fornecido com SQL Server 2005 até SQL Server 2017. Foi [anunciado como preterido em 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) e não é mais mantido, não sendo recomendável usar esse driver para um novo desenvolvimento. Em 2017, a tecnologia de acesso a dados OLE DB foi subseqüentemente [não preterida e uma nova versão planejada foi anunciada](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) para 2018. O novo provedor de OLE DB é chamado de "Microsoft OLE DB driver for SQL Server" (MSOLEDBSQL) e é atualmente mantido e tem suporte.

## <a name="adonet"></a>ADO.NET

O ADO.NET foi introduzido com a estrutura de Microsoft .NET e continua a ser melhorado e mantido. É um componente fundamental da estrutura de Microsoft .NET. Para obter mais informações, consulte [Microsoft ADO.NET for SQL Server](ado-net/microsoft-ado-net-for-sql-server.md).

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver para SQL Server

Introduzido no 2000, o Microsoft JDBC Driver para SQL Server continua a ser melhorado e mantido. Ele foi aberto de origem em 2016. Para obter as informações mais recentes, incluindo como baixar o driver, consulte [visão geral do driver JDBC](./jdbc/overview-of-the-jdbc-driver.md).

## <a name="php"></a>PHP

### <a name="microsoft-drivers-for-php-for-sql-server"></a>Drivers da Microsoft para PHP para SQL Server

Introduzido no 2009 como um projeto de software livre, os drivers da Microsoft para PHP para SQL Server continuam a ser aprimorados e mantidos. Para obter as informações mais recentes, incluindo como baixar o driver PHP, consulte [drivers da Microsoft para PHP para SQL Server](./php/microsoft-php-driver-for-sql-server.md).

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>Driver da Microsoft para node. js para SQL Server

O driver da Microsoft para node. js para SQL Server permite que aplicativos node. js no Microsoft Windows e no Microsoft Windows Azure acessem o Microsoft SQL Server e o banco de dados SQL do Microsoft Windows Azure. Os esforços de desenvolvimento não estão mais concentrados neste driver. Não é recomendável criar novos aplicativos usando o driver da Microsoft para node. js para SQL Server.

Para obter mais informações sobre o driver da Microsoft para node. js para SQL Server, consulte [WindowsAzure/node-SqlServer](https://github.com/Azure/node-sqlserver).

### <a name="tedious"></a>Enfadonho

A Microsoft atualmente contribui e dá suporte ao módulo entediante de software livre no node. js para conectividade com SQL Server usando JavaScript. Para obter mais informações, consulte [Driver node. js para SQL Server](./node-js/node-js-driver-for-sql-server.md).

## <a name="microsoft-or-windows-data-access-components"></a>Componentes de acesso a dados da Microsoft ou do Windows

Os Microsoft/Windows Data Access Components (MDAC/WDAC) são fornecidos com o Windows para compatibilidade com versões anteriores de aplicativos e não fazem parte da pilha de tecnologia de SQL Server atual. Nenhum novo recurso será adicionado aos componentes no MDAC/WDAC e não é recomendável usá-los para o desenvolvimento de novos aplicativos.

Para os fins deste documento, você pode dividir a pilha do MDAC/WDAC nos seguintes componentes, com base na tecnologia e nos produtos:

* **ADO** (incluindo ADOMD e ADOX)
* **OLE DB** (incluindo OLE DB serviços principais, SQL Server provedor de OLE DB, provedor de OLE DB Oracle, provedor de OLE DB para drivers ODBC, provedor de forma de dados e Provedor de Dados remotos)
* **ODBC** (incluindo o Gerenciador de driver ODBC, o driver ODBC do SQL e o driver ODBC do Oracle)

### <a name="mdacwdac-components"></a>Componentes do MDAC/WDAC

O MDAC/WDAC inclui estes componentes:

* **ODBC:** A interface ODBC (Open Database Connectivity) da Microsoft é uma interface de linguagem de programação C que permite que os aplicativos acessem dados de uma variedade de DBMS (sistemas de gerenciamento de banco de dados). Os aplicativos que usam essa API estão limitados a acessar somente fontes de dados relacionais.
* **OLE DB:** OLE DB é um conjunto de interfaces COM para acessar dados em uma variedade de armazenamentos de dados. Existem provedores de OLE DB para acessar dados em bancos de dado, sistemas de arquivos, armazenamentos de mensagens, serviços de diretório, fluxo de trabalho e repositórios de documentos.
* **ADO:** O ActiveX Data Objects (ADO) fornece um modelo de programação de alto nível. Embora seja um pouco menos eficaz do que codificar para OLE DB ou ODBC diretamente, o ADO é simples de aprender e usar. Ele pode ser usado a partir de linguagens de script, como Microsoft Visual Basic Scripting Edition (VBScript) ou Microsoft JScript.
* **ADOMD.** Multidimensional ADO (ADOMD) deve ser usada com provedores de dados multidimensionais, como o provedor do Microsoft OLAP, também conhecido como Microsoft provedor do Analysis Services. Não foram feitas melhorias de recursos importantes desde o MDAC 2,0.
* **ADOX:** As extensões ADO para DDL e segurança (ADOX) permitem a criação e a modificação de definições de um banco de dados, tabela, índice ou procedimento armazenado. Você pode usar o ADOX com qualquer provedor. O provedor de OLE DB do Microsoft Jet fornece suporte completo para o ADOX, enquanto o provedor de OLE DB de Microsoft SQL Server fornece suporte limitado.
* **Microsoft SQL Server bibliotecas de rede:** O SQL Server bibliotecas de rede permitem SQLOLEDB e SQLODBC para se comunicar com o banco de dados SQL Server. As seguintes SQL Server bibliotecas de rede foram preteridas em versões do MDAC/WDAC: Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet e RPC. O TCP/IP e os pipes nomeados continuarão a ter suporte e estarão disponíveis no sistema operacional Windows de 64 bits.
* **MSDASQL:** O provedor de OLE DB da Microsoft para ODBC (MSDASQL) permite que aplicativos criados em OLE DB e ADO (que usa o OLEDB internamente) acessem fontes de dados por meio de um driver ODBC. MSDASQL é um provedor OLEDB que se conecta ao ODBC, em vez de um banco de dados. Ele se destina como uma ponte de OLE DB para um driver ODBC quando não existe um provedor de OLE DB direto para uma fonte de dados. O MSDASQL é fornecido com o sistema operacional Windows, e o Windows Server 2008 e o Vista SP1 foram as primeiras versões do Windows para incluir uma versão de 64 bits da tecnologia.

### <a name="deprecated-mdacwdac-components"></a>Componentes MDAC/WDAC preteridos

Esses componentes ainda têm suporte na versão atual do MDAC/WDAC, mas podem ser removidos em versões futuras. Ao desenvolver novos aplicativos, a Microsoft recomenda que você evite usar esses componentes. Além disso, ao atualizar ou modificar aplicativos existentes, remova qualquer dependência desses componentes.

* **SQLOLEDB:** O provedor de OLE DB da Microsoft para SQL Server (SQLOLEDB), que dá suporte ao acesso ao Microsoft SQL Server, foi preterido. Sua conectividade com versões futuras do SQL Server pode não ter suporte. A capacidade de se conectar a versões anteriores à SQL Server 7 será removida do sistema operacional após o Windows 7. Os novos aplicativos devem usar o Microsoft OLE DB driver for SQL Server (MSOLEDBSQL), que oferece suporte a novos recursos de SQL Server. Os aplicativos existentes devem migrar para o Microsoft OLE DB driver para SQL Server também para melhorar o desempenho, a confiabilidade e a compatibilidade. Para obter mais informações, consulte [atualizando um aplicativo para OLE DB driver para SQL Server do MDAC](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).
* **SQLODBC:** O driver ODBC Microsoft SQL Server (SQLODBC), que dá suporte ao acesso ao Microsoft SQL Server, foi preterido. Sua conectividade com versões futuras do SQL Server pode não ter suporte. A capacidade de se conectar a versões anteriores à SQL Server 7 será removida do sistema operacional após o Windows 7. Os novos aplicativos devem usar o Microsoft ODBC Driver for SQL Server no Windows, que oferece suporte a novos recursos de SQL Server. Os aplicativos existentes devem migrar para o Microsoft ODBC Driver for SQL Server também para melhorar o desempenho, a confiabilidade e a compatibilidade. Para obter informações relevantes, consulte [atualizando um aplicativo para SQL Server Native Client do MDAC](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).
* **Microsoft Jet Mecanismo de Banco de Dados 4,0:** A partir da versão 2,6, o MDAC não contém mais componentes do Jet. Em outras palavras, o MDAC 2,6, 2,7 e 2,8 não contêm o Microsoft Jet, o provedor de OLE DB do Microsoft Jet, os drivers de banco de dados da área de trabalho do ODBC ou DAO (objetos de acesso ao Data) do Jet. 

  Não há nenhuma versão de 64 bits do Jet Mecanismo de Banco de Dados, o driver OLEDB do Jet, os drivers ODBC Jet ou o Jet DAO disponíveis. Para saber mais, consulte o [artigo da base de dados 957570](https://support.microsoft.com/kb/957570). Nas versões de 64 bits do Windows, o Jet de 32 bits é executado no subsistema WOW64 do Windows. Para obter mais informações sobre o WOW64, consulte a [documentação do WOW64 do MSDN](/windows/desktop/WinProg64/wow64-implementation-details). Os aplicativos nativos de 64 bits não podem se comunicar com os drivers Jet de 32 bits em execução no WOW64.

  Em vez do Microsoft Jet, a Microsoft recomenda usar o [Microsoft SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express) ao desenvolver novos aplicativos de acesso não-Microsoft que exijam um armazenamento de dados relacional. Esses aplicativos Jet novos ou convertidos podem continuar a usar o Jet com a intenção de usar Microsoft Office 2003 e arquivos anteriores (. mdb e. xls) para armazenamento de dados não primário. No entanto, para esses aplicativos, você deve planejar a migração do Jet para o Mecanismo de Banco de Dados do Microsoft Access. Você pode [baixar o Mecanismo de Banco de Dados do Microsoft Access](https://www.microsoft.com/download/details.aspx?id=54920), que permite a leitura e a gravação em arquivos pré-existentes nos formatos de arquivo .mdb e .xls no Office 2003 ou *.accdb, *.xlsm, *.xlsx e *.xlsb no Office 2007.

  > [!IMPORTANT]
  > Leia o contrato de licença de usuário final do 2007 Office System para obter limitações de uso específicas.

  > [!NOTE]
  > SQL Server aplicativos também podem acessar o 2007 Office System e, antes, os arquivos de SQL Server recursos de serviços de integração e integrações de dados heterogêneos também, por meio do driver do sistema do Office 2007. Além disso, os aplicativos de 64 bits SQL Server podem acessar o Jet de 32 bits e os arquivos do sistema Office do 2007 usando o SSIS (32-bit SQL Server Integration Services) no Windows de 64 bits.

* **MSDADS:** Com o Microsoft OLE DB Provider for Data Shaping (MSDADS), você pode criar relações hierárquicas entre chaves, campos ou conjuntos de linhas em um aplicativo. Não foram feitas melhorias de recursos importantes desde o MDAC 2,1. Este provedor foi preterido. A Microsoft recomenda que você use XML, em vez de MSDADS.
* **Oracle ODBC e oracle OLE DB:** O Microsoft Oracle ODBC Driver (Oracle ODBC) e o Provedor Microsoft OLE DB para Oracle (Oracle OLE DB) fornecem acesso a servidores de banco de dados Oracle. Eles são criados usando o Oracle Call interface (OCI) versão 7 e fornecem suporte total ao Oracle 7. Além disso, ele usa a emulação do Oracle 7 para fornecer suporte limitado a bancos de dados Oracle 8. O Oracle não dá mais suporte a aplicativos que usam chamadas de OCI versão 7. Essas tecnologias foram preteridas. Se você estiver usando fontes de dados Oracle, deverá migrar para o driver e o provedor fornecidos pela Oracle.
* **RDS:** O RDS (serviços de dados remotos) é um mecanismo proprietário da Microsoft para acessar objetos do conjunto de registros ADO remoto na Internet ou em uma intranet. O RDS foi preterido; Não foram feitas melhorias de recursos importantes no RDS desde o MDAC 2,1. A Microsoft lançou o .NET Framework, que tem recursos extensos de SOAP e substitui os componentes do RDS. Todos os componentes do servidor RDS serão removidos do sistema operacional após o Windows 7.
* **JRO:** Os objetos de replicação do Jet (JRO) foram preteridos. O JRO é usado no ADO com bancos*de dados Jet (. mdb) para criar e compactar bancos de dados Jet (. mdb) e executar o gerenciamento de replicação do Jet. O MDAC 2,7 será sua última versão. O JRO não estará disponível no sistema operacional Windows de 64 bits. Não há suporte para o JRO no formato de arquivo do Microsoft*Access 2007 (. accdb).
* **suporte a ODBC de 16 bits:** Se você estiver usando aplicativos de 16 bits, deverá migrar para um aplicativo de 32 bits. a funcionalidade de 16 bits foi preterida e está sendo removida dos sistemas operacionais de 64 bits. Para saber mais, consulte o [artigo 896458 da base de dados de conhecimento](https://support.microsoft.com/kb/896458).
* **Provedor simples OleDb (MSDAOSP):** O provedor simples do OLEDB oferece uma estrutura para a criação rápida de provedores de OLE DB sobre dados simples. MSDAOSP foi preterido.
* **Biblioteca de cursores ODBC:** A biblioteca de cursores ODBC (ODBCCR32. dll) fornece cursores de dados limitados do lado do cliente. A biblioteca de cursores ODBC foi preterida; seu aplicativo pode usar implementações de cursor do lado do servidor como uma substituição.
* **OLE DB comunicação remota da interface fora do processo:** A interface de comunicação remota do OLEDB (MSDAPS. dll) foi uma tentativa de permitir que os provedores de OLE DB esgotassem fora do processo. A comunicação remota da interface de fora do processo do OLEDB foi preterida.
* **Bibliotecas de rede do SQL AppleTalk e Banyan Vines:** As bibliotecas de rede Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet e RPC SQL são preteridas. Se você estiver usando qualquer uma dessas tecnologias, deverá modificar seus aplicativos para usar uma das outras bibliotecas de rede, como TCP/IP e pipe nomeado.

### <a name="mdacwdac-releases"></a>Versões do MDAC/WDAC

Aqui está uma lista dos cenários de suporte das versões anteriores do MDAC/WDAC, começando pelo mais cedo.

* **Mdac 1,5, mdac 2,0 e mdac 2,1:** Essas versões do MDAC eram versões independentes que foram lançadas por meio do Microsoft Windows NT Option Pack, do SDK da plataforma Microsoft Windows ou do site do MDAC. Não há mais suporte para essas versões do MDAC.
* **MDAC** Esta versão do MDAC foi incluído com o sistema operacional Windows 2000. Os Service Packs do MDAC 2,5 foram incluídos nos Service Packs do Windows 2000 correspondentes.
* MDAC RTM do **MDAC 2.6**, SP1 e SP2 foram incluídas com o Microsoft SQL Server 2000 RTM, SP1 e SP2, respectivamente. Além disso, esses Service Packs do MDAC foram lançados no site do MDAC de acordo com a agenda de lançamento do Service Pack do Microsoft SQL Server 2000. Você pode instalar esta versão do MDAC e seus Service Packs nas plataformas Windows 2000, Windows Millennium Edition, Windows NT, Windows 95 e Windows 98. Não há mais suporte para esta versão do MDAC.
* **MDAC** Esta versão do MDAC foi incluído com os sistemas operacionais Microsoft Windows XP RTM e SP1. Você pode instalar esta versão do MDAC e seus Service Packs nas plataformas Windows 2000, Windows Millennium, Windows NT e Windows 98. Você pode instalar essa versão na plataforma Windows XP somente por meio do sistema operacional ou seus pacotes de serviços. Não há mais suporte para esta versão do MDAC.
* **MDAC** Esta versão do MDAC foi incluído com o Windows Server 2003 e Windows XP SP2 e posterior. Você também pode instalar esta versão do MDAC e seus service packs no Windows 2000.

  * A versão de 32 bits do MDAC 2,8 também foi lançada no site do MDAC ao mesmo tempo em que o Windows Server 2003 foi lançado para o cliente.
  * A versão de 64 bits do MDAC 2,8 foi lançada com a versão de 64 bits do Windows Server 2003 e Windows XP.

* **Windows Data Access Components (WDAC):** O MDAC alterou seu nome para WDAC-"componentes de acesso a dados do Windows" a partir do Windows Vista e do Windows Server 2008. O WDAC é incluído como parte do sistema operacional e não está disponível separadamente para redistribuição. A manutenção para o WDAC está sujeita ao ciclo de vida do sistema operacional.

  as versões de 32 bits e 64 bits do WDAC são lançadas com as versões de 32 bits e de 64 bits dos sistemas operacionais Windows, respectivamente.

## <a name="obsolete-data-access-technologies"></a>Tecnologias de acesso a dados obsoletas

Tecnologias obsoletas são tecnologias que não foram aprimoradas ou atualizadas em várias versões de produtos e que serão excluídas de futuras versões de produtos. Não use essas tecnologias ao escrever novos aplicativos. Quando você modifica os aplicativos existentes que são gravados usando essas tecnologias, considere migrar esses aplicativos para o ADO.NET ou outra tecnologia atual.

Os seguintes componentes são considerados obsoletos:

* **DB-Library** DB-Library é um modelo de programação específicas do SQL Server que inclui APIs de C. Não houve aprimoramentos de recursos para a biblioteca de banco de dado desde SQL Server 6,5. Sua versão final foi com o SQL Server 2000 e não será portada para o sistema operacional Windows de 64 bits.
* **SQL inserido (E-SQL):** O E-SQL é um modelo de programação específico de SQL Server que permite que as instruções Transact-SQL sejam inseridas no código do Visual C. Nenhum aprimoramento de recurso foi feito no E-SQL desde SQL Server 6,5. Sua versão final foi com o SQL Server 2000 e não será portada para o sistema operacional Windows de 64 bits.
* **DAO (objetos de acesso a dados):** O DAO fornece acesso aos bancos de dados do JET (Access). Essa API pode ser usada no Microsoft Visual Basic, Microsoft Visual C++e linguagens de script. Ele foi incluído com o Microsoft Office 2000 e o Office XP. O DAO 3,6 é a versão final dessa tecnologia. Ele não estará disponível no sistema operacional Windows de 64 bits.
* **Objetos de dados remotos (RDO):** O RDO foi projetado especificamente para acessar fontes de dados relacionais ODBC remotas e tornou mais fácil usar o ODBC sem código de aplicativo complexo. Ele foi incluído com o Microsoft Visual Basic versões 4, 5 e 6. O RDO versão 2,0 foi a versão final desta tecnologia.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
