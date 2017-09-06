---
title: Migrar bancos de dados do Access para o SQL Server - banco de dados SQL do Azure | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 08/15/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
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
author: sabotta
ms.author: carlasab
manager: murato
ms.translationtype: MT
ms.sourcegitcommit: e4a6157cb56c6db911406585f841046a431eef99
ms.openlocfilehash: 5f5a567fba47be944dcf02f2facd2253d7852e88
ms.contentlocale: pt-br
ms.lasthandoff: 08/16/2017

---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>Migrando bancos de dados do Access para o SQL Server - banco de dados do SQL do Azure (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Assistente de migração (SSMA) é uma ferramenta que fornece um ambiente abrangente que ajuda a migrar rapidamente bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Usando o SSMA, você pode revisar o acesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure objetos de banco de dados, avaliar o banco de dados para a migração, converter objetos de banco de dados do Access, carregá-los em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure, e, em seguida, migrar dados.  
  
## <a name="recommended-migration-process"></a>Processo de migração recomendado  
Para migrar com êxito os objetos e dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure, use o seguinte processo:  
  
1.  [Criar um novo projeto SSMA](http://msdn.microsoft.com/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7). Depois de criar o projeto, você pode [definir opções de projeto](http://msdn.microsoft.com/0a7304df-2f35-4453-96ef-7ac83dea1167), incluindo opções de conversão, opções de migração e mapeamentos de tipo de dados.  
  
2.  [Adicionar arquivos de banco de dados do Access](http://msdn.microsoft.com/e944c740-4c8a-4bc1-b0ed-be57bc06dced) ao projeto.  
  
    Você pode adicionar arquivos individuais, incluindo arquivos que encontrar no computador ou rede.  
  
3.  [Conectar-se à instância de destino do SQL Server](http://msdn.microsoft.com/f84cf007-ddf1-4396-a07c-3e0729abc769) ou [conectar-se à instância de destino do SQL Azure](http://msdn.microsoft.com/1ba0d113-dc05-4431-8689-e14a8821bafd).  
  
    Você pode se conectar para SQL Server ou SQL Azure.  
  
4.  Para personalizar o mapeamento entre um ou mais bancos de dados do Access e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou esquemas do SQL Azure, [mapear os bancos de dados de origem e destino](http://msdn.microsoft.com/69bee937-7b2c-49ee-8866-7518c683fad4).  
  
5.  Opcionalmente, você pode [criar um relatório de avaliação](http://msdn.microsoft.com/8b9e23d6-da62-437a-8c05-8ad2628b9441) para determinar se os objetos de banco de dados do Access podem ser convertidos com êxito em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.  
  
6.  [Converter objetos de banco de dados do Access](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou definições de objeto do SQL Azure.  
  
7.  [Carregar os objetos de banco de dados convertido no SQL Server](http://msdn.microsoft.com/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba).  
  
    Você pode carregar os objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure usando o SSMA, ou você pode salvar [!INCLUDE[tsql](../../includes/tsql_md.md)] scripts.  
  
8.  [Migrar dados do Access para o SQL Server](http://msdn.microsoft.com/f3b18af7-1af0-499d-a00d-a0af94895625).  
  
    > [!NOTE]  
    > Você pode converter, carregar e migrar esquemas e dados em uma única etapa. Para executar a migração de um único clique, clique o **converter, carregar e migrar** botão.  
  
9. Se quiser que seus aplicativos de acesso para usar os dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure, use [vincular as tabelas do Access às tabelas do SQL Server](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4).  
  
Você também pode usar o Assistente de migração para orientar você durante esse processo. Para obter mais informações, consulte [Assistente de migração](http://msdn.microsoft.com/5bab5914-b2ae-4795-8cf5-83e42d64bef2).  
  
## <a name="see-also"></a>Consulte também  
[Introdução ao Assistente de migração do SQL Server para Access](http://msdn.microsoft.com/462a731f-08f1-44e1-9eeb-4deac6d2f6c5)  
[Preparar bancos de dados do Access para a migração](http://msdn.microsoft.com/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)
