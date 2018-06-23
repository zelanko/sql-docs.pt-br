---
title: Driver do Microsoft OLE DB para SQL Server | Microsoft Docs
description: Driver do Microsoft OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 1fba5146cd663c2d7c312bb6a5c689162c1489ac
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36240818"
---
# <a name="microsoft-ole-db-driver-for-sql-server"></a>Driver do Microsoft OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  OLE DB Driver para SQL Server é uma dados autônoma acesso aplicativo interface de programação (API) usada para OLE DB, que foi introduzida no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. OLE DB Driver para SQL Server oferece o driver OLE DB do SQL em uma biblioteca de vínculo dinâmico (DLL). Ele também oferece uma nova funcionalidade além da fornecida pelo Windows DAC (Windows Data Access Components, anteriormente conhecido como MDAC ou Microsoft Data Access Components). OLE DB Driver para SQL Server pode ser usado para criar novos aplicativos ou aprimorar aplicativos existentes que precisam aproveitar os recursos introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], como vários conjuntos de resultados ativos (MARS), tipos de dados definidos pelo usuário (UDT), consulta suportam a notificações, o isolamento de instantâneo e o tipo de dados XML.  
  
> [!NOTE]  
>  Para obter uma lista das diferenças entre o OLE DB Driver para SQL Server e Windows DAC, além de informações sobre os problemas a serem considerados antes de atualizar um aplicativo do Windows DAC para o Driver do OLE DB para SQL Server, consulte [atualizando um aplicativo para o Driver do OLE DB para SQL Servidor do MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  
  
 O Driver OLE DB para SQL Server pode ser usado em conjunto com o OLE DB Core Services fornecido com o Windows DAC, mas isso não é um requisito; a opção de usar ou não o Core Services depende dos requisitos do aplicativo individual (por exemplo, se o pool de conexão é necessário).  
  
 Aplicativos de ActiveX Data Object (ADO) podem usar o Driver OLE DB para SQL Server, mas é recomendável usar o ADO em conjunto com o **DataTypeCompatibility** palavra-chave de cadeia de caracteres de conexão (ou correspondente  **Fonte de dados** propriedade). Ao usar o Driver OLE DB para SQL Server, os aplicativos ADO poderão explorar esses novos recursos introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que estão disponíveis por meio do Driver OLE DB para SQL Server por meio de palavras-chave de cadeia de caracteres de conexão ou propriedades do OLE DB ou [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para obter mais informações sobre o uso desses recursos com o ADO, consulte [usando o ADO com OLE DB para SQL Server](../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md).  
  
 OLE DB Driver para SQL Server foi projetado para fornecer um método simplificado de obter acesso a dados nativos para SQL Server usando o OLE DB. Ele fornece uma maneira de inovar e desenvolver novos recursos de acesso de dados sem alterar os componentes de Windows DAC atuais, que agora fazem parte da plataforma Microsoft Windows.  
  
 Enquanto o OLE DB Driver para SQL Server usa os componentes do Windows DAC, não é explicitamente dependente em uma versão específica do Windows DAC. Você pode usar o Driver do OLE DB para SQL Server com a versão do Windows DAC instalada com qualquer sistema operacional com suporte pelo Driver do OLE DB para SQL Server.  

 ## <a name="different-generations-of-ole-db-drivers"></a>Diferentes gerações de Drivers do OLE DB

Há três gerações distintas do provedor Microsoft OLE DB para SQL Server.

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1. Provedor Microsoft OLE DB para SQL Server (SQLOLEDB)
O [Microsoft OLE DB Provider para SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) ainda é fornecido como parte do [Windows Data Access Components](https://msdn.microsoft.com/en-us/library/ms692897.aspx). Não é mais mantido e não é recomendável usar esse driver para novo desenvolvimento.

### <a name="2-sql-server-native-client-snac"></a>2. SQL Server Native Client (SNAC)
A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md) inclui uma interface de provedor do OLE DB (SQLNCLI) e é o provedor OLE DB que acompanha [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] por meio de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].

Foi [anunciados como substituídos no 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) e não é recomendável usar esse driver para novo desenvolvimento. Para obter mais informações sobre o ciclo de vida SNAC e downloads disponíveis, consulte [SNAC de ciclo de vida explicado](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/).

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3. Driver do Microsoft OLE DB para SQL Server (MSOLEDBSQL)
OLE DB foi [undeprecated](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) e lançadas em 2018.

O novo provedor de OLE DB é chamado de Driver OLE DB da Microsoft para SQL Server (MSOLEDBSQL). O novo provedor será atualizado com os recursos de servidor mais recentes no futuro.

> [!NOTE]
> Para usar o novo Microsoft OLE DB Driver para SQL Server nos aplicativos existentes, você deve planejar converter cadeias de caracteres de conexão do SQLOLEDB ou SQLNCLI, para MSOLEDBSQL.
  
## <a name="in-this-section"></a>Nesta seção  
[Quando usar o Driver do OLE DB para SQL Server](../oledb/when-to-use-oledb-driver-for-sql-server.md)  
 Discute como OLE DB Driver para SQL Server se encaixa em dados do Microsoft tecnologias de acesso, como ele se compara ao Windows DAC e o ADO.NET e fornece ponteiros para decidir qual tecnologia para usar o acesso a dados.  
  
 [Recursos do Driver do OLE DB para SQL Server](../oledb/features/oledb-driver-for-sql-server-features.md )  
 Descreve os recursos com suporte pelo Driver do OLE DB para SQL Server.  
  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
 Fornece uma visão geral do Driver do OLE DB para desenvolvimento do SQL Server, incluindo como ele é diferente de Windows DAC, os componentes que ele usa, e como o ADO pode ser usado com ele.  
  
 Esta seção também discute o Driver do OLE DB para instalação do SQL Server e a implantação, incluindo como redistribuir o Driver OLE DB para a biblioteca do SQL Server.  
  
 [Requisitos do sistema para o Driver do OLE DB para SQL Server](../oledb/system-requirements-for-oledb-driver-for-sql-server.md)  
 Discute os recursos de sistema necessários para usar o Driver do OLE DB para SQL Server.  
  
 [Programação no Driver do OLE DB para SQL Server](../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
 Fornece informações sobre como usar o Driver OLE DB para SQL Server.  
  
 [Como encontrar mais informações sobre o Driver do OLE DB para SQL Server](../oledb/finding-more-oledb-driver-for-sql-server-information.md)  
 Fornece recursos adicionais sobre o Driver do OLE DB para SQL Server, incluindo links para recursos externos e assistência adicional.  
  
  
## <a name="see-also"></a>Consulte também  
 [Atualizando um aplicativo do SQL Server 2005 Native Client](../oledb/applications/updating-an-application-from-sql-server-2005-native-client.md)    
 [Tópicos de instruções do OLE DB](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
