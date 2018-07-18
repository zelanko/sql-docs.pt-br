---
title: Migrar bancos de dados Sybase ASE para o SQL Server – BD SQL do Azure | Microsoft Docs
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a021ac1cfc442943b15ade737c54d0b9e227ef03
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38982208"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>Migrar bancos de dados do SAP ASE para SQL Server - banco de dados do SQL do Azure (SybaseToSQL)
SQL Server SSMA (Migration Assistant) para o SAP Adaptive Server Enterprise (ASE) é um ambiente abrangente que ajuda você a migrar rapidamente bancos de dados do SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados SQL. Usando o SSMA para SAP ASE, você pode examinar os objetos de banco de dados e dados, avaliar os bancos de dados para a migração, migrar objetos de banco de dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou o banco de dados SQL Azure, e, em seguida, migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados SQL.  
  
## <a name="recommended-migration-process"></a>Processo de migração recomendado  
Para migrar com êxito os objetos e dados de bancos de dados do SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados SQL, use o seguinte processo:  
  
1.  [Criar um novo projeto SSMA](http://msdn.microsoft.com/11091d95-c488-48c3-891a-743cac94ac93).  
  
    Depois de criar o projeto, você pode definir opções de mapeamento de tipo, migração e conversão de projeto. Para obter informações sobre as configurações do projeto, consulte [definir opções do projeto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md). Para obter informações sobre como personalizar mapeamentos de tipo de dados, consulte [mapeamento ASE do Sybase e tipos de dados do SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
2.  [Conectar ao servidor de banco de dados do SAP ASE](http://msdn.microsoft.com/a45a2330-9175-4c9e-af38-ef920e350614).  
  
3.  [Conectar-se a uma instância do SQL Server](http://msdn.microsoft.com/dd368a1a-45b0-40e9-b4d3-5cdb48c26606) ou [conectar-se a uma instância do banco de dados SQL](http://msdn.microsoft.com/9e77e4b0-40c0-455c-8431-ca5d43849aa7).  
  
4.  [Mapear esquemas de banco de dados do SAP ASE para o SQL Server / banco de dados do banco de dados SQL esquemas](http://msdn.microsoft.com/2c927003-c49d-4fe1-8e3e-5b2899166268).  
  
5.  Opcionalmente, [crie relatórios de avaliação](http://msdn.microsoft.com/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c) avaliar os objetos de banco de dados para a conversão e estimar o tempo de conversão.  
  
6.  [Converter esquemas de banco de dados do SAP ASE no SQL Server / esquemas de banco de dados SQL](http://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3).  
  
7.  [Carregar os objetos de banco de dados convertidos no SQL Server / Azure SQL Database](http://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06).  
  
    Ou salvar um script e executá-lo em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados SQL Azure, ou sincronizar os objetos de banco de dados.  
  
8.  [Migrar dados para o SQL Server / Azure SQL Database](http://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
9. Se necessário, atualize seus aplicativos de banco de dados.  
  
## <a name="see-also"></a>Confira também  
[Instalar o SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[Introdução ao SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
