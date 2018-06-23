---
title: Requisitos de sistema do SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- system requirements [SQL Server Native Client]
- data access [SQL Server Native Client], system requirements
- SQL Server Native Client, system requirements
- SQLNCLI, system requirements
ms.assetid: 1c8e2f8a-a440-44da-8e3a-af632d34c52c
caps.latest.revision: 60
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 87ec4582047abd6742756e1764d95c9f7d751061
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010667"
---
# <a name="system-requirements-for-sql-server-native-client"></a>Requisitos do sistema do SQL Server Native Client
  Para usar recursos de acesso a dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como o MARS, você precisa ter este software instalado:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client em seu cliente.  
  
-   Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em seu servidor.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client exige o Windows Installer 3.0. O Windows Installer 3.0 já está instalado nos sistemas operacionais [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Para todas as outras plataformas, é preciso instalá-lo explicitamente. Para obter mais informações, consulte [Windows Installer 3.0 redistribuível](http://go.microsoft.com/fwlink/?LinkId=46459).  
  
> [!NOTE]  
>  Certifique-se de que tenha efetuado logon com privilégios de administrador antes de instalar esse software.  
  
## <a name="operating-system-requirements"></a>Requisitos do sistema operacional  
 Para obter uma lista dos sistemas operacionais que oferecem suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, consulte [políticas de suporte do SQL Server Native Client](applications/support-policies-for-sql-server-native-client.md).  
  
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
  
 Aplicativos OLE DB e ADO podem usar a palavra-chave da cadeia de conexão `DataTypeCompatibility` com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para operar com tipos de dados mais antigos. Quando `DataTypeCompatibility=80`, os clientes OLE DB se conectarão com a versão TDS do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], em vez de com a versão do TDS. Isso significa que, para o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e tipos de dados posteriores, a conversão de nível inferior será executada pelo servidor, e não pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Isso também significa que os recursos disponíveis na conexão serão limitados ao conjunto de recursos do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. As tentativas de uso de novos tipos de dados ou recursos são detectadas o quanto antes em chamadas API e erros são retornados ao aplicativo da chamada, em vez de se tentar passar solicitações inválidas ao servidor.  
  
 Não há controle `DataTypeCompatibility` para ODBC.  
  
 IDBInfo::GetKeywords sempre retornará uma lista de palavras-chave que corresponde à versão do servidor em que a conexão e não é afetada por `DataTypeCompatibility`.  
  
|Tipo de dados|SQL Server Native Client<br /><br /> SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Windows Data Access Components, MDAC e<br /><br /> Aplicativos OLE DB do SQL Server Native Client com DataTypeCompatibility=80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<= 8 Kb)|udt|Udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|image|  
|varchar(max)|varchar|varchar|Texto|  
|nvarchar(max)|NVARCHAR|NVARCHAR|Ntext|  
|xml|xml|xml|Ntext|  
|CLR UDT (> 8Kb)|udt|varbinary|image|  
|Data|Data|varchar|Varchar|  
|datetime2|datetime2|varchar|Varchar|  
|datetimeoffset|datetimeoffset|varchar|Varchar|  
|time|time|varchar|Varchar|  
  
## <a name="see-also"></a>Consulte também  
 [Programação do SQL Server Native Client](sql-server-native-client-programming.md)   
 [Instalando o SQL Server Native Client](applications/installing-sql-server-native-client.md)  
  
  