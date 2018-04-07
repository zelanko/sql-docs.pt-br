---
title: Migrando dados do Access para o SQL Server - banco de dados do SQL Azure (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- bulk loading data
- data, loading into SQL Azure
- data, loading into SQL Server
- migrating databases, loading data
- migrating databases, options
- options, migrating data
- SQL Azure, migrating data into
- SQL Server, migrating data into
ms.assetid: f3b18af7-1af0-499d-a00d-a0af94895625
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 937d75eb150a65bf65d1f55c01c5de760f0d36d4
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="migrating-access-data-into-sql-server---azure-sql-db-accesstosql"></a>Migrando dados do Access para o SQL Server - banco de dados do SQL Azure (AccessToSQL)
Depois que você criou com êxito os objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você pode migrar dados de acesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.  
  
## <a name="setting-migration-options"></a>Definindo opções de migração  
Antes de migrar dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure, examine as opções de migração de projeto no **configurações de projeto** caixa de diálogo. Na caixa de diálogo, você pode definir o tamanho de lote de migração, bloqueio de tabela, a restrição de verificação, gatilho de inserção de acionamento, identidade e tratamento de valor nulo e a manipulação de datas que estão fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] intervalo. Para obter mais informações, consulte [configurações do projeto (migração)](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d).  
  
## <a name="migrating-data"></a>Migração de dados  
Migração de dados são uma operação de carregamento em massa que move linhas de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure em transações. O número de linhas a ser carregado em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure em cada transação é configurado nas configurações do projeto.  
  
Para exibir mensagens de migração, verifique se que o painel de saída está visível. Se não estiver, sobre o **exibição** menu, selecione **saída**.  
  
**Para migrar dados**  
  
1.  Verifique se você carregou os objetos de banco de dados do Access em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.  
  
2.  No Gerenciador de metadados de acesso, selecione os objetos que contêm os dados que você deseja migrar:  
  
    -   Para migrar dados para um banco de dados inteiro, marque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para migrar dados de tabelas individuais, expanda o banco de dados, **tabelas**e, em seguida, selecione a caixa de seleção ao lado da tabela. Para omitir os dados de tabelas individuais, desmarque a caixa de seleção.  
  
3.  Clique com botão direito **bancos de dados** e, em seguida, selecione **migrar dados**.  
  
Você também pode migrar dados fora o SSMA usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **bcp** utilitário de linha de comando ou [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)]. Para obter mais informações sobre essas ferramentas, consulte [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="next-step"></a>Próxima etapa  
Se você tiver aplicativos de banco de dados do Access que você deseja continuar a usar após a migração, vincular as tabelas de banco de dados do Access para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou tabelas do SQL Azure. Para obter mais informações, consulte [vinculação aplicativos de acesso ao SQL Server](http://msdn.microsoft.com/en-us/82374ad2-7737-4164-a489-13261ba393d4).  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[Conversão de configuração e opções de migração](http://msdn.microsoft.com/en-us/0a7304df-2f35-4453-96ef-7ac83dea1167)  
  
