---
description: Migrando dados do Access para o SQL Server – banco de AccessToSQL (Azure SQL Database)
title: Migrando dados do Access para o SQL Server – banco de AccessToSQL (Azure SQL Database) | Microsoft Docs
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: cc1cdb31969eb94c29a6c58f974aef92c5cdfc62
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988647"
---
# <a name="migrating-access-data-into-sql-server---azure-sql-database-accesstosql"></a>Migrando dados do Access para o SQL Server – banco de AccessToSQL (Azure SQL Database)
Depois de ter criado com êxito os objetos de banco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados no, você pode migrar de acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.  
  
## <a name="setting-migration-options"></a>Definindo opções de migração  
Antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o ou SQL Azure, examine as opções de migração do projeto na caixa de diálogo **configurações do projeto** . Nessa caixa de diálogo, você pode definir o tamanho do lote de migração, o bloqueio de tabela, a verificação de restrição, o acionamento do gatilho de inserção, a manipulação de valor de identidade e de nulo e como lidar com datas fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intervalo. Para obter mais informações, consulte [configurações do projeto (migração)](./project-settings-migration-accesstosql.md).  
  
## <a name="migrating-data"></a>Migrando dados  
A migração de dados é uma operação de carregamento em massa que move linhas de dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure em transações. O número de linhas a serem carregadas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure em cada transação é definido nas configurações do projeto.  
  
Para exibir as mensagens de migração, verifique se o painel de saída está visível. Se não estiver, no menu **Exibir** , selecione **saída**.  
  
**Para migrar dados**  
  
1.  Verifique se você carregou os objetos de banco de dados do Access no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.  
  
2.  No Gerenciador de metadados do Access, selecione os objetos que contêm os dados que você deseja migrar:  
  
    -   Para migrar dados para um banco de dado inteiro, marque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para migrar dados de tabelas individuais, expanda o banco de dado, expanda **tabelas**e marque a caixa de seleção ao lado da tabela. Para omitir dados de tabelas individuais, desmarque a caixa de seleção.  
  
3.  Clique com o botão direito do mouse em **bancos** de dados e selecione **migrar data**.  
  
Você também pode migrar dados fora do SSMA usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utilitário de linha de comando **bcp** ou [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações sobre essas ferramentas, consulte os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] manuais online do.  
  
## <a name="next-step"></a>Próxima etapa  
Se você tiver aplicativos de banco de dados do Access que deseja continuar a usar após a migração, vincule as tabelas de banco de dados do Access às [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas ou SQL Azure. Para obter mais informações, consulte [vinculando aplicativos de acesso ao SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md).  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Definindo opções de conversão e migração](setting-conversion-and-migration-options-accesstosql.md)  
