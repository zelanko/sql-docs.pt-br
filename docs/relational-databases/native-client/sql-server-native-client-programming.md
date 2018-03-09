---
title: "Programação do SQL Server Native Client | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQLNCLI, about SQL Server Native Client
- SQL Server Native Client, about SQL Server Native Client
- data access [SQL Server Native Client], about SQL Server Native Client
- data access [SQL Server Native Client]
- SQL Server Native Client
- SQLNCLI
- native data access [SQL Server Native Client]
ms.assetid: 14ba2cb1-a424-4e4d-b224-0bf1015ab801
caps.latest.revision: "66"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 80e90fe4e92edb1cc3cd7dd60e8f948b00cf4377
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="sql-server-native-client-programming"></a>Programação do SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client é uma API (interface de programação de aplicativo) autônoma para acesso a dados que foi introduzida no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e que é usada tanto para OLE DB quanto para ODBC. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client integra o provedor OLE DB SQL e o driver ODBC SQL em uma DLL (biblioteca de vínculo dinâmico) nativa. Ele também oferece uma nova funcionalidade além da fornecida pelo Windows DAC (Windows Data Access Components, anteriormente conhecido como MDAC ou Microsoft Data Access Components). O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client pode ser usado para criar novos aplicativos ou aprimorar aplicativos existentes que precisam aproveitar os novos recursos apresentados no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], tais como MARS (vários conjuntos de resultados ativos), UDT (tipos de dados definidos pelo usuário), notificações de consulta, isolamento do instantâneo e suporte a tipos de dados XML.  
  
> [!NOTE]  
>  Para obter uma lista das diferenças entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client e Windows DAC, além de informações sobre os problemas a serem considerados antes de atualizar um aplicativo do Windows DAC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, consulte [atualizando um aplicativo para o SQL Server Cliente nativo do MDAC](../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client sempre é usado com o Gerenciador de Driver ODBC fornecido com o Windows DAC. O provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client pode ser usado com o OLE DB Core Services fornecido com o Windows DAC, mas isso não é um requisito; a opção por usar ou não o Core Services depende dos requisitos do aplicativo individual (por exemplo, caso o pool de conexões seja obrigatório).  
  
 Aplicativos de ActiveX Data Object (ADO) podem usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client, mas é recomendável usar ADO em conjunto com o **DataTypeCompatibility** palavra-chave de cadeia de caracteres de conexão (ou seu correspondente **Fonte de dados** propriedade). Quando você usar o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, os aplicativos ADO poderão explorar esses novos recursos apresentados no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e disponíveis através das palavras-chave da cadeia de caracteres de conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, das propriedades de OLE DB ou do [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para obter mais informações sobre o uso desses recursos com o ADO, consulte [usando o ADO com SQL Server Native Client](../../relational-databases/native-client/applications/using-ado-with-sql-server-native-client.md).  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client foi projetado para fornecer um método simplificado de obter acesso a dados nativos no SQL Server usando o OLE DB ou o ODBC. Ele é simplificado pois combina as tecnologias OLE DB e ODBC em uma só biblioteca, além de fornecer uma maneira de inovar e desenvolver novos recursos de acesso a dados, sem alterar os componentes atuais do Windows DAC, que agora fazem parte da plataforma Microsoft Windows.  
  
 Embora o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client use componentes do Windows DAC, ele não depende explicitamente de uma versão específica do Windows DAC. É possível usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client com a versão do Windows DAC instalada com qualquer sistema operacional para o qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client oferece suporte.  
  
## <a name="in-this-section"></a>Nesta seção  
 [SQL Server Native Client](../../relational-databases/native-client/sql-server-native-client.md)  
 Lista os principais novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [Quando usar o SQL Server Native Client](../../relational-databases/native-client/when-to-use-sql-server-native-client.md)  
 Aborda como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se adapta a tecnologias de acesso a dados da Microsoft, mostra suas semelhanças com o Windows DAC e o ADO.NET e fornece ponteiros para decidir qual tecnologia de acesso a dados deve ser usada.  
  
 [Recursos do SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
 Descreve os recursos aos quais o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte.  
  
 [Criando aplicativos com o SQL Server Native Client](../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
 Fornece uma visão geral do desenvolvimento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, inclusive as diferenças entre ele e o Windows DAC, os componentes usados por ele e como o ADO pode ser usado com ele.  
  
 Esta seção também discute a instalação e a implantação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, incluindo como redistribuir a biblioteca do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [Requisitos do sistema do SQL Server Native Client](../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md)  
 Aborda os recursos de sistema necessários ao uso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
 Fornece informações sobre como usar o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [Cliente nativo do SQL Server &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
 Fornece informações sobre como usar o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [Localizando mais informações sobre o SQL Server Native Client](../../relational-databases/native-client/finding-more-sql-server-native-client-information.md)  
 Fornece recursos adicionais sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, incluindo links para recursos externos e assistência adicional.  
  
 [Erros do SQL Server Native Client](http://msdn.microsoft.com/library/ebd0e9a8-5fe5-4b15-9a44-2f131a13c186)  
 Contém tópicos sobre erros de tempo de execução associados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="see-also"></a>Consulte também  
 [Atualizando um aplicativo do SQL Server 2005 Native Client](../../relational-databases/native-client/applications/updating-an-application-from-sql-server-2005-native-client.md)   
 [Tópicos de instruções sobre ODBC](../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [Tópicos de instruções do OLE DB](../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
