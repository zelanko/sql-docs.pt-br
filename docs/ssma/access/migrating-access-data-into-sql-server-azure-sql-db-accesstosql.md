---
title: Migrar dados de acesso para o SQL Server – BD SQL do Azure (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
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
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ab3ce18b1b79951c76b34be3f90b2d8782ba64e4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773815"
---
# <a name="migrating-access-data-into-sql-server---azure-sql-db-accesstosql"></a>Migrar dados de acesso para o SQL Server – BD SQL do Azure (AccessToSQL)
Depois que você criou com êxito os objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode migrar dados de acesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.  
  
## <a name="setting-migration-options"></a>Definindo opções de migração  
Antes de migrar dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure, examine as opções de migração de projeto na **configurações do projeto** caixa de diálogo. Na caixa de diálogo, você pode definir o tamanho do lote de migração, bloqueio de tabela, a restrição de verificação, o gatilho de inserção disparando, identidade e o valor null de tratamento e como lidar com as datas que estão fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intervalo. Para obter mais informações, consulte [configurações do projeto (migração)](http://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d).  
  
## <a name="migrating-data"></a>Migração de dados  
Migração de dados são uma operação de carregamento em massa que move as linhas de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure em transações. O número de linhas a serem carregados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure em cada transação é configurado nas configurações do projeto.  
  
Para exibir mensagens de migração, verifique se que o painel de saída está visível. Se não, é sobre o **modo de exibição** menu, selecione **saída**.  
  
**Para migrar dados**  
  
1.  Verifique se você carregou os objetos de banco de dados do Access em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.  
  
2.  No Gerenciador de metadados de acesso, selecione os objetos que contêm os dados que você deseja migrar:  
  
    -   Para migrar dados para um banco de dados inteiro, marque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para migrar dados de tabelas individuais, expanda o banco de dados, expanda **tabelas**e, em seguida, selecione a caixa de seleção ao lado da tabela. Para omitir dados de tabelas individuais, desmarque a caixa de seleção.  
  
3.  Clique com botão direito **bancos de dados** e, em seguida, selecione **migrar dados**.  
  
Você também pode migrar dados fora do SSMA usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bcp** utilitário de linha de comando ou [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Para obter mais informações sobre essas ferramentas, consulte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
## <a name="next-step"></a>Próxima etapa  
Se você tiver aplicativos de banco de dados de acesso que você deseja continuar a usar após a migração, vincular as tabelas de banco de dados do Access para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou tabelas do SQL Azure. Para obter mais informações, consulte [vinculação de aplicativos de acesso ao SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Conversão de configuração e opções de migração](setting-conversion-and-migration-options-accesstosql.md)  
  
