---
title: Migrar bancos de dados do Access para o SQL Server-BD SQL do Azure | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- instructions, migration
- migrating databases, overview
- overview, migration process
- procedure, migration
- recommended migration process
ms.assetid: 76a3abcf-2998-4712-9490-fe8d872c89ca
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 959af9bcb1879dc19d2bfb99253b4c40d637fd1e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68260240"
---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>Migrando bancos de dados do Access para o SQL Server – BD SQL do Azure (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O Assistente de Migração (SSMA) é uma ferramenta que fornece um ambiente abrangente que ajuda você a migrar rapidamente bancos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados do Access para o ou o SQL Azure. Usando o SSMA, você pode examinar o acesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ou SQL Azure objetos de banco de dados, avaliar o banco de dados do Access para migração, converter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos de banco de dados do Access, carregá-los em ou SQL Azure e, em seguida, migrar dados.  
  
## <a name="recommended-migration-process"></a>Processo de migração recomendado  
Para migrar com êxito objetos e dados do acesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao ou SQL Azure, use o seguinte processo:  
  
1.  [Crie um novo projeto do SSMA](creating-and-managing-projects-accesstosql.md). Depois de criar o projeto, você pode [definir opções de projeto](setting-conversion-and-migration-options-accesstosql.md), incluindo opções de conversão, opções de migração e mapeamentos de tipo de dados.  
  
2.  [Adicione arquivos de banco de dados do Access](adding-and-removing-access-database-files-accesstosql.md) ao projeto.  
  
    Você pode adicionar arquivos individuais, incluindo arquivos que você encontrar no computador ou na rede.  
  
3.  [Conecte-se à instância de destino do SQL Server](connecting-to-sql-server-accesstosql.md) ou [Conecte-se à instância de destino do SQL Azure](connecting-to-azure-sql-db-accesstosql.md).  
  
    Você pode se conectar a SQL Server ou SQL Azure.  
  
4.  Para personalizar o mapeamento entre um ou mais bancos de dados do Access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ou SQL Azure esquemas, [mapeie os bancos de dados de origem e de destino](mapping-source-and-target-databases-accesstosql.md).  
  
5.  Opcionalmente, você pode [criar um relatório de avaliação](assessing-access-database-objects-for-conversion-accesstosql.md) para determinar se os objetos de banco de dados do Access podem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ser convertidos com êxito ou SQL Azure.  
  
6.  [Converter objetos de banco](converting-access-database-objects-accesstosql.md) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados de acesso para ou SQL Azure definições de objeto.  
  
7.  [Carregue os objetos de banco de dados convertidos em SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md).  
  
    Você pode carregar os objetos de banco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados no ou SQL Azure usando o SSMA ou pode salvar [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts.  
  
8.  [Migre dados do Access para o SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md).  
  
    > [!NOTE]  
    > Você pode converter, carregar e migrar esquemas e dados em uma única etapa. Para executar a migração com um clique, clique no botão **converter, carregar e migrar** .  
  
9. Se você quiser que seus aplicativos do Access usem os dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ou SQL Azure, use [vincular as tabelas do Access às tabelas do SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md).  
  
Você também pode usar o assistente de migração para orientá-lo nesse processo. Para obter mais informações, consulte [Migration Wizard](migration-wizard-accesstosql.md).  
  
## <a name="see-also"></a>Confira também  
[Introdução com Assistente de Migração do SQL Server para acesso](getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[Preparar bancos de dados do Access para migração](preparing-access-databases-for-migration-accesstosql.md)
