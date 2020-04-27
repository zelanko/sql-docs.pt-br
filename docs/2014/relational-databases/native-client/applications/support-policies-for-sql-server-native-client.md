---
title: Políticas de suporte para SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 09c80cf4-23e6-4027-a24f-cdb9c87af811
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e5c7a01cc2a9569dd8c05316a2aa3314959e894
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63046521"
---
# <a name="support-policies-for-sql-server-native-client"></a>Políticas de suporte do SQL Server Native Client
  Este tópico aborda como vários componentes de acesso a dados podem ser usados com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="server-support"></a>Suporte de servidor  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]O Native Client 11,0 dá suporte a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]conexões [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]com [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]o [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)],, [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)],, e.  
  
## <a name="supported-operating-system-versions"></a>Versões do sistema operacional compatíveis  
 A tabela a seguir lista os sistemas operacionais que oferecem suporte ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
|Versão do SQL Server Native Client|Sistemas operacionais compatíveis|  
|--------------------------------------|---------------------------------|  
|SQL Server Native Client (SQL Server 2005)|-Microsoft Windows 2000 Service Pack 4 ou posterior<br />-Microsoft Windows Server 2003 ou posterior<br />-Microsoft Windows XP Service Pack 1 ou posterior<br />-Microsoft Windows Vista (requer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Service Pack 2 ou posterior)<br />-Microsoft Windows Server 2008 (requer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Service Pack 2 ou posterior)|  
|SQL Server Native Client 10,0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)])|-Microsoft Windows Server 2003 Service Pack 2 ou posterior<br />-Microsoft Windows XP Service Pack 2 ou posterior<br />-Microsoft Windows Vista<br />-Microsoft Windows Server 2008|  
|SQL Server Native Client 10,5 ([!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)])|-Microsoft Windows Server 2003 Service Pack 2 ou posterior<br />-Microsoft Windows XP Service Pack 2 ou posterior<br />-Microsoft Windows Vista<br />-Microsoft Windows Server 2008<br />-Microsoft Windows 7|  
|SQL Server Native Client 11.0 ([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)])|-Microsoft Windows Vista<br />-Microsoft Windows Server 2008<br />-Microsoft Windows 7<br />-Microsoft Windows 8<br />-Microsoft Windows Server 2012|  
  
## <a name="ado-support-policies"></a>Políticas de suporte para ADO  
 Os aplicativos ADO podem usar o provedor OLE DB SQLOLEDB incluído no Windows caso não precisem dos recursos do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou posterior.  
  
 Os aplicativos ADO podem usar a versão [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do Native Client incluída [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]no. Os aplicativos ADO também podem usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 (incluído no [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]), mas caso façam isso, eles devem especificar `DataTypeCompatibility=80` nas cadeias de conexão. Apenas os recursos do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] estão disponíveis quando `DataTypeCompatibility=80` está presente nas cadeias de conexão.  
  
## <a name="bcp-support-policies"></a>Políticas de suporte do BCP  
 A partir do [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], bcp.exe dá suporte a arquivos de dados que não sejam de mais de três versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores em relação à versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no qual o bcp.exe é fornecido.  
  
## <a name="odbc-support-policies"></a>Políticas de suporte do ODBC  
 Os aplicativos devem usar o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluído no sistema operacional Windows. É possível usar o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client caso o aplicativo seja certificado para ser usado com uma versão específica do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="ole-db-support-policies"></a>Políticas de suporte do OLE DB  
 Os aplicativos devem usar o provedor de dados OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluído no sistema operacional Windows. É possível usar o provedor de dados OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client caso o aplicativo seja certificado para ser usado com uma versão específica do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
 Os aplicativos OLE DB sem-certificação para serem usados com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client podem usar o cliente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native caso especifiquem `DataTypeCompatibility=80` nas cadeias de conexão.  
  
 Os aplicativos OLE DB que usam Componentes de Serviço do OLE DB só podem usar o cliente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Nativo caso especifiquem `DataTypeCompatibility=80` nas cadeias de conexão. No entanto, nenhum recurso [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] adicionado após estará disponível nesse caso.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos com o SQL Server Native Client](building-applications-with-sql-server-native-client.md)  
  
  
