---
description: Requisitos do sistema do SQL Server Native Client
title: Requisitos de sistema
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- system requirements [SQL Server Native Client]
- data access [SQL Server Native Client], system requirements
- SQL Server Native Client, system requirements
- SQLNCLI, system requirements
ms.assetid: 1c8e2f8a-a440-44da-8e3a-af632d34c52c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c3a96191f072a0b5b5a5e0c216f5a21cae023aca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448236"
---
# <a name="system-requirements-for-sql-server-native-client"></a>Requisitos do sistema do SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Para usar recursos de acesso a dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como o MARS, você precisa ter este software instalado:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client em seu cliente.  
  
-   Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em seu servidor.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client exige o Windows Installer 3.0. O Windows Installer 3.0 já está instalado nos sistemas operacionais [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Para todas as outras plataformas, é preciso instalá-lo explicitamente. Para obter mais informações, consulte [Windows Installer 3,0 redistribuível](https://www.microsoft.com/download/details.aspx?id=16821).  
  
> [!NOTE]  
>  Certifique-se de que tenha efetuado logon com privilégios de administrador antes de instalar esse software.  
  
## <a name="operating-system-requirements"></a>Requisitos do Sistema Operacional  
 Para obter uma lista de sistemas operacionais que dão suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cliente nativo, consulte [políticas de suporte para SQL Server Native Client](../../relational-databases/native-client/applications/support-policies-for-sql-server-native-client.md).  
  
## <a name="sql-server-requirements"></a>Requisitos do SQL Server  
 Para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para acessar dados em bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você precisa ter uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada.  
  
 O [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] dá suporte a conexões de todas as versões do MDAC, do Windows Data Access Components e de todas as versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Quando uma versão anterior do cliente se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tipos de dados de servidor desconhecidos desse cliente são mapeados para tipos compatíveis com a versão do cliente. Para obter mais informações, consulte Compatibilidade de tipo de dados para versões do cliente, mais adiante nesse tópico.  
  
## <a name="cross-language-requirements"></a>Requisitos entre idiomas  
 A versão em inglês do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client tem suporte em todas as versões localizadas de sistemas operacionais suportados. As versões localizadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client têm suporte nos sistemas operacionais localizados que têm o mesmo idioma que a versão localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. As versões localizadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client também são suportadas nas versões em inglês dos sistemas operacionais suportados, desde que as configurações do idioma correspondente estejam instaladas.  
  
 Para atualizações:  
  
-   Versões em inglês do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client podem ser atualizadas para qualquer versão localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
-   Versões localizadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client podem ser atualizadas para versões localizadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no mesmo idioma.  
  
-   A versão localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client pode ser atualizada para a versão em inglês do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
-   Versões localizadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client não podem ser atualizadas para versões localizadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client em um idioma localizado diferente.  
  
## <a name="data-type-compatibility-for-client-versions"></a>Compatibilidade de tipo de dados para versões de cliente  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client mapeiam tipos de dados novos para tipos de dados mais antigos que são compatíveis com clientes de níveis inferiores, conforme mostrado na tabela abaixo.  
  
 Os aplicativos OLE DB e ADO podem usar a palavra-chave de cadeia de conexão **DataTypeCompatibility** com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para operar com tipos de dados mais antigos. Quando **DataTypeCompatibility=80**, os clientes do OLE DB se conectarão com a versão do protocolo TDS do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], em vez de com a versão TDS. Isso significa que, para o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e tipos de dados posteriores, a conversão de nível inferior será executada pelo servidor, e não pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Isso também significa que os recursos disponíveis na conexão serão limitados ao conjunto de recursos do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. As tentativas de uso de novos tipos de dados ou recursos são detectadas o quanto antes em chamadas API e erros são retornados ao aplicativo da chamada, em vez de se tentar passar solicitações inválidas ao servidor.  
  
 Não há nenhum controle **DataTypeCompatibility** para o ODBC.  
  
 IDBInfo::GetKeywords sempre retornará uma lista de palavras-chave que corresponde à versão de servidor na conexão e não é afetada por **DataTypeCompatibility**.  
  
|Tipo de dados|SQL Server Native Client<br /><br /> SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Windows Data Access Components, MDAC e<br /><br /> Aplicativos OLE DB do SQL Server Native Client com DataTypeCompatibility=80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<= 8Kb)|udt|Udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|Imagem|  
|varchar(max)|varchar|varchar|Texto|  
|nvarchar(max)|NVARCHAR|NVARCHAR|Ntext|  
|Xml|Xml|Xml|Ntext|  
|CLR UDT (> 8 KB)|udt|varbinary|Imagem|  
|date|date|varchar|Varchar|  
|datetime2|datetime2|varchar|Varchar|  
|datetimeoffset|datetimeoffset|varchar|Varchar|  
|time|time|varchar|Varchar|  
  
## <a name="see-also"></a>Consulte Também  
 [Programação de SQL Server Native Client](../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [Instalando o SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
  
