---
title: Programação de SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c288ade95434bc06fcbf7613a71c2106631128e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "76929549"
---
# <a name="sql-server-native-client-programming"></a>Programação do SQL Server Native Client
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client é uma API (interface de programação de aplicativo) autônoma para acesso a dados que foi introduzida no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e que é usada tanto para OLE DB quanto para ODBC. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client integra o provedor OLE DB SQL e o driver ODBC SQL em uma DLL (biblioteca de vínculo dinâmico) nativa. Ele também oferece uma nova funcionalidade além da fornecida pelo Windows DAC (Windows Data Access Components, anteriormente conhecido como MDAC ou Microsoft Data Access Components). O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client pode ser usado para criar novos aplicativos ou aprimorar aplicativos existentes que precisam aproveitar os novos recursos apresentados no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], tais como MARS (vários conjuntos de resultados ativos), UDT (tipos de dados definidos pelo usuário), notificações de consulta, isolamento do instantâneo e suporte a tipos de dados XML.  
  
> [!NOTE]  
>  Para obter uma lista das diferenças entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o cliente nativo e o DAC do Windows, além de informações sobre os problemas a serem considerados antes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de atualizar um aplicativo de DAC do Windows para o Native Client, consulte [atualizando um aplicativo para SQL Server Native Client do MDAC](applications/updating-an-application-to-sql-server-native-client-from-mdac.md).  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client sempre é usado com o Gerenciador de Driver ODBC fornecido com o Windows DAC. O provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client pode ser usado com o OLE DB Core Services fornecido com o Windows DAC, mas isso não é um requisito; a opção por usar ou não o Core Services depende dos requisitos do aplicativo individual (por exemplo, caso o pool de conexões seja obrigatório).  
  
 Os aplicativos ADO (ActiveX Data Object) podem usar o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, embora se recomende usar o ADO com a palavra-chave da cadeia de caracteres de conexão `DataTypeCompatibility` (ou a propriedade `DataSource` correspondente). Quando você usar o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, os aplicativos ADO poderão explorar esses novos recursos apresentados no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e disponíveis através das palavras-chave da cadeia de caracteres de conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, das propriedades de OLE DB ou do [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para obter mais informações sobre o uso desses recursos com o ADO, consulte [usando o ADO com SQL Server Native Client](applications/using-ado-with-sql-server-native-client.md).  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client foi projetado para fornecer um método simplificado de obter acesso a dados nativos no SQL Server usando o OLE DB ou o ODBC. Ele é simplificado pois combina as tecnologias OLE DB e ODBC em uma só biblioteca, além de fornecer uma maneira de inovar e desenvolver novos recursos de acesso a dados, sem alterar os componentes atuais do Windows DAC, que agora fazem parte da plataforma Microsoft Windows.  
  
 Embora [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Native Client use componentes no DAC do Windows, ele não depende explicitamente de uma versão específica do DAC do Windows. É possível usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client com a versão do Windows DAC instalada com qualquer sistema operacional para o qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client oferece suporte.  
  
## <a name="in-this-section"></a>Nesta seção  
 [O que há de novo no SQL Server Native Client](sql-server-native-client.md)  
 Lista os principais novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [Quando usar o SQL Server Native Client](when-to-use-sql-server-native-client.md)  
 Aborda como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se adapta a tecnologias de acesso a dados da Microsoft, mostra suas semelhanças com o Windows DAC e o ADO.NET e fornece ponteiros para decidir qual tecnologia de acesso a dados deve ser usada.  
  
 [Recursos do SQL Server Native Client](features/sql-server-native-client-features.md)  
 Descreve os recursos aos quais o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte.  
  
 [Criando aplicativos com o SQL Server Native Client](applications/building-applications-with-sql-server-native-client.md)  
 Fornece uma visão geral do desenvolvimento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, inclusive as diferenças entre ele e o Windows DAC, os componentes usados por ele e como o ADO pode ser usado com ele.  
  
 Esta seção também discute a instalação e a implantação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, incluindo como redistribuir a biblioteca do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [Requisitos do sistema do SQL Server Native Client](system-requirements-for-sql-server-native-client.md)  
 Aborda os recursos de sistema necessários ao uso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [SQL Server Native Client &#40;OLE DB&#41;](ole-db/sql-server-native-client-ole-db.md)  
 Fornece informações sobre como usar o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [SQL Server Native Client &#40;ODBC&#41;](odbc/sql-server-native-client-odbc.md)  
 Fornece informações sobre como usar o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [Localizando mais informações sobre o SQL Server Native Client](finding-more-sql-server-native-client-information.md)  
 Fornece recursos adicionais sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, incluindo links para recursos externos e assistência adicional.  
  
 [Erros do SQL Server Native Client](../native-client-ole-db-errors/errors.md)  
 Contém tópicos sobre erros de runtime associados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="see-also"></a>Consulte Também  
 [Atualizando um aplicativo do SQL Server Native Client 2005](applications/updating-an-application-from-sql-server-2005-native-client.md)   
 [Tópicos de instruções sobre ODBC](../native-client-odbc-how-to/odbc-how-to-topics.md)   
 [Tópicos de instruções sobre OLE DB](../native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
