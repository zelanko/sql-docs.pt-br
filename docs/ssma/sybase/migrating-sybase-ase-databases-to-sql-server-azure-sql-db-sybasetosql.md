---
title: Migrar bancos de dados Sybase ASE para o SQL Server – BD SQL do Azure | Microsoft Docs
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 96ade7125c0d03963e8e012ed72bdb8fdef492cf
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51662345"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>Migrar bancos de dados do SAP ASE para SQL Server - banco de dados do SQL do Azure (SybaseToSQL)
SQL Server SSMA (Migration Assistant) para o SAP Adaptive Server Enterprise (ASE) é um ambiente abrangente que ajuda você a migrar rapidamente bancos de dados do SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL. Usando o SSMA para SAP ASE, você pode examinar os objetos de banco de dados e dados, avaliar os bancos de dados para a migração, migrar objetos de banco de dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o banco de dados SQL Azure, e, em seguida, migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL.  
  
## <a name="recommended-migration-process"></a>Processo de migração recomendado  
Para migrar com êxito os objetos e dados de bancos de dados do SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL, use o seguinte processo:  
  
1.  [Criar um novo projeto SSMA](working-with-ssma-projects-sybasetosql.md).  
  
    Depois de criar o projeto, você pode definir opções de mapeamento de tipo, migração e conversão de projeto. Para obter informações sobre as configurações do projeto, consulte [definir opções do projeto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md). Para obter informações sobre como personalizar mapeamentos de tipo de dados, consulte [mapeamento ASE do Sybase e tipos de dados do SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
2.  [Conectar ao servidor de banco de dados do SAP ASE](connecting-to-sybase-ase-sybasetosql.md).  
  
3.  [Conectar-se a uma instância do SQL Server](connecting-to-sql-server-sybasetosql.md) ou [conectar-se a uma instância do banco de dados SQL](connecting-to-azure-sql-db-sybasetosql.md).  
  
4.  [Mapear esquemas de banco de dados do SAP ASE para o SQL Server / banco de dados do banco de dados SQL esquemas](https://msdn.microsoft.com/2c927003-c49d-4fe1-8e3e-5b2899166268).  
  
5.  Opcionalmente, [crie relatórios de avaliação](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md) avaliar os objetos de banco de dados para a conversão e estimar o tempo de conversão.  
  
6.  [Converter esquemas de banco de dados do SAP ASE no SQL Server / esquemas de banco de dados SQL](https://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3).  
  
7.  [Carregar os objetos de banco de dados convertidos no SQL Server / Azure SQL Database](https://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06).  
  
    Ou salvar um script e executá-lo em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL Azure, ou sincronizar os objetos de banco de dados.  
  
8.  [Migrar dados para o SQL Server / Azure SQL Database](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
9. Se necessário, atualize seus aplicativos de banco de dados.  
  
## <a name="see-also"></a>Confira também  
[Instalar o SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[Introdução ao SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
