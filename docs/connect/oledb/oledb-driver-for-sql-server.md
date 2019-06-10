---
title: Microsoft OLE DB Driver for SQL Server | Microsoft Docs
description: Driver do Microsoft OLE DB para SQL Server
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server
- MSOLEDBSQL
- native data access [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: bf7f80fb6488e4508d4a7abda59d690e7f7dc805
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66795865"
---
# <a name="microsoft-ole-db-driver-for-sql-server"></a>Driver do Microsoft OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

O OLE DB Driver for SQL Server é uma interface de programação de aplicativo (API) de acesso de dados autônoma, usada para OLE DB, que foi introduzida no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. O OLE DB Driver for SQL Server oferece o driver do OLE DB do SQL em uma biblioteca de vínculo dinâmico (DLL). Ele também oferece uma nova funcionalidade além da fornecida pelo Windows DAC (Windows Data Access Components, anteriormente conhecido como MDAC ou Microsoft Data Access Components). O OLE DB Driver for SQL Server pode ser usado para criar novos aplicativos ou aprimorar os aplicativos existentes que precisam utilizar os recursos introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], como o MARS (conjuntos de resultados ativos múltiplos), UDT (tipos de dados definidos pelo usuário), notificações de consulta, isolamento de instantâneo e suporte a tipos de dados XML.  
  
> [!NOTE]  
> Para obter uma lista das diferenças entre o OLE DB Driver for SQL Server e o Windows DAC, além de informações sobre os problemas a considerar antes de atualizar um aplicativo do Windows DAC para OLE DB Driver for SQL Server, confira [Atualização de um aplicativo do OLE DB Driver for SQL Server no MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  

> [!IMPORTANT]
> O [Microsoft OLE DB Provider para SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) anterior e o provedor [SQL Server Native Client OLE DB](../../relational-databases/native-client/sql-server-native-client.md) (SQLNCLI) permanecem preteridos e não é recomendável usar nenhum dos dois para um novo trabalho de desenvolvimento.
  
 O OLE DB Driver for SQL Server pode ser usado com o OLE DB Core Services fornecido com o Windows DAC, mas isso não é um requisito; a opção de usar ou não o Core Services depende dos requisitos do aplicativo individual (por exemplo, se o pool de conexões é obrigatório).  
  
 Os aplicativos ADO (ActiveX Data Object) podem usar o provedor OLE DB Driver for SQL Server, embora recomendemos usar o ADO com a palavra-chave da cadeia de conexão**DataTypeCompatibility** (ou a propriedade **DataSource** correspondente). Ao usar o OLE DB Driver for SQL Server, os aplicativos ADO podem explorar esses novos recursos apresentados no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] disponíveis por meio das palavras-chave de cadeia de conexão, pelas propriedades do OLE DB ou por [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para saber mais sobre o uso desses recursos com ADO, confira [Usar o ADO com o Driver OLE DB para SQL Server](../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md).  
  
 O OLE DB Driver for SQL Server foi projetado para fornecer um método simplificado de obter acesso a dados nativos no SQL Server usando o OLE DB. Ele fornece uma maneira de inovar e desenvolver novos recursos de acesso a dados, sem alterar os componentes atuais do Windows DAC, que agora fazem parte da plataforma Microsoft Windows.  
  
 Embora o OLE DB Driver for SQL Server use componentes do Windows DAC, ele não depende explicitamente de uma versão específica do Windows DAC. É possível usar o OLE DB Driver for SQL Server com a versão do Windows DAC instalada com qualquer sistema operacional compatível com OLE DB Driver for SQL Server.  

 ## <a name="different-generations-of-ole-db-drivers"></a>Diferentes gerações de OLE DB Drivers

Há três gerações distintas de provedores Microsoft OLE DB para SQL Server.

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1. Provedor Microsoft OLE DB para SQL Server (SQLOLEDB)
O [Microsoft OLE DB Provider para SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) ainda é fornecido como parte do [Windows Data Access Components](https://msdn.microsoft.com/library/ms692897.aspx). Ele não é mais mantido e não é recomendável usar esse driver para um novo desenvolvimento.

### <a name="2-sql-server-native-client-snac"></a>2. SNAC (SQL Server Native Client)
A partir da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md) inclui a interface do provedor OLE DB (SQLNCLI), sendo o provedor OLE DB fornecido com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] através do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].

Foi [anunciado como preterido em 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) e não é mais mantido, não sendo recomendável usar esse driver para um novo desenvolvimento. Para saber mais sobre o ciclo de vida de SNAC e downloads disponíveis, confira [Explicação do ciclo de vida de SNAC](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/).

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3. Microsoft OLE DB Driver for SQL Server (MSOLEDBSQL)
O OLE DB [não está mais preterido](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) e foi lançado em 2018.

O novo provedor OLE DB é chamado Microsoft OLE DB Driver for SQL Server (MSOLEDBSQL). De agora em diante, o novo provedor será atualizado com os mais recentes recursos de servidor.

> [!NOTE]
> Para usar o novo Microsoft OLE DB Driver for SQL Server nos aplicativos existentes, você deve converter as cadeias de conexão de SQLOLEDB ou SQLNCLI para MSOLEDBSQL.
  
## <a name="in-this-section"></a>Nesta seção  
[Quando usar o Driver do OLE DB para SQL Server](../oledb/when-to-use-oledb-driver-for-sql-server.md)  
 Aborda como o OLE DB Driver for SQL Server se adapta a tecnologias de acesso a dados da Microsoft, mostra suas semelhanças com o Windows DAC e o ADO.NET e fornece ponteiros para decidir qual tecnologia de acesso a dados deve ser usada.  
  
 [Recursos do OLE DB Driver para SQL Server](../oledb/features/oledb-driver-for-sql-server-features.md )  
 Descreve os recursos compatíveis com o OLE DB Driver for SQL Server.  
  
 [Criar aplicativos com o OLE DB Driver para SQL Server](../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
 Fornece uma visão geral do desenvolvimento do OLE DB Driver for SQL Server, incluindo as diferenças entre ele e o Windows DAC, os componentes usados e como o ADO pode ser usado com ele.  
  
 Esta seção também discute a instalação e a implantação do OLE DB Driver for SQL Server, incluindo como redistribuir a biblioteca do OLE DB Driver for SQL Server.  
  
 [Requisitos do sistema para o OLE DB Driver para SQL Server](../oledb/system-requirements-for-oledb-driver-for-sql-server.md)  
 Aborda os recursos de sistema necessários ao uso do OLE DB Driver for SQL Server.  
  
 [Programação no OLE DB Driver para SQL Server](../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
 Fornece informações sobre como usar o OLE DB Driver for SQL Server.  
  
 [Encontrar mais informações sobre o OLE DB Driver para SQL Server](../oledb/finding-more-oledb-driver-for-sql-server-information.md)  
 Fornece recursos adicionais sobre o OLE DB Driver for SQL Server, incluindo links para recursos externos e assistência adicional.  
  
  
## <a name="see-also"></a>Confira também  
 [Atualização de um aplicativo no SQL Server 2005 Native Client](../oledb/applications/updating-an-application-from-sql-server-2005-native-client.md)    
 [Tópicos de instruções do OLE DB](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
