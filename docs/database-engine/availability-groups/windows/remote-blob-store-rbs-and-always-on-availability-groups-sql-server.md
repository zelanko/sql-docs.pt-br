---
title: RBS (Remote BLOB Store) com grupos de disponibilidade
description: 'Uma descrição de como usar o RBS (Remote BLOB Store) com bancos de dados que fazem parte de um Grupo de Disponibilidade AlwaysOn. '
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 01a70258-d4fd-40bc-bc44-c490b5d6c420
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 864ed8080c3978ec272f5212fa0a5e8dc40c2350
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74822484"
---
# <a name="use-remote-blob-store-rbs-with-always-on-availability-groups"></a>Usar o RBS (Remote BLOB Store) com Grupos de Disponibilidade AlwaysOn
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] pode fornecer uma solução de alta disponibilidade e recuperação de desastre para os objetos BLOB (blobs) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][RBS (Remote Blob Store)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md) . [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] protege quaisquer esquemas e metadados RBS armazenados em um banco de dados de disponibilidade replicando-os para as réplicas secundárias. Esse é o banco de dados de conteúdo do SharePoint. Em linhas gerais, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] armazena esses metadados RBS independentemente do blob.  
  
 A proteção para dados BLOB RBS depende do local do repositório de BLOB, da seguinte forma:  
  
|Local do repositório de BLOB|Os grupos de disponibilidade podem proteger esses dados BLOB?|  
|-------------------------|-----------------------------------------------------|  
|O mesmo banco de dados que contém os metadados RBS (armazenados por meio de um provedor remoto FILESTREAM RBS)|Sim|  
|Outro banco de dados na mesma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (armazenado por meio de um provedor remoto FILESTREAM RBS)|Sim<br /><br /> Recomendamos que você coloque esse banco de dados no mesmo grupo de disponibilidade que o banco de dados que contém os metadados RBS.|  
|Outro banco de dados em uma instância diferente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (armazenado por meio de um provedor remoto FILESTREAM RBS)|Sim<br /><br /> Esse banco de dados deve estar em um grupo de disponibilidade separado.|  
|Um repositório de BLOB de terceiros|Não<br /><br /> Para proteger esses dados BLOB, use os mecanismos de alta disponibilidade do provedor de repositório de BLOB.|  
  
##  <a name="limitations"></a><a name="Limitations"></a> Limitações  
  
-   Os mantenedores do RBS precisam ser direcionados para a réplica primária.  
  
##  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Use um ouvinte de grupo de disponibilidade. Para obter mais informações, consulte [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md).  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Maintaining Remote BLOB Store](https://msdn.microsoft.com/library/gg316773\(SQL.105\).aspx) (Mantendo o Remote BLOB Store) (nos Manuais Online do [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] )  
  
-   [Running RBS Maintainer](https://blogs.msdn.com/b/sqlrbs/archive/2010/03/19/running-rbs-maintainer.aspx) (Executando o Mantenedor do RBS) (blog)  
  
-   [Configure Remote BLOB Storage (RBS) with the FILESTREAM provider (SharePoint 2010)](https://blogs.msdn.com/b/mvpawardprogram/archive/2012/04/02/configure-remote-blob-storage-rbs-with-the-filestream-provider-sharepoint-2010.aspx) (Configurar o RBS (Remote BLOB Storage) com o provedor FILESTREAM (SharePoint 2010)) (blog)  
  
## <a name="see-also"></a>Consulte Também  
 [Conectividade de cliente AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)   
 [Remote Blob Store &#40;RBS&#41; &#40;SQL Server&#41;](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
  
