---
title: Requisitos do sistema para o OLE DB Driver for SQL Server | Microsoft Docs
description: Requisitos do OLE DB Driver for SQL Server
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
- system requirements [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], system requirements
- OLE DB Driver for SQL Server, system requirements
- MSOLEDBSQL, system requirements
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 718f9d7f7739fde0577420e03137ef6caeab4747
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43024127"
---
# <a name="system-requirements-for-ole-db-driver-for-sql-server"></a>Requisitos do sistema para o OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  Para usar recursos de acesso a dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como o MARS, você precisa ter este software instalado:  

-   Driver do OLE DB para SQL Server no seu cliente.  

-   Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em seu servidor.   

> [!NOTE]  
>  Certifique-se de que tenha efetuado logon com privilégios de administrador antes de instalar esse software.  

## <a name="operating-system-requirements"></a>Requisitos do sistema operacional  
 Para obter uma lista dos sistemas operacionais que dão suporte ao Driver do OLE DB para SQL Server, consulte [políticas de suporte para o Driver do OLE DB para SQL Server](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md).  

## <a name="sql-server-requirements"></a>Requisitos do SQL Server  
 Para usar o Driver do OLE DB para SQL Server para acessar dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados, você deve ter uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado.  

 O [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] dá suporte a conexões de todas as versões do MDAC, do Windows Data Access Components e de todas as versões do OLE DB Driver for SQL Server. Quando uma versão anterior do cliente se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tipos de dados de servidor desconhecidos desse cliente são mapeados para tipos compatíveis com a versão do cliente. Para obter mais informações, consulte Compatibilidade de tipo de dados para versões do cliente, mais adiante nesse tópico.  

## <a name="cross-language-requirements"></a>Requisitos entre idiomas  
 A versão do idioma inglês do Driver do OLE DB para SQL Server é suportada em todas as versões localizadas de sistemas operacionais com suporte. As versões localizadas do Driver do OLE DB para SQL Server têm suporte em sistemas operacionais localizados que têm o mesmo idioma, como o localizada Driver do OLE DB para a versão do SQL Server. Também há suporte para as versões localizadas do OLE DB Driver for SQL Server nas versões em inglês dos sistemas operacionais compatíveis, desde que as configurações do idioma correspondente estejam instaladas.  

 Para atualizações:  

-   Versões de idioma inglês do Driver do OLE DB para SQL Server podem ser atualizadas a qualquer versão localizada do Driver do OLE DB para SQL Server.  

-   As versões localizadas do Driver do OLE DB para SQL Server podem ser atualizadas para versões localizadas do Driver do OLE DB para SQL Server no mesmo idioma.  

-   Versão localizada do Driver do OLE DB para SQL Server pode ser atualizado para a versão do idioma inglês do Driver do OLE DB para SQL Server.  

-   As versões localizadas do Driver do OLE DB para SQL Server não podem ser atualizadas para localizada Driver do OLE DB para SQL Server versões de um idioma localizado diferente.  

## <a name="data-type-compatibility-for-client-versions"></a>Compatibilidade de tipo de dados para versões de cliente  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o OLE DB Driver for SQL Server mapeiam novos tipos de dados para tipos de dados mais antigos que são compatíveis com clientes de nível inferior, conforme mostrado na tabela abaixo.  

 Aplicativos OLE DB e ADO podem usar o **DataTypeCompatibility** palavra-chave de cadeia de caracteres de conexão com o Driver do OLE DB para SQL Server operar com tipos de dados mais antigos. Quando **DataTypeCompatibility=80**, os clientes do OLE DB se conectarão com a versão do protocolo TDS do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], em vez de com a versão TDS. Isso significa que, para o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e tipos de dados posteriores, a conversão de nível inferior será executada pelo servidor, em vez de pelo OLE DB Driver for SQL Server. Isso também significa que os recursos disponíveis na conexão serão limitados ao conjunto de recursos do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. As tentativas de uso de novos tipos de dados ou recursos são detectadas o quanto antes em chamadas API e erros são retornados ao aplicativo da chamada, em vez de se tentar passar solicitações inválidas ao servidor.   


 IDBInfo::GetKeywords sempre retornará uma lista de palavra-chave que corresponde à versão do servidor em que a conexão e não é afetada pelas **DataTypeCompatibility**.  

|Tipo de dados|SQL Server Native Client<br /><br />SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|OLE DB Driver for SQL Server|Windows Data Access Components, MDAC e<br /><br /> Driver do OLE DB para aplicativos OLE DB do SQL Server com Datatypecompatibility=80 = 80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<= 8Kb)|udt|udt|udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|varbinary|image|  
|varchar(max)|varchar|varchar|varchar|Texto|  
|nvarchar(max)|NVARCHAR|NVARCHAR|NVARCHAR|Ntext|  
|xml|xml|xml|xml|Ntext|  
|CLR UDT (> 8Kb)|varbinary|udt|udt|image|  
|Data|varchar|Data|Data|Varchar|  
|datetime2|varchar|datetime2|datetime2|Varchar|  
|datetimeoffset|varchar|datetimeoffset|datetimeoffset|Varchar|  
|time|varchar|time|time|Varchar|  

## <a name="see-also"></a>Consulte Também  
 [OLE DB Driver for SQL Server](../oledb/oledb-driver-for-sql-server.md)   
 [Instalação do Driver do OLE DB para SQL Server](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
