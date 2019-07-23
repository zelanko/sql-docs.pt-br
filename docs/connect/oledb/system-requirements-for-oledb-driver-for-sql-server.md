---
title: Requisitos do sistema para o OLE DB Driver para SQL Server | Microsoft Docs
description: Requisitos do OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 02/12/2019
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
author: pmasl
ms.author: pelopes
ms.openlocfilehash: cec8b2aca53f64e7a3883dbccddce1a330c8a6e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993783"
---
# <a name="system-requirements-for-ole-db-driver-for-sql-server"></a>Requisitos do sistema para o OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  Para usar recursos de acesso a dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como o MARS, você precisa ter este software instalado:  

-   OLE DB driver para SQL Server em seu cliente.  

-   Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em seu servidor.   

> [!NOTE]  
>  Certifique-se de que tenha efetuado logon com privilégios de administrador antes de instalar esse software.  

## <a name="operating-system-requirements"></a>Requisitos do sistema operacional  
 Para obter uma lista de sistemas operacionais que dão suporte ao driver OLE DB para SQL Server, consulte [políticas de suporte para o driver de OLE DB para SQL Server](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md).  

 ## <a name="azure-active-directory-authentication-requirements"></a>Requisitos de autenticação do Azure Active Directory  
 Ao usar Azure Active Directory métodos de autenticação com o driver OLE DB, verifique se o [biblioteca de autenticação do Active Directory para SQL Server](https://go.microsoft.com/fwlink/?LinkID=513072) foi instalado. A ADAL não é necessária para os outros métodos de autenticação ou operações de OLE DB.
Para saber mais, confira [Usar o Azure Active Directory](features/using-azure-active-directory.md).

## <a name="sql-server-requirements"></a>Requisitos do SQL Server  
 Para usar o OLE DB driver para SQL Server acessar dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dado, você deve ter uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada.  

 O [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] dá suporte a conexões de todas as versões do MDAC, do Windows Data Access Components e de todas as versões do OLE DB Driver for SQL Server. Quando uma versão anterior do cliente se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tipos de dados de servidor desconhecidos desse cliente são mapeados para tipos compatíveis com a versão do cliente. Para saber mais, confira [Compatibilidade de tipo de dados para versões do cliente](#data-type-compatibility-for-client-versions).  

## <a name="cross-language-requirements"></a>Requisitos entre idiomas  
 Há suporte para a versão em inglês do driver OLE DB para SQL Server em todas as versões localizadas de sistemas operacionais com suporte. As versões localizadas do driver OLE DB para SQL Server têm suporte em sistemas operacionais localizados que são o mesmo idioma do driver de OLE DB localizado para SQL Server versão. Também há suporte para as versões localizadas do OLE DB Driver for SQL Server nas versões em inglês dos sistemas operacionais compatíveis, desde que as configurações do idioma correspondente estejam instaladas.  

 Para atualizações:  

-   As versões de idioma inglês do driver OLE DB para SQL Server podem ser atualizadas para qualquer versão localizada do driver OLE DB para SQL Server.  

-   Versões localizadas do driver OLE DB para SQL Server podem ser atualizadas para versões localizadas do driver OLE DB para SQL Server do mesmo idioma.  

-   A versão localizada do driver OLE DB para SQL Server pode ser atualizada para a versão em inglês do driver OLE DB para SQL Server.  

-   As versões localizadas do driver de OLE DB para SQL Server não podem ser atualizadas para o driver de OLE DB localizado para versões SQL Server de um idioma localizado diferente.  

## <a name="data-type-compatibility-for-client-versions"></a>Compatibilidade de tipo de dados para versões de cliente  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o OLE DB Driver for SQL Server mapeiam novos tipos de dados para tipos de dados mais antigos que são compatíveis com clientes de nível inferior, conforme mostrado na tabela abaixo.  

 Os aplicativos OLE DB e ADO podem usar a palavra-chave de cadeia de conexão **DataTypeCompatibility** com OLE DB Driver para SQL Server operar com tipos de dados mais antigos. Quando **DataTypeCompatibility=80**, os clientes do OLE DB se conectarão com a versão do protocolo TDS do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], em vez de com a versão TDS. Isso significa que, para o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e tipos de dados posteriores, a conversão de nível inferior será executada pelo servidor, em vez de pelo OLE DB Driver for SQL Server. Isso também significa que os recursos disponíveis na conexão serão limitados ao conjunto de recursos do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. As tentativas de uso de novos tipos de dados ou recursos são detectadas o quanto antes em chamadas API e erros são retornados ao aplicativo da chamada, em vez de se tentar passar solicitações inválidas ao servidor.   


 IDBInfo:: getpalavra-chave sempre retornará uma lista de palavras-chave que corresponde à versão do servidor na conexão e não é afetada pelo **DataTypeCompatibility**.  

|Tipo de dados|SQL Server Native Client<br /><br />SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|OLE DB Driver for SQL Server|Windows Data Access Components, MDAC e<br /><br /> Driver de OLE DB para aplicativos de SQL Server OLE DB com DataTypeCompatibility = 80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<= 8 KB)|udt|udt|udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|varbinary|image|  
|varchar(max)|varchar|varchar|varchar|Texto|  
|nvarchar(max)|NVARCHAR|NVARCHAR|NVARCHAR|Ntext|  
|xml|xml|xml|xml|Ntext|  
|CLR UDT (> 8 KB)|varbinary|udt|udt|image|  
|Data|varchar|Data|Data|Varchar|  
|datetime2|varchar|datetime2|datetime2|Varchar|  
|datetimeoffset|varchar|datetimeoffset|datetimeoffset|Varchar|  
|time|varchar|time|time|Varchar|  

## <a name="see-also"></a>Confira também  
 [OLE DB Driver for SQL Server](../oledb/oledb-driver-for-sql-server.md)   
 [Instalação do Driver do OLE DB para SQL Server](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
