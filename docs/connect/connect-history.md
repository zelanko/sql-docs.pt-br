---
title: Histórico de driver do Microsoft SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 5/4/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
manager: kenvh
ms.openlocfilehash: 2f2f4bafe48018da5c6f634b272a540021fd4ca2
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34236027"
---
# <a name="driver-history-for-microsoft-sql-server"></a>Histórico de driver do Microsoft SQL Server

Esta página descreve as tecnologias de conexão de dados históricos da Microsoft para se conectar ao SQL Server.

## <a name="odbc"></a>ODBC

Há três gerações distintas dos drivers ODBC da Microsoft para SQL Server. O driver ODBC "SQL Server" primeira ainda seja fornecido como parte do [Windows Data Access Components](#microsoft-or-windows-data-access-components). Não é recomendável usar esse driver para novo desenvolvimento. A partir do SQL Server 2005, o [SQL Server Native Client](#sql-server-native-client) inclui uma interface ODBC e o driver ODBC fornecido com o SQL Server 2005 por meio do SQL Server 2012. Não é recomendável usar esse driver para novo desenvolvimento. Após o SQL Server 2012, o [Microsoft ODBC Driver para SQL Server](#microsoft-odbc-driver-for-sql-server) é o driver é atualizado com os recursos de servidor mais recentes no futuro.

### <a name="sql-server-native-client"></a>SQL Server Native Client

SQL Server Native Client é uma biblioteca autônoma que é usada para OLE DB e ODBC. SQL Server Native Client (SNAC muitas vezes abreviado) foi incluído no SQL Server 2005 por meio de 2012. SQL Server Native Client pode ser usado para aplicativos que precisam aproveitar os novos recursos introduzidos no SQL Server 2005 por meio do SQL Server 2012. (Microsoft/Windows Data Access Components não são atualizadas para esses novos recursos no SQL Server.) Novos recursos além do SQL Server 2012, SQL Server Native Client não será atualizado. Alterne para o Microsoft ODBC Driver para SQL Server ou o Driver OLE DB do Microsoft SQL Server se você quiser tirar proveito dos novos recursos do SQL Server no futuro.

Para obter a documentação completa do SQL Server Native Client, consulte o [documentação do SQL Server Native Client](../relational-databases/native-client/sql-server-native-client-programming.md).

### <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

Após o SQL Server 2012, o driver ODBC principal para o SQL Server foi desenvolvido e lançado como o Microsoft ODBC Driver para SQL Server. Para obter mais informações, consulte o [Microsoft ODBC Driver para a documentação do SQL Server](./odbc/microsoft-odbc-driver-for-sql-server.md).

## <a name="ole-db"></a>OLE DB

Há três gerações distintas do provedor Microsoft OLE DB para SQL Server. O primeiro "Microsoft OLE DB Provider para SQL Server" (SQLOLEDB) ainda é fornecido como parte do [Windows Data Access Components](#microsoft-or-windows-data-access-components). Este provedor não será atualizado com novos recursos e não é recomendável usar esse driver para novo desenvolvimento. A partir do SQL Server 2005, o [SQL Server Native Client](#sql-server-native-client) inclui uma interface de provedor do OLE DB (SQLNCLI) e é o provedor OLE DB que acompanha o SQL Server 2005 por meio de 2017 do SQL Server. Foi [anunciados como substituídos no 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) e não é recomendável usar esse driver para novo desenvolvimento. Em 2017, a tecnologia de acesso de dados do OLE DB foi subsequentemente [undeprecated e uma nova versão planejada foi anunciada](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) para 2018. O novo provedor de OLE DB é chamado de "Microsoft OLE DB Driver para SQL Server" (MSOLEDBSQL) e no momento é mantido e suporte.

## <a name="adonet"></a>ADO.NET

ADO.NET foi introduzido com o Microsoft .NET Framework e continua a ser aprimorado e mantidas. É um componente principal do Microsoft .NET Framework. Para obter mais informações, consulte [Microsoft ADO.NET para o SQL Server](ado-net/microsoft-ado-net-for-sql-server.md).

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver para SQL Server

O Microsoft JDBC Driver para SQL Server introduzida em 2000, continua a ser aprimorado e mantidas. Foi originado de abertura de 2016. Para obter as informações mais recentes, incluindo como baixar o driver, consulte [visão geral do Driver JDBC](./jdbc/overview-of-the-jdbc-driver.md).

## <a name="php"></a>PHP

### <a name="microsoft-drivers-for-php-for-sql-server"></a>Drivers da Microsoft para PHP para SQL Server

Os Drivers da Microsoft para PHP para SQL Server introduzida em 2009 como um projeto de código-fonte aberto, continuar a ser aprimorado e mantidas. Para obter as informações mais recentes, incluindo como baixar o driver do PHP, consulte [Drivers da Microsoft para PHP para SQL Server](./php/microsoft-php-driver-for-sql-server.md).

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>Driver da Microsoft para Node.js para SQL Server

O Driver da Microsoft para Node.js para SQL Server permite que aplicativos Node.js no Microsoft Windows e Microsoft Windows Azure acessar o Microsoft SQL Server e Microsoft Windows Azure SQL Database. Os esforços de desenvolvimento não estão sendo concentrados neste driver. Não é recomendável para criar novos aplicativos usando o Driver da Microsoft para Node.js para SQL Server.

Para obter mais informações sobre o Driver da Microsoft para Node.js para SQL Server, consulte [WindowsAzure / nó sqlserver](https://github.com/Azure/node-sqlserver).

### <a name="tedious"></a>Entediante

A Microsoft atualmente contribui para e suporta o módulo de código-fonte aberto entediante em Node. js à conectividade com o SQL Server usando JavaScript. Para obter mais informações, consulte [Node. js Driver para SQL Server](./node-js/node-js-driver-for-sql-server.md).

## <a name="microsoft-or-windows-data-access-components"></a>Microsoft ou Windows Data Access Components

Microsoft/Windows Data Access Components (MDAC/WDAC) são fornecidos com e com suporte do Windows para o aplicativo com versões anteriores compatibilidade e não fazem parte da pilha de tecnologia do SQL Server atual. Nenhum recurso novo será adicionado aos componentes de MDAC/WDAC e não é recomendável usá-los para o desenvolvimento de novos aplicativos.

Para os fins deste documento, você pode dividir a pilha do MDAC/WDAC nos seguintes componentes, com base em produtos e tecnologia:

* **ADO** (incluindo ADOMD e ADOX)
* **OLE DB** (incluindo o OLE DB Core Services, OLE DB provedor do SQL Server, Oracle OLE DB Provider, provedor OLE DB para Drivers ODBC, o provedor de dados de forma e o provedor de dados remoto)
* **ODBC** (incluindo o Gerenciador de Driver ODBC, o Driver ODBC do SQL e o Driver ODBC do Oracle)

### <a name="mdacwdac-components"></a>Componentes do MDAC/WDAC

MDAC/WDAC inclui os seguintes componentes:

* **ODBC:** a interface do Microsoft ODBC Open Database Connectivity () é uma interface de linguagem de programação C que permite que aplicativos acessem dados de uma variedade de sistemas de gerenciamento de banco de dados (DBMS). Aplicativos que usam essa API são limitados a acessar apenas fontes de dados relacionais.
* **OLE DB:** OLE DB é um conjunto de interfaces para acessar dados em uma variedade de armazenamentos de dados. Existem provedores de OLE DB para acessar dados em bancos de dados, sistemas de arquivos, repositórios de mensagens, serviços de diretório, fluxo de trabalho e repositórios de documento.
* **ADO:** ActiveX Data Objects (ADO) fornece um modelo de programação de alto nível. Embora um pouco menos funcionais que codificar diretamente para OLE DB ou ODBC, ADO é simples de aprender e usar. Ele pode ser usado em linguagens de script, como Microsoft Visual Basic Scripting Edition (VBScript) ou Microsoft JScript.
* **ADOMD:** multidimensional ADO (ADOMD) é usada com provedores de dados multidimensionais, como o provedor do Microsoft OLAP, também conhecido como Microsoft provedor do Analysis Services. Nenhum aprimoramentos importantes foram feitos a ele desde o MDAC 2.0.
* **ADOX:** ADO Extensions for DDL and Security (ADOX) permitem a criação e modificação de definições de um banco de dados, tabela, índice ou procedimento armazenado. Você pode usar ADOX com qualquer provedor. O Microsoft Jet OLE DB Provider fornece suporte completo para ADOX, enquanto o Microsoft SQL Server OLE DB Provider fornece suporte limitado.
* **Bibliotecas de rede do Microsoft SQL Server:** as bibliotecas de rede do SQL Server permitir SQLOLEDB e SQLODBC para se comunicar com o banco de dados do SQL Server. As seguintes bibliotecas de rede do SQL Server foram preteridas em versões do MDAC/WDAC: Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet e RPC. TCP/IP e Pipes nomeados continuarão a ter suporte e estão disponíveis no sistema de operacional Windows de 64 bits.
* **MSDASQL:** o Microsoft OLE DB Provider para ODBC (MSDASQL) permite que os aplicativos que são criados no OLE DB e ADO (que usa internamente OLEDB) para acessar fontes de dados por meio de um driver ODBC. MSDASQL é um provedor OLE DB que se conecta ao ODBC, em vez de um banco de dados. Ele destina-se como uma ponte do OLE DB para um driver ODBC quando não existe nenhum provedor OLE DB direta para uma fonte de dados. MSDASQL fornecido com o sistema operacional Windows e Windows Server 2008 e Vista SP1 foram que a primeira versões para incluir uma versão de 64 bits da tecnologia.

### <a name="deprecated-mdacwdac-components"></a>Componentes do MDAC/WDAC preteridos

Esses componentes ainda têm suporte na versão atual do MDAC/WDAC, mas eles podem ser removidos em versões futuras. Ao desenvolver novos aplicativos, a Microsoft recomenda que você evite usar esses componentes. Além disso, quando você atualiza ou modifica os aplicativos existentes, remova qualquer dependência nesses componentes.

* **SQLOLEDB:** o Microsoft OLE DB Provider para SQL Server (SQLOLEDB), que dá suporte ao acesso ao Microsoft SQL Server, foi preterido. A conectividade para versões futuras do SQL Server pode não ter suporte. A capacidade de se conectar a versões anteriores ao SQL Server 7 será removida do sistema operacional após o Windows 7. Novos aplicativos devem usar o Driver do Microsoft OLE DB para SQL Server (MSOLEDBSQL), que dá suporte a novos recursos do SQL Server. Aplicativos existentes devem migrar para o Driver OLE DB da Microsoft para SQL Server também para melhor desempenho, confiabilidade e capacidade de suporte. Para obter mais informações, consulte [atualizando um aplicativo para o Driver do OLE DB para SQL Server do MDAC](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).
* **SQLODBC:** o Microsoft SQL Server ODBC Driver (SQLODBC), que dá suporte ao acesso ao Microsoft SQL Server, foi preterido. A conectividade para versões futuras do SQL Server pode não ter suporte. A capacidade de se conectar a versões anteriores ao SQL Server 7 será removida do sistema operacional após o Windows 7. Novos aplicativos devem usar o Microsoft ODBC Driver for SQL Server no Windows, que dá suporte a novos recursos do SQL Server. Aplicativos existentes devem migrar para o Microsoft ODBC Driver para SQL Server também para melhor desempenho, confiabilidade e capacidade de suporte. Para obter informações relevantes, consulte [atualizando um aplicativo para o SQL Server Native Client do MDAC](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).
* **Mecanismo de banco de dados Microsoft Jet 4.0:** a partir da versão 2.6, MDAC não possui mais componentes do Jet. Em outras palavras, o MDAC 2.8, 2.6 e 2.7 não contêm Microsoft Jet, o Microsoft Jet OLE DB Provider, o ODBC Drivers de banco de dados de área de trabalho ou objetos de acesso a dados Jet (DAO). Os componentes do mecanismo de banco de dados Microsoft Jet 4.0 entrou em um estado de substituição funcional e mantida engenharia e não receberam aprimoramentos do nível desde se tornando uma parte do Microsoft Windows no Windows 2000.

  Não há nenhuma versão de 64 bits do mecanismo de banco de dados Jet, o Driver do Jet OLEDB, os Drivers de ODBC Jet ou Jet DAO disponível. Para obter mais informações, consulte [artigo 957570](http://support.microsoft.com/kb/957570). Em versões de 64 bits do Windows, o Jet de 32 bits é executado sob o subsistema Windows WOW64. Para obter mais informações sobre WOW64, consulte o [documentação MSDN WOW64](https://msdn.microsoft.com/library/windows/desktop/aa384274(v=vs.85).aspx). Aplicativos nativos de 64 bits não podem se comunicar com os drivers de Jet de 32 bits em execução no WOW64.

  Em vez do Microsoft Jet, a Microsoft recomenda usar [Microsoft SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express) ao novo, desenvolver aplicativos não - Microsoft Access que exigem um repositório de dados relacional. Esses aplicativos novos ou convertidos do Jet podem continuar a usar o Jet com a intenção de usar o Microsoft Office 2003 e anteriores arquivos (. mdb e. xls) para o armazenamento de dados não primária. No entanto, para esses aplicativos, você deve planejar a migração do Jet para o Driver do sistema Office 2007. Você pode [baixar o 2007 Office System Driver](https://www.microsoft.com/downloads/details.aspx?displaylang=en&FamilyID=7554f536-8c28-4598-9b72-ef94e038c891), que permite que você ler e gravar em arquivos já existentes no Office 2003 (. mdb e. xls) ou os formatos de arquivo do Office 2007 (*. accdb, xlsm, xlsx e *.xlsb).

  > [!IMPORTANT]
  > Leia o contrato de licença de usuário final do 2007 Office System para limitações de uso específicos.

  > [!NOTE]
  > Aplicativos do SQL Server também pode acessar o sistema Office 2007 e anterior, arquivos de conectividade de dados heterogêneos do SQL Server e serviços de integração, recursos por meio do Driver do sistema Office 2007. Além disso, os aplicativos do SQL Server de 64 bits podem acessar Jet de 32 bits e arquivos do sistema Office 2007 por meio de 32 bits SQL Server Integration Services (SSIS) no Windows de 64 bits.

* **MSDADS:** com o Microsoft OLE DB Provider para dados de formatação (MSDADS), você pode criar relações hierárquicas entre chaves, campos ou conjuntos de linhas em um aplicativo. Nenhum dos principais recursos aprimoramentos foram feitos desde o MDAC 2.1. Este provedor foi preterido. A Microsoft recomenda que você use o XML, em vez de MSDADS.
* **Oracle, ODBC e OLE DB Oracle:** o Microsoft Driver ODBC do Oracle (Oracle ODBC) e o Microsoft OLE DB Provider for Oracle (Oracle OLE DB) fornecem acesso a servidores de banco de dados Oracle. Eles são criados usando Oracle Call Interface (OCI) versão 7 e oferecem suporte completo para o Oracle 7. Além disso, ele usa emulação Oracle 7 para fornecer suporte limitado para bancos de dados Oracle 8. Oracle não dá suporte a aplicativos que usam OCI versão 7 chamadas. Essas tecnologias são preteridas. Se você estiver usando fontes de dados Oracle, você deve migrar para o provedor e driver fornecido pela Oracle.
* **RDS:** serviços de dados remota (RDS) é um mecanismo Microsoft proprietário para acessar objetos de conjunto de registros ADO remotos pela Internet ou Intranet. RDS é preterido; Nenhum aprimoramentos importantes foram feitos ao RDS desde MDAC 2.1. A Microsoft lançou o .NET Framework, que tem recursos abrangentes de SOAP e substitui os componentes RDS. Todos os componentes de servidor RDS serão removidos do sistema operacional após o Windows 7.
* **JRO:** Jet Replication Objects (JRO) foi preterido. JRO é usado no ADO com Jet (*. mdb) bancos de dados para criar e compactar bancos de dados Jet (do. mdb) e executar o gerenciamento de replicação do Jet. MDAC 2.7 será sua última versão. JRO não estará disponível no sistema de operacional Windows de 64 bits. Não há suporte para JRO no formato de arquivo do Microsoft Access 2007 (*. accdb).
* **Suporte de ODBC de 16 bits:** se você estiver usando aplicativos de 16 bits, você deve migrar para um aplicativo de 32 bits. funcionalidade de 16-bit foi preterida e está sendo removida do sistemas operacionais de 64 bits. Para obter mais informações, consulte [artigo da base de dados de Conhecimento 896458](http://support.microsoft.com/kb/896458).
* **Provedor de OLE DB simples (MSDAOSP):** provedor de OLE DB simples oferece uma estrutura para a criação rápida de provedores OLE DB em dados simples. MSDAOSP foi preterido.
* **Biblioteca de cursores ODBC:** biblioteca de cursores ODBC (ODBCCR32.dll) fornece os cursores de dados limitada do lado do cliente. Biblioteca de cursores ODBC foi preterida; seu aplicativo pode usar implementações de cursor do lado do servidor como uma substituição.
* **OLE DB fora do processo Interface Remoting:** remoto da Interface OLE DB (msdaps.dll) foi feita uma tentativa para permitir que os provedores OLE DB para execução fora do processo. Comunicação remota do OLEDB Interface fora do processo foi preterida.
* **AppleTalk e bibliotecas de rede Banyan Vines SQL:** o Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet e RPC SQL bibliotecas de rede são preteridas. Se você estiver usando qualquer uma dessas tecnologias, você deve modificar seus aplicativos para usar uma das outras bibliotecas de rede, como TCP/IP e o Pipe nomeado.

### <a name="mdacwdac-releases"></a>Versões do MDAC/WDAC

Aqui está uma lista dos cenários de suporte de versões anteriores do MDAC/WDAC, começando com o mais recente.

* **O MDAC 1.5, MDAC 2.0 e 2.1 do MDAC:** nessas versões do MDAC foram independentes versões lançadas por meio do Microsoft Windows NT Option Pack, SDK da plataforma Microsoft Windows ou site do MDAC. Não há suporte para essas versões do MDAC.
* **MDAC 2.5:** nesta versão do MDAC foi incluída com o sistema operacional Windows 2000. Service packs do MDAC 2.5 foram incluídos com os service packs do Windows 2000 correspondentes.
* **MDAC 2.6:** MDAC 2.6 RTM, SP1 e SP2 foram incluídos com o Microsoft SQL Server 2000 RTM, SP1 e SP2, respectivamente. Além disso, esses pacotes de serviço do MDAC foram lançadas para o site do MDAC acordo com a agenda de versão de service pack do Microsoft SQL Server 2000. Você pode instalar esta versão do MDAC e seus pacotes de serviço em plataformas Windows 2000, Windows Millennium Edition, Windows NT, Windows 95 e Windows 98. Esta versão do MDAC não é suportada.
* **MDAC 2.7:** nesta versão do MDAC foi incluída com os sistemas operacionais Microsoft Windows XP RTM e SP1. Você pode instalar esta versão do MDAC e seus pacotes de serviço em plataformas Windows 2000, Windows Millennium, Windows NT e Windows 98. Você pode instalar esta versão na plataforma Windows XP apenas por meio de seus pacotes de serviços ou de sistema operacional. Esta versão do MDAC não é suportada.
* **MDAC 2.8:** nesta versão do MDAC foi incluído no Windows Server 2003 e Windows XP SP2 e posterior. Você também pode instalar esta versão do MDAC e seus pacotes de serviço no Windows 2000.

  * A versão de 32 bits do MDAC 2.8 também foi liberada para o site do MDAC ao mesmo tempo que o Windows Server 2003 foi lançado para o cliente.
  * A versão de 64 bits do MDAC 2.8 foi liberada com a versão de 64 bits do Windows Server 2003 e Windows XP.

* **Windows Data Access Components (WDAC):** MDAC trocou o nome para WDAC - "Windows Data Access Components" começando com o Windows Vista e Windows Server 2008. WDAC é incluído como parte do sistema operacional e não está disponível separadamente para redistribuição. Facilidade de manutenção para WDAC está sujeito ao ciclo de vida do sistema operacional.

  versões de 32 bits e 64 bits do WDAC são lançadas com as versões de 32 bits e 64 bits dos sistemas operacionais Windows, respectivamente.

## <a name="obsolete-data-access-technologies"></a>Tecnologias de acesso a dados obsoletos

Obsoletas tecnologias são tecnologias que não foram aprimorados ou atualizados em diversas versões do produto e que serão excluídos de versões futuras do produto. Não use essas tecnologias ao criar novos aplicativos. Ao modificar aplicativos existentes que são escritos usando essas tecnologias, considere migrar esses aplicativos para o ADO.NET ou outra tecnologia atual.

Os seguintes componentes são considerados obsoletos:

* **Biblioteca de banco de dados:** DB-Library é um modelo de programação específicas do SQL Server que inclui APIs de C. Não houve nenhuma melhorias de recurso na biblioteca de banco de dados desde o SQL Server 6.5. Versão final foi com o SQL Server 2000, e não será ser movido para o sistema de operacional do Windows de 64 bits.
* **Embedded SQL (E-SQL):** SQL E é um modelo de programação específicas do SQL Server que permite que as instruções de Transact-SQL a ser inserido no código do Visual C#. Não foram feitas melhorias nenhum recurso para o SQL E desde o SQL Server 6.5. Versão final foi com o SQL Server 2000, e não será ser movido para o sistema de operacional do Windows de 64 bits.
* **Objetos de acesso de dados (DAO):** DAO fornece acesso aos bancos de dados JET (acesso). Esta API pode ser usada do Microsoft Visual Basic, Microsoft Visual C++ e linguagens de script. Ele foi incluído no Microsoft Office 2000 e Office XP. DAO 3.6 é a versão final dessa tecnologia. Ele não estará disponível no sistema de operacional Windows de 64 bits.
* **Objetos de dados remotos (RDO):** RDO foi projetado especificamente para acessar fontes de dados relacionais remotos do ODBC e para facilitar a usar o ODBC sem código de aplicativo complexo. Ele foi incluído no Microsoft Visual Basic versões 4, 5 e 6. RDO versão 2.0 foi a versão final dessa tecnologia.