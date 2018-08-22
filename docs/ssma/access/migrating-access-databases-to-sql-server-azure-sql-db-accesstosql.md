---
title: Migrar bancos de dados Access para o SQL Server – BD SQL do Azure | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- instructions, migration
- migrating databases, overview
- overview, migration process
- procedure, migration
- recommended migration process
ms.assetid: 76a3abcf-2998-4712-9490-fe8d872c89ca
caps.latest.revision: 23
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: f3552b4617d4579be7beebccae357b417ea6a563
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393776"
---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>Migrando bancos de dados do Access para o SQL Server – BD SQL do Azure (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de migração (SSMA) é uma ferramenta que fornece um ambiente abrangente que ajuda você a migrar rapidamente bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Usando o SSMA, você pode examinar o acesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure objetos de banco de dados, avaliar o banco de dados do Access para a migração, converta objetos de banco de dados do Access, carregá-los em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, e, em seguida, migrar dados.  
  
## <a name="recommended-migration-process"></a>Processo de migração recomendado  
Para migrar com êxito os objetos e dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, use o seguinte processo:  
  
1.  [Criar um novo projeto SSMA](creating-and-managing-projects-accesstosql.md). Depois de criar o projeto, você pode [definir opções de projeto](setting-conversion-and-migration-options-accesstosql.md), incluindo opções de conversão, as opções de migração e mapeamentos de tipo de dados.  
  
2.  [Adicionar arquivos de banco de dados do Access](adding-and-removing-access-database-files-accesstosql.md) ao projeto.  
  
    Você pode adicionar arquivos individuais, incluindo os arquivos que você encontrar no computador ou na rede.  
  
3.  [Conectar-se a instância de destino do SQL Server](connecting-to-sql-server-accesstosql.md) ou [conectar-se a instância de destino do SQL Azure](connecting-to-azure-sql-db-accesstosql.md).  
  
    Você pode se conectar ao SQL Server ou SQL Azure.  
  
4.  Para personalizar o mapeamento entre um ou mais bancos de dados do Access e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas do SQL Azure, ou [mapear os bancos de dados de origem e destino](mapping-source-and-target-databases-accesstosql.md).  
  
5.  Opcionalmente, você pode [criar um relatório de avaliação](assessing-access-database-objects-for-conversion-accesstosql.md) para determinar se os objetos de banco de dados de acesso podem ser convertidos com êxito para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.  
  
6.  [Converter objetos de banco de dados do Access](converting-access-database-objects-accesstosql.md) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou definições de objeto do SQL Azure.  
  
7.  [Carregar os objetos de banco de dados convertidos no SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md).  
  
    Você pode carregar os objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure usando o SSMA, ou você pode salvar [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts.  
  
8.  [Migrar dados do Access para o SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md).  
  
    > [!NOTE]  
    > Você pode converter, carregar e migrar esquemas e dados em uma única etapa. Para executar a migração de um clique, clique o **converter, carregar e migrar** botão.  
  
9. Se você deseja que seus aplicativos de acesso para usar os dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure, use [vincular as tabelas do Access às tabelas do SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md).  
  
Você também pode usar o Assistente de migração para orientá-lo por meio desse processo. Para obter mais informações, consulte [Assistente de migração](migration-wizard-accesstosql.md).  
  
## <a name="see-also"></a>Confira também  
[Introdução ao Assistente de migração do SQL Server para Access](getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[Preparar bancos de dados de acesso para a migração](preparing-access-databases-for-migration-accesstosql.md)
