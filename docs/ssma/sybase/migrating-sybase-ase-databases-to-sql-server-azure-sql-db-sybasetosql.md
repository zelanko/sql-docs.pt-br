---
title: Migrar bancos de dados de ASE do Sybase para o SQL Server-Azure SQL Database | Microsoft Docs
description: Use esse processo recomendado para migrar bancos de dados corporativos do SAP Adaptive Server para o SQL Server ou o Azure SQL Database usando o Assistente de Migração do SQL Server (SSMA).
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: e0a938d615b15dc7b280a6c6b9337a546e0059bf
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934654"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>Migrando bancos de dados do SAP ASE para o SQL Server-SybaseToSQL (Azure SQL Database)
O Assistente de Migração do SQL Server (SSMA) para SAP Adaptive Server Enterprise (ASE) é um ambiente abrangente que ajuda você a migrar rapidamente bancos de dados do SAP ASE para o ou para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure SQL Database. Usando o SSMA para SAP ASE, você pode examinar os objetos e os dados do banco de dados, avaliar os bancos de dado para migração, migrar objetos de banco de dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Azure SQL Database e, em seguida, migrar dados para o ou para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure.  
  
## <a name="recommended-migration-process"></a>Processo de migração recomendado  
Para migrar com êxito objetos e dados de bancos de dado SAP ASE para o ou para o banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL do Azure, use o seguinte processo:  
  
1.  [Crie um novo projeto do SSMA](working-with-ssma-projects-sybasetosql.md).  
  
    Depois de criar o projeto, você pode definir opções de conversão de projeto, migração e mapeamento de tipo. Para obter informações sobre configurações de projeto, consulte [definindo opções de projeto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md). Para obter informações sobre como personalizar mapeamentos de tipo de dados, consulte [mapeando Sybase ase e SQL Server tipos de dados &#40;&#41;SybaseToSQL ](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
2.  [Conecte-se ao servidor de banco de dados SAP ase](connecting-to-sybase-ase-sybasetosql.md).  
  
3.  [Conecte-se a uma instância do SQL Server](connecting-to-sql-server-sybasetosql.md) ou [Conecte-se a uma instância do banco de dados SQL do Azure](connecting-to-azure-sql-db-sybasetosql.md).  
  
4.  [Mapeie esquemas de banco de dados SAP ase para SQL Server/esquemas de banco de dados do banco de dados SQL do Azure](https://msdn.microsoft.com/2c927003-c49d-4fe1-8e3e-5b2899166268).  
  
5.  Opcionalmente, [Crie relatórios de avaliação](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md) para avaliar objetos de banco de dados para conversão e estimar o tempo de conversão.  
  
6.  [Converta esquemas de banco de dados do SAP ASE em esquemas de banco de dados SQL do SQL Server/Azure](https://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3).  
  
7.  [Carregue os objetos de banco de dados convertidos em SQL Server/banco de dados SQL do Azure](https://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06).  
  
    Salve um script e execute-o no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou no banco de dados SQL do Azure ou sincronize os objetos de banco de dados.  
  
8.  [Migre dados para o SQL Server/banco de dado SQL do Azure](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
9. Se necessário, atualize seus aplicativos de banco de dados.  
  
## <a name="see-also"></a>Consulte também  
[Instalando o SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[Introdução com o SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
