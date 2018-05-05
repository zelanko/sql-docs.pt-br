---
title: Requisitos do sistema para o Driver do OLE DB para SQL Server | Microsoft Docs
description: Requisitos para o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: e109f228d8b902e5c34b4ed5731b80e315fffe3c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="system-requirements-for-ole-db-driver-for-sql-server"></a>Requisitos do sistema para o Driver do OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  Para usar recursos de acesso a dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como o MARS, você precisa ter este software instalado:  

-   OLE DB Driver para SQL Server no seu cliente.  

-   Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em seu servidor.   

> [!NOTE]  
>  Certifique-se de que tenha efetuado logon com privilégios de administrador antes de instalar esse software.  

## <a name="operating-system-requirements"></a>Requisitos do sistema operacional  
 Para obter uma lista dos sistemas operacionais que dão suporte ao Driver do OLE DB para SQL Server, consulte [políticas de suporte do OLE DB Driver for SQL Server](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md).  

## <a name="sql-server-requirements"></a>Requisitos do SQL Server  
 Para usar o Driver do OLE DB para SQL Server para acessar dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados, você deve ter uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado.  

 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] oferece suporte a conexões de todas as versões do MDAC, Windows Data Access Components e todas as versões do Driver do OLE DB para SQL Server. Quando uma versão anterior do cliente se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tipos de dados de servidor desconhecidos desse cliente são mapeados para tipos compatíveis com a versão do cliente. Para obter mais informações, consulte Compatibilidade de tipo de dados para versões do cliente, mais adiante nesse tópico.  

## <a name="cross-language-requirements"></a>Requisitos entre idiomas  
 A versão do idioma inglês do OLE DB Driver for SQL Server é suportada em todas as versões localizadas de sistemas operacionais com suporte. Versões localizadas do OLE DB Driver para SQL Server têm suporte em sistemas operacionais localizados que têm o mesmo idioma que o OLE DB Driver localizado para a versão do SQL Server. Versões localizadas do OLE DB Driver para SQL Server também têm suporte em versões no idioma inglês de sistemas operacionais com suporte, desde que as configurações de idioma correspondente estejam instaladas.  

 Para atualizações:  

-   Versões de idioma inglês do OLE DB Driver for SQL Server podem ser atualizadas para qualquer versão localizada do Driver do OLE DB para SQL Server.  

-   Versões localizadas do OLE DB Driver para SQL Server podem ser atualizadas para versões localizadas do Driver do OLE DB para SQL Server do mesmo idioma.  

-   Versão localizada do OLE DB Driver para SQL Server pode ser atualizado para a versão em inglês do Driver do OLE DB para SQL Server.  

-   Versões localizadas do OLE DB Driver para SQL Server não podem ser atualizadas para OLE DB Driver localizado para versões do SQL Server de um idioma localizado diferente.  

## <a name="data-type-compatibility-for-client-versions"></a>Compatibilidade de tipo de dados para versões de cliente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e OLE DB Driver para SQL Server mapa novos tipos de dados para tipos de dados mais antigos que são compatíveis com clientes de nível inferior, conforme mostrado na tabela a seguir.  

 Aplicativos OLE DB e ADO podem usar o **DataTypeCompatibility** palavra-chave de cadeia de caracteres de conexão com OLE DB para SQL Server para funcionar com os tipos de dados mais antigos. Quando **DataTypeCompatibility = 80**, os clientes de OLE DB se conectarão usando o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] versão (TDS), em vez da versão do protocolo TDS de fluxo de dados tabulares. Isso significa que para [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e tipos de dados mais recente, conversão de nível inferior serão executados pelo servidor, em vez de pelo Driver do OLE DB para SQL Server. Isso também significa que os recursos disponíveis na conexão serão limitados ao conjunto de recursos do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. As tentativas de uso de novos tipos de dados ou recursos são detectadas o quanto antes em chamadas API e erros são retornados ao aplicativo da chamada, em vez de se tentar passar solicitações inválidas ao servidor.   


 IDBInfo::GetKeywords sempre retornará uma lista de palavras-chave que corresponde à versão do servidor em que a conexão e não é afetada por **DataTypeCompatibility**.  

|Tipo de dados|SQL Server Native Client<br /><br />SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Driver do OLE DB para SQL Server|Windows Data Access Components, MDAC e<br /><br /> OLE DB Driver para aplicativos OLE DB do SQL Server com DataTypeCompatibility = 80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<= 8 Kb)|udt|udt|udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|varbinary|image|  
|varchar(max)|varchar|varchar|varchar|Texto|  
|nvarchar(max)|nvarchar|nvarchar|nvarchar|Ntext|  
|xml|xml|xml|xml|Ntext|  
|CLR UDT (> 8Kb)|varbinary|udt|udt|image|  
|date|varchar|date|date|Varchar|  
|datetime2|varchar|datetime2|datetime2|Varchar|  
|datetimeoffset|varchar|datetimeoffset|datetimeoffset|Varchar|  
|time|varchar|time|time|Varchar|  

## <a name="see-also"></a>Consulte também  
 [Driver do OLE DB para SQL Server](../oledb/oledb-driver-for-sql-server.md)   
 [Instalação do Driver do OLE DB para SQL Server](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
