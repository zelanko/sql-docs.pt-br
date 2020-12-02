---
title: Requisitos do sistema para o OLE DB Driver for SQL Server
description: Conheça os pré-requisitos de software necessários para usar os recursos de acesso a dados do SQL Server, como MARS, no Driver do OLE DB para SQL Server.
ms.custom: ''
ms.date: 03/18/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- system requirements [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], system requirements
- OLE DB Driver for SQL Server, system requirements
- MSOLEDBSQL, system requirements
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c86f62f98e81ce3c4fdd86e1e79e8f73e1422851
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127969"
---
# <a name="system-requirements-for-ole-db-driver-for-sql-server"></a>Requisitos do sistema para o OLE DB Driver for SQL Server

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

Para usar recursos de acesso a dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como o MARS, você precisa ter este software instalado:  

* Driver do OLE DB para SQL Server no cliente.  
* Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em seu servidor.

> [!NOTE]  
> Certifique-se de que tenha efetuado logon com privilégios de administrador antes de instalar esse software.  

## <a name="operating-system-requirements"></a>Requisitos do sistema operacional  

Para obter uma lista dos sistemas operacionais que dão suporte ao Driver do OLE DB para SQL Server, confira [Políticas de suporte para o Driver do OLE DB para SQL Server](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md).  

## <a name="azure-active-directory-authentication-requirements"></a>Requisitos de autenticação do Azure Active Directory  

Ao usar métodos de autenticação do Azure Active Directory com versões do Driver do OLE DB para SQL Server ***anteriores à** _ 18.3, verifique se a [Biblioteca de Autenticação do Active Directory para o SQL Server](https://go.microsoft.com/fwlink/?LinkID=513072) foi instalada. (A versão 18.3 inclui a dependência como parte do pacote do instalador.) A ADAL não é necessária para os outros métodos de autenticação nem para as outras operações do OLE DB. Para obter mais informações, consulte: [Como usar o Azure Active Directory](features/using-azure-active-directory.md).

## <a name="sql-server-requirements"></a>Requisitos do SQL Server  

Para usar o Driver do OLE DB para SQL Server para acessar dados em bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você precisa ter uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada.  

O [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] dá suporte a conexões de todas as versões do MDAC, do Windows Data Access Components e de todas as versões do OLE DB Driver for SQL Server. Quando uma versão anterior do cliente se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tipos de dados de servidor desconhecidos desse cliente são mapeados para tipos compatíveis com a versão do cliente. Para saber mais, confira [Compatibilidade de tipo de dados para versões do cliente](#data-type-compatibility-for-client-versions).  

## <a name="cross-language-requirements"></a>Requisitos entre idiomas  

A versão em inglês do Driver do OLE DB para SQL Server é compatível com todas as versões localizadas de sistemas operacionais compatíveis. As versões localizadas do Driver do OLE DB para SQL Server são compatíveis com os sistemas operacionais localizados que têm o mesmo idioma que a versão localizada do Driver do OLE DB para SQL Server. Também há suporte para as versões localizadas do OLE DB Driver for SQL Server nas versões em inglês dos sistemas operacionais compatíveis, desde que as configurações do idioma correspondente estejam instaladas.  

Para atualizações:  

_ As versões de idioma inglês do Driver do OLE DB para SQL Server podem ser atualizadas para qualquer versão localizada do Driver do OLE DB para SQL Server.  
* As versões localizadas do Driver do OLE DB para SQL Server podem ser atualizadas para versões localizadas do Driver do OLE DB para SQL Server no mesmo idioma.  
* A versão localizada do Driver do OLE DB para SQL Server pode ser atualizada para a versão em idioma inglês do Driver do OLE DB para SQL Server.  
* As versões localizadas do Driver do OLE DB para SQL Server não podem ser atualizadas para versões do Driver do OLE DB para SQL Server localizadas em um idioma diferente.  

## <a name="data-type-compatibility-for-client-versions"></a>Compatibilidade de tipo de dados para versões de cliente  

O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o OLE DB Driver for SQL Server mapeiam novos tipos de dados para tipos de dados mais antigos que são compatíveis com clientes de nível inferior, conforme mostrado na tabela abaixo.  

Aplicativos OLE DB e ADO podem usar a palavra-chave da cadeia de conexão **DataTypeCompatibility** com o Driver do OLE DB para SQL Server para operar com tipos de dados mais antigos. Quando **DataTypeCompatibility=80**, os clientes do OLE DB se conectarão com a versão do protocolo TDS do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], em vez de com a versão TDS. Isso significa que, para o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e tipos de dados posteriores, a conversão de nível inferior será executada pelo servidor, em vez de pelo OLE DB Driver for SQL Server. Isso também significa que os recursos disponíveis na conexão serão limitados ao conjunto de recursos do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. As tentativas de uso de novos tipos de dados ou recursos são detectadas o quanto antes em chamadas API e erros são retornados ao aplicativo da chamada, em vez de se tentar passar solicitações inválidas ao servidor.  

IDBInfo::GetKeywords sempre retornará uma lista de palavras-chave que corresponde à versão de servidor na conexão e não é afetada por **DataTypeCompatibility**.  

|Tipo de dados|SQL Server Native Client<br /><br />SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|OLE DB Driver for SQL Server|Windows Data Access Components, MDAC e<br /><br /> Aplicativos do Driver do OLE DB para SQL Server com DataTypeCompatibility=80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<= 8 KB)|udt|udt|udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|varbinary|Imagem|  
|varchar(max)|varchar|varchar|varchar|Texto|  
|nvarchar(max)|NVARCHAR|NVARCHAR|NVARCHAR|Ntext|  
|Xml|Xml|Xml|Xml|Ntext|  
|CLR UDT (> 8 KB)|varbinary|udt|udt|Imagem|  
|date|varchar|date|date|Varchar|  
|datetime2|varchar|datetime2|datetime2|Varchar|  
|datetimeoffset|varchar|datetimeoffset|datetimeoffset|Varchar|  
|time|varchar|time|time|Varchar|  

## <a name="see-also"></a>Confira também  

[Driver do OLE DB para SQL Server](../oledb/oledb-driver-for-sql-server.md)  
[Instalação do Driver do OLE DB para SQL Server](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
