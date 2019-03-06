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
manager: craigg
ms.openlocfilehash: 00be1d87dbc8ba071403722b7e575e5ab1c7a215
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744566"
---
# <a name="microsoft-ole-db-driver-for-sql-server"></a>Driver do Microsoft OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  Driver do OLE DB para SQL Server é uma dados autônoma acesso aplicativo interface de programação (API) usada para OLE DB, que foi introduzido no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Driver do OLE DB para SQL Server oferece o driver do OLE DB do SQL em uma biblioteca de vínculo dinâmico (DLL). Ele também oferece uma nova funcionalidade além da fornecida pelo Windows DAC (Windows Data Access Components, anteriormente conhecido como MDAC ou Microsoft Data Access Components). O OLE DB Driver for SQL Server pode ser usado para criar aplicativos ou aprimorar os aplicativos existentes que precisam aproveitar os novos recursos introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], como o MARS (conjuntos de resultados ativos múltiplos), UDT (tipos de dados definidos pelo usuário), notificações de consulta, isolamento de instantâneo e suporte a tipos de dados XML.  
  
> [!NOTE]  
>  Para obter uma lista das diferenças entre o Driver do OLE DB para SQL Server e Windows DAC, além de informações sobre os problemas a considerar antes de atualizar um aplicativo do Windows DAC para o Driver do OLE DB para SQL Server, consulte [atualizando um aplicativo para o Driver do OLE DB para SQL Servidor do MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  
  
 O OLE DB Driver for SQL Server pode ser usado com o OLE DB Core Services fornecido com o Windows DAC, mas isso não é um requisito; a opção de usar ou não o Core Services depende dos requisitos do aplicativo individual (por exemplo, se o pool de conexões é obrigatório).  
  
 Aplicativos de ActiveX Data Object (ADO) podem usar o Driver do OLE DB para SQL Server, mas é recomendável usar o ADO em conjunto com o **DataTypeCompatibility** palavra-chave de cadeia de caracteres de conexão (ou correspondente  **Fonte de dados** propriedade). Ao usar o Driver do OLE DB para SQL Server, os aplicativos ADO poderão explorar esses novos recursos introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que estão disponíveis por meio do Driver do OLE DB para SQL Server por meio de palavras-chave de cadeia de caracteres de conexão ou propriedades do OLE DB ou [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para obter mais informações sobre o uso desses recursos com o ADO, consulte [usando o ADO com o Driver do OLE DB para SQL Server](../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md).  
  
 O OLE DB Driver for SQL Server foi projetado para fornecer um método simplificado de obter acesso a dados nativos no SQL Server usando o OLE DB. Ele fornece uma maneira de inovar e desenvolver novos recursos de acesso de dados sem alterar os componentes de Windows DAC atuais, que agora fazem parte da plataforma Microsoft Windows.  
  
 Embora o OLE DB Driver for SQL Server use componentes do Windows DAC, ele não depende explicitamente de uma versão específica do Windows DAC. Você pode usar o Driver do OLE DB para SQL Server com a versão do Windows DAC instalada com qualquer sistema operacional com suporte pelo Driver do OLE DB para SQL Server.  

 ## <a name="different-generations-of-ole-db-drivers"></a>Diferentes gerações de Drivers de OLE DB

Há três gerações distintas do provedor Microsoft OLE DB para SQL Server.

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1. Provedor Microsoft OLE DB para SQL Server (SQLOLEDB)
O [Microsoft OLE DB Provider para SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) ainda é fornecido como parte da [Windows Data Access Components](https://msdn.microsoft.com/library/ms692897.aspx). Não é mais mantido e não é recomendável usar esse driver para novo desenvolvimento.

### <a name="2-sql-server-native-client-snac"></a>2. SNAC (SQL Server Native Client)
A partir [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md) inclui uma interface de provedor do OLE DB (SQLNCLI) e é o provedor OLE DB que acompanha [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] por meio de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].

Ele foi [anunciados como substituídos em 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) e não é recomendável usar esse driver para novo desenvolvimento. Para obter mais informações sobre o ciclo de vida do SNAC e downloads disponíveis, consulte [ciclo de vida do SNAC explicado](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/).

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3. Microsoft OLE DB Driver for SQL Server (MSOLEDBSQL)
OLE DB foi [undeprecated](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) e lançado em 2018.

O novo provedor de OLE DB é chamado o Driver OLE DB da Microsoft para SQL Server (MSOLEDBSQL). O novo provedor será atualizado com os mais recentes recursos de servidor no futuro.

> [!NOTE]
> Para usar o novo Microsoft Driver do OLE DB para SQL Server nos aplicativos existentes, você deve planejar converter as cadeias de conexão de SQLOLEDB ou SQLNCLI, para MSOLEDBSQL.
  
## <a name="in-this-section"></a>Nesta seção  
[Quando usar o Driver do OLE DB para SQL Server](../oledb/when-to-use-oledb-driver-for-sql-server.md)  
 Aborda como o OLE DB Driver for SQL Server se adapta a tecnologias de acesso a dados da Microsoft, mostra suas semelhanças com o Windows DAC e o ADO.NET e fornece ponteiros para decidir qual tecnologia de acesso a dados deve ser usada.  
  
 [Recursos do OLE DB Driver para SQL Server](../oledb/features/oledb-driver-for-sql-server-features.md )  
 Descreve os recursos com suporte pelo Driver do OLE DB para SQL Server.  
  
 [Criar aplicativos com o OLE DB Driver para SQL Server](../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
 Fornece uma visão geral do desenvolvimento do OLE DB Driver for SQL Server, incluindo as diferenças entre ele e o Windows DAC, os componentes usados e como o ADO pode ser usado com ele.  
  
 Esta seção também discute o Driver do OLE DB para instalação do SQL Server e a implantação, incluindo como redistribuir o Driver OLE DB para a biblioteca do SQL Server.  
  
 [Requisitos do sistema para o OLE DB Driver para SQL Server](../oledb/system-requirements-for-oledb-driver-for-sql-server.md)  
 Discute os recursos de sistema necessários para usar o Driver do OLE DB para SQL Server.  
  
 [Programação no OLE DB Driver para SQL Server](../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
 Fornece informações sobre como usar o Driver do OLE DB para SQL Server.  
  
 [Encontrar mais informações sobre o OLE DB Driver para SQL Server](../oledb/finding-more-oledb-driver-for-sql-server-information.md)  
 Fornece recursos adicionais sobre o Driver do OLE DB para SQL Server, incluindo links para recursos externos e assistência adicional.  
  
  
## <a name="see-also"></a>Confira também  
 [Atualização de um aplicativo no SQL Server 2005 Native Client](../oledb/applications/updating-an-application-from-sql-server-2005-native-client.md)    
 [Tópicos de instruções do OLE DB](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
