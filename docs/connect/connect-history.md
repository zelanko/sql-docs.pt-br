---
title: Histórico de driver do Microsoft SQL Server | Microsoft Docs
description: Esta página descreve as tecnologias de conexão de dados históricas da Microsoft para se conectar ao SQL Server.
ms.custom: ''
ms.date: 05/04/2018
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3724e9c616a17e490946888d2acc8c886a57545a
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81529063"
---
# <a name="driver-history-for-microsoft-sql-server"></a>Histórico de driver para o Microsoft SQL Server

Esta página descreve as tecnologias de conexão de dados históricas da Microsoft para se conectar ao SQL Server.

## <a name="odbc"></a>ODBCODBC

Há três gerações distintas de drivers ODBC da Microsoft para SQL Server. O primeiro driver ODBC do "SQL Server" ainda é fornecido como parte dos [Windows Data Access Components](#microsoft-or-windows-data-access-components). Não é recomendável usar esse driver para um novo desenvolvimento. No SQL Server 2005 e em versões posteriores, o [SQL Server Native Client](#sql-server-native-client) inclui uma interface ODBC e é o driver ODBC que era fornecido com o SQL Server da versão 2005 até a 2012. Não é recomendável usar esse driver para um novo desenvolvimento. Em versões do SQL Server posteriores à 2012, o [Microsoft ODBC Driver for SQL Server](#microsoft-odbc-driver-for-sql-server) é o driver que é atualizado com os recursos de servidor mais recentes, orientados a tecnologias futuras.

### <a name="sql-server-native-client"></a>SQL Server Native Client

O SQL Server Native Client é uma biblioteca autônoma usada para o OLE DB e o ODBC. O SQL Server Native Client (frequentemente abreviado como SNAC) foi incluído no SQL Server 2005 e mantido até a versão 2012. O SQL Server Native Client pode ser usado para aplicativos que precisam aproveitar os novos recursos introduzidos nas versões 2005 a 2012 do SQL Server. (Os Microsoft/Windows Data Access Components não são atualizados para esses novos recursos no SQL Server.) Para novos recursos posteriores ao SQL Server 2012, o SQL Server Native Client não será atualizado. Alterne para o Microsoft ODBC Driver for SQL Server ou o Driver do Microsoft OLE DB para SQL Server se você quiser aproveitar os novos recursos do SQL Server no futuro.

Para obter a documentação completa do SQL Server Native Client, confira a [documentação do SQL Server Native Client](../relational-databases/native-client/sql-server-native-client-programming.md).

### <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

Após o SQL Server 2012, o driver ODBC primário para SQL Server foi desenvolvido e liberado como o Microsoft ODBC Driver for SQL Server. Para obter mais informações, confira a [documentação do Microsoft ODBC Driver for SQL Server](./odbc/microsoft-odbc-driver-for-sql-server.md).

## <a name="ole-db"></a>OLE DB

Há três gerações distintas de provedores Microsoft OLE DB para SQL Server. O primeiro "Microsoft OLE DB Provider para SQL Server" (SQLOLEDB) ainda é fornecido como parte do [Windows Data Access Components](#microsoft-or-windows-data-access-components). Esse provedor não será atualizado com novos recursos e não é recomendável usar esse driver para um novo desenvolvimento. No SQL Server 2005 e em versões posteriores, o [SQL Server Native Client](#sql-server-native-client) inclui uma interface do provedor OLE DB (SQLNCLI) e é o provedor OLE DB que era fornecido com o SQL Server da versão 2005 até a 2017. Foi [anunciado como preterido em 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) e não é mais mantido, não sendo recomendável usar esse driver para um novo desenvolvimento. Em 2017, a tecnologia de acesso a dados do OLE DB subsequentemente [deixou de ser preterida e uma nova versão planejada foi anunciada](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) para 2018. O novo provedor OLE DB é chamado "Driver do Microsoft OLE DB para SQL Server (MSOLEDBSQL) e atualmente recebe manutenção e suporte".

## <a name="adonet"></a>ADO.NET

O ADO.NET foi introduzido com o Microsoft .NET Framework e continua a ser aprimorado e mantido. É um componente fundamental do Microsoft .NET Framework. Para obter mais informações, confira [Microsoft ADO.NET for SQL Server](ado-net/microsoft-ado-net-sql-server.md).

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver para SQL Server

Introduzido em 2000, o Microsoft JDBC Driver para SQL Server continua a ser aprimorado e mantido. Em 2016, ele foi transformado em software livre. Para obter as informações mais recentes, incluindo como baixar o driver, confira [Visão geral do JDBC Driver](./jdbc/overview-of-the-jdbc-driver.md).

## <a name="php"></a>PHP

### <a name="microsoft-drivers-for-php-for-sql-server"></a>Drivers da Microsoft para PHP para SQL Server

Introduzido em 2009 como um projeto de software livre, os Drivers da Microsoft para PHP para SQL Server continuam a ser aprimorados e mantidos. Para obter as informações mais recentes, incluindo como baixar o driver PHP, confira [Drivers da Microsoft para PHP para SQL Server](./php/microsoft-php-driver-for-sql-server.md).

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>Driver da Microsoft para Node.js para SQL Server

O Driver da Microsoft para Node.js para SQL Server permite que aplicativos Node.js no Microsoft Windows e no Microsoft Azure acessem o Microsoft SQL Server e o Banco de Dados SQL do Microsoft Azure. Os esforços de desenvolvimento não estão mais concentrados neste driver. Não é recomendável criar aplicativos usando o Driver da Microsoft para Node.js para SQL Server.

Para obter mais informações sobre o Driver da Microsoft para Node.js para SQL Server, confira [WindowsAzure / node-sqlserver](https://github.com/Azure/node-sqlserver).

### <a name="tedious"></a>Tedious

A Microsoft atualmente contribui e dá suporte ao módulo de software livre tedious no Node.js para conectividade com o SQL Server usando JavaScript. Para obter mais informações, confira [Driver do Node.js para SQL Server](./node-js/node-js-driver-for-sql-server.md).

## <a name="microsoft-or-windows-data-access-components"></a>Microsoft ou Windows Data Access Components

Os Microsoft/Windows Data Access Components (MDAC/WDAC) são fornecidos com o Windows para compatibilidade com versões anteriores de aplicativos e não fazem parte da pilha de tecnologia atual do SQL Server. Nenhum novo recurso será adicionado aos componentes no MDAC/WDAC e não é recomendável usá-los para o desenvolvimento de novos aplicativos.

Para os fins deste documento, você pode dividir a pilha do MDAC/WDAC nos seguintes componentes, com base na tecnologia e nos produtos:

* **ADO** (incluindo ADOMD e ADOX)
* **OLE DB** (incluindo Serviços Principais do OLE DB, Provedor OLE DB para SQL Server, Provedor OLE DB Oracle, Provedor OLE DB para Drivers ODBC, Provedor de Forma de Dados e Provedor de Dados Remotos)
* **ODBC** (incluindo o Gerenciador de Driver ODBC, o Driver ODBC do SQL e o Driver ODBC Oracle)

### <a name="mdacwdac-components"></a>Componentes do MDAC/WDAC

O MDAC/WDAC inclui estes componentes:

* **ODBC:** a interface Microsoft ODBC (Open Database Connectivity) é uma interface de linguagem de programação C que permite que os aplicativos acessem dados de uma variedade de DBMS (sistemas de gerenciamento de banco de dados). Os aplicativos que usam essa API estão limitados a acessar somente fontes de dados relacionais.
* **OLE DB:** O OLE DB é um conjunto de interfaces COM para acessar dados em uma variedade de armazenamentos de dados. Existem provedores do OLE DB para acessar dados em bancos de dados, sistemas de arquivos, armazenamentos de mensagens, serviços de diretório, fluxo de trabalho e repositórios de documentos.
* **ADO:** o ADO (ActiveX Data Objects) fornece um modelo de programação de alto nível. Embora apresente desempenho um pouco inferior ao da codificação direta para OLE DB ou ODBC, o ADO é fácil de aprender e usar. Ele pode ser usado em linguagens de script, como o Microsoft JScript ou o Microsoft VBScript (Visual Basic Scripting Edition).
* **ADOMD:** a ADOMD (ADO multidimensional) deve ser usada com provedores de dados multidimensionais, como o provedor do Microsoft OLAP, também conhecido como o Provedor do Microsoft Analysis Services. Nenhum aprimoramento importante de recurso foi feito a ele desde a versão 2.0 do MDAC.
* **ADOX:** o ADOX (extensões do ADO para DDL e segurança) permitem a criação e modificação de definições de um banco de dados, tabela, índice ou procedimento armazenado. Você pode usar o ADOX com qualquer provedor. O Provedor do Microsoft Jet OLE DB dá suporte completo para o ADOX, enquanto o Provedor do Microsoft OLE DB para SQL Server dá suporte limitado.
* **Bibliotecas de Rede do Microsoft SQL Server:** as Bibliotecas de Rede do SQL Server permitem que o SQLOLEDB e o SQLODBC se comuniquem com o banco de dados do SQL Server. As seguintes Bibliotecas de Rede do SQL Server foram preteridas em versões do MDAC/WDAC: Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet e RPC. TCP/IP e pipes nomeados continuarão a ser compatíveis e estão disponíveis no sistema operacional Windows de 64 bits.
* **MSDASQL:** o MSDASQL (Provedor Microsoft OLE DB para ODBC) permite que aplicativos criados no OLE DB e no ADO (que usa o OLE DB internamente) acessem fontes de dados por meio de um driver ODBC. O MSDASQL é um provedor OLEDB que conecta-se ao ODBC, em vez de a um banco de dados. Ele é destinado a ser uma ponte do OLE DB para um driver ODBC quando não há nenhum provedor OLE DB direto para uma fonte de dados. O MSDASQL é enviado com o sistema operacional Windows e o Windows Server 2008 e o Vista SP1 foram as primeiras versões do Windows a incluírem uma versão de 64 bits da tecnologia.

### <a name="deprecated-mdacwdac-components"></a>Componentes preteridos do MDAC/WDAC

Esses componentes ainda são compatíveis com a versão atual do MDAC/WDAC, mas eles poderão ser removidos em versões futuras. Ao desenvolver novos aplicativos, a Microsoft recomenda que você evite usar esses componentes. Além disso, ao atualizar ou modificar aplicativos existentes, remova as dependências desses componentes.

* **SQLOLEDB:** o SQLOLEDB (provedor Microsoft OLE DB para SQL Server), que dá suporte ao acesso ao Microsoft SQL Server, foi preterido. A conectividade dele a versões futuras do SQL Server talvez não seja compatível. A capacidade de se conectar a versões anteriores ao SQL Server 7 será removida do sistema operacional após o Windows 7. Novos aplicativos devem usar o MSOLEDBSQL (Driver do Microsoft OLE DB para SQL Server), que dá suporte aos novos recursos do SQL Server. Os aplicativos existentes também devem migrar para o Driver do Microsoft OLE DB para SQL Server para melhores desempenho, confiabilidade e compatibilidade. Para obter mais informações, confira [Como atualizar um aplicativo do Driver do OLE DB para SQL Server no MDAC](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).
* **SQLODBC:** o SQLODBC (Microsoft ODBC Driver for SQL Server), que dá suporte ao acesso ao Microsoft SQL Server, foi preterido. A conectividade dele a versões futuras do SQL Server talvez não seja compatível. A capacidade de se conectar a versões anteriores ao SQL Server 7 será removida do sistema operacional após o Windows 7. Os novos aplicativos devem usar o Microsoft ODBC Driver for SQL Server no Windows, que dá suporte a novos recursos do SQL Server. Os aplicativos existentes também devem migrar para o Microsoft ODBC Driver for SQL Server para melhores desempenho, confiabilidade e compatibilidade. Para obter informações relevantes, confira [Como atualizar um aplicativo do MDAC para o SQL Server Native Client](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).
* **Mecanismo de Banco de Dados do Microsoft Jet 4.0:** da versão 2.6 em diante, o MDAC não contêm mais componentes do Jet. Em outras palavras, as versões 2.6, 2.7 e 2.8 do MDAC não contêm o Microsoft Jet, o Provedor OLE DB do Microsoft Jet, os Drivers de Banco de Dados do ODBC Desktop ou os DAO (Objetos de Acesso a Dados) do Jet. 

  Não há nenhuma versão de 64 bits do Mecanismo de Banco de Dados do Jet, do Driver OLE DB do Jet e nem do DAO do Jet disponível. Para saber mais, consulte o [artigo da base de dados 957570](https://support.microsoft.com/kb/957570). Nas versões de 64 bits do Windows, o Jet de 32 bits é executado no subsistema WOW64 do Windows. Para obter mais informações sobre o WOW64, confira a [documentação do WOW64 do MSDN](/windows/desktop/WinProg64/wow64-implementation-details). Os aplicativos nativos de 64 bits não podem se comunicar com os drivers Jet de 32 bits em execução no WOW64.

  Em vez do Microsoft Jet, a Microsoft recomenda usar o [Microsoft SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express) ao desenvolver aplicativos novos, que não sejam do Microsoft Access e que exijam um armazenamento de dados relacional. Esses aplicativos do Jet novos ou convertidos podem continuar a usar o Jet com a intenção de usar arquivos do Microsoft Office 2003 e de versões anteriores (.mdb e .xls) para armazenamento de dados não primário. No entanto, para esses aplicativos, você deve planejar a migração do Jet para o Mecanismo de Banco de Dados do Microsoft Access. Você pode [baixar o Mecanismo de Banco de Dados do Microsoft Access](https://www.microsoft.com/download/details.aspx?id=54920), que permite a leitura e a gravação em arquivos pré-existentes nos formatos de arquivo .mdb e .xls no Office 2003 ou *.accdb, *.xlsm, *.xlsx e *.xlsb no Office 2007.

  > [!IMPORTANT]
  > Leia o contrato de licença de usuário final de 2007 do Sistema Office para conhecer as limitações de uso específicas.

  > [!NOTE]
  > Os aplicativos do SQL Server também podem acessar arquivos do Sistema Office 2007 e de versões anteriores, bem como arquivos das funcionalidades do Integration Services e de conectividade de dados heterogêneos do SQL Server, por meio do Driver do Sistema Office 2007. Além disso, os aplicativos de 64 bits do SQL Server podem acessar arquivos do Sistema Office 2007 e do Jet de 32 bits usando o SSIS (SQL Server Integration Services) de 32 bits no Windows de 64 bits.

* **MSDADS:** com o MSDADS (Provedor Microsoft OLE DB para Data Shaping), você pode criar relações hierárquicas entre chaves, campos ou conjuntos de linhas em um aplicativo. Nenhum aprimoramento importante de recurso foi feito a ele desde a versão 2.1 do MDAC. Esse provedor foi preterido. A Microsoft recomenda que você use XML em vez do MSDADS.
* **Oracle ODBC e Oracle OLE DB:** o Microsoft ODBC Driver para Oracle (Oracle ODBC) e o Provedor Microsoft OLE DB para Oracle (Oracle OLE DB) fornecem acesso a servidores de banco de dados Oracle. Eles são criados usando a OCI (Oracle Call Interface) versão 7 e fornecem suporte total ao Oracle 7. Além disso, ele usa a emulação do Oracle 7 para fornecer suporte limitado a bancos de dados Oracle 8. O Oracle não dá mais suporte a aplicativos que usam chamadas da OCI versão 7. Essas tecnologias foram preteridas. Se você estiver usando fontes de dados Oracle, deverá migrar para o driver e o provedor fornecidos pela Oracle.
* **RDS:** o RDS (Serviços de Dados Remotos) é um mecanismo proprietário da Microsoft para acessar objetos do Conjunto de Registros de ADO remoto pela Internet ou por uma intranet. O RDS foi preterido. Nenhum aprimoramento importante de recurso foi feito a ele desde a versão 2.1 do MDAC. A Microsoft lançou o .NET Framework, que tem funcionalidades extensas de SOAP e substitui os componentes do RDS. Todos os componentes do servidor RDS serão removidos do sistema operacional após o Windows 7.
* **JRO:** O JRO (Objetos de Replicação do Jet) foi preterido. O JRO é usado no ADO com bancos de dados do Jet ( *.mdb) para criar e compactar bancos de dados do Jet (.mdb) e executar o gerenciamento de replicação do Jet. O MDAC 2.7 será sua última versão. O JRO não estará disponível no sistema operacional Windows de 64 bits. O JRO não é compatível com o formato de arquivo do Microsoft Access 2007 (* .accdb).
* **Suporte a ODBC de 16 bits:** se você estiver usando aplicativos de 16 bits, deverá migrar para um aplicativo de 32 bits. a funcionalidade de 16 bits foi preterida e está sendo removida dos sistemas operacionais de 64 bits. Para saber mais, consulte o [artigo 896458 da base de dados de conhecimento](https://support.microsoft.com/kb/896458).
* **Provedor simples do OLEDB (MSDAOSP):** o Provedor simples do OLEDB oferece uma estrutura para a criação rápida de provedores de OLE DB sobre dados simples. O MSDAOSP foi preterido.
* **Biblioteca de cursores ODBC:** a Biblioteca de cursores ODBC (ODBCCR32.dll) fornece cursores de dados limitados do lado do cliente. A Biblioteca de cursores ODBC foi preterida; seu aplicativo pode usar implementações de cursor do lado do servidor como uma substituição.
* **Comunicação remota da interface fora do processo do OLE DB:** a comunicação remota da interface do OLEDB (MSDAPS.dll) foi uma tentativa de permitir que os provedores de OLE DB executassem fora do processo. A comunicação remota de interface fora do processo do OLEDB foi preterida.
* **Bibliotecas de rede do SQL AppleTalk e Banyan Vines:** as bibliotecas de rede Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet e RPC SQL foram preteridas. Se você estiver usando qualquer uma dessas tecnologias, deverá modificar seus aplicativos para usar uma das outras bibliotecas de rede, como TCP/IP e pipe nomeado.

### <a name="mdacwdac-releases"></a>Versões do MDAC/WDAC

Aqui está uma lista dos cenários de suporte às versões anteriores do MDAC/WDAC, começando pelas mais antigas.

* **MDAC 1.5, MDAC 2.0 e MDAC 2.1:** essas versões do MDAC eram versões independentes que foram lançadas por meio do Pacote de Opções do Microsoft Windows NT, do SDK da plataforma Microsoft Windows ou do site do MDAC. Essa versões do MDAC não são mais compatíveis.
* **MDAC 2.5:** essa versão do MDAC foi incluída com o sistema operacional Windows 2000. Os Service Packs do MDAC 2.5 foram incluídos nos Service Packs correspondentes do Windows 2000.
* **MDAC 2.6:** as versões 2.6 RTM, SP1 e SP2 do MDAC foram incluídas com o Microsoft SQL Server 2000 RTM, SP1 e SP2, respectivamente. Além disso, esses Service Packs do MDAC foram lançados no site do MDAC de acordo com a agenda de lançamento de service packs do Microsoft SQL Server 2000. Você pode instalar esta versão do MDAC e os respectivos service packs nas plataformas Windows 2000, Windows Millennium Edition, Windows NT, Windows 95 e Windows 98. Essa versão do MDAC não é mais compatível.
* **MDAC 2.7:** essa versão do MDAC foi incluída com os sistemas operacionais Microsoft Windows XP RTM e SP1. Você pode instalar essa versão do MDAC e os respectivos service packs nas plataformas Windows 2000, Windows Millennium, Windows NT e Windows 98. Você pode instalar essa versão na plataforma Windows XP somente por meio do sistema operacional ou dos respectivos service packs. Essa versão do MDAC não é mais compatível.
* **MDAC 2.8:** essa versão do MDAC foi incluída com o Windows Server 2003 e Windows XP SP2 e versões posteriores. Você também pode instalar essa versão do MDAC e os respectivos service packs no Windows 2000.

  * A versão de 32 bits do MDAC 2.8 também foi lançada no site do MDAC quando o Windows Server 2003 foi lançado para o cliente.
  * A versão de 64 bits do MDAC 2.8 foi lançada com a versão de 64 bits do Windows Server 2003 e Windows XP.

* **WDAC (Windows Data Access Components):** o MDAC alterou seu nome para WDAC ("Windows Data Access Components"), desde o Windows Vista e do Windows Server 2008. O WDAC é incluído como parte do sistema operacional e não está disponível separadamente para redistribuição. A manutenção para o WDAC está sujeita ao ciclo de vida do sistema operacional.

  As versões de 32 bits e 64 bits do WDAC são lançadas com as versões de 32 bits e de 64 bits dos sistemas operacionais Windows, respectivamente.

## <a name="obsolete-data-access-technologies"></a>Tecnologias de acesso a dados obsoletas

Tecnologias obsoletas são tecnologias que não foram aprimoradas nem atualizadas após várias novas versões de produtos e que serão excluídas de futuras versões de produtos. Não use essas tecnologias ao escrever novos aplicativos. Quando você modifica os aplicativos existentes que são gravados usando essas tecnologias, considere migrar esses aplicativos para o ADO.NET ou outra tecnologia atual.

Os seguintes componentes são considerados obsoletos:

* **DB-Library:** DB-Library é um modelo de programação específicas do SQL Server que inclui APIs de C. Não houve aprimoramentos de recursos para a DB-Library desde o SQL Server 6.5. Sua versão final foi com o SQL Server 2000 e ela não será portada para o sistema operacional Windows de 64 bits.
* **E-SQL (Embedded SQL):** o E-SQL é um modelo de programação específico de SQL Server que permite que as instruções Transact-SQL sejam inseridas no código do Visual C. Nenhum aprimoramento de recurso foi feito no E-SQL desde o SQL Server 6.5. Sua versão final foi com o SQL Server 2000 e ela não será portada para o sistema operacional Windows de 64 bits.
* **DAO (Objetos de Acesso a Dados):** O DAO fornece acesso a bancos de dados do Jet (Access). Essa API pode ser usada do Microsoft Visual Basic, do Microsoft Visual C++ e de linguagens de script. Ele foi incluído com o Microsoft Office 2000 e o Office XP. O DAO 3.6 é a versão final dessa tecnologia. Ele não estará disponível no sistema operacional Windows de 64 bits.
* **RDO (Objetos de Dados Remotos):** o RDO foi projetado especificamente para acessar fontes de dados relacionais remotas do ODBC e tornou mais fácil usar o ODBC sem código de aplicativo complexo. Ele foi incluído com o Microsoft Visual Basic versões 4, 5 e 6. O RDO 2.0 foi a versão final dessa tecnologia.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
