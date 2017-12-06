---
title: Migrar bancos de dados Sybase ASE para o SQL Server - banco de dados SQL do Azure | Microsoft Docs
ms.custom: 
ms.date: 11/30/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e9b4f48de979d4ce1949842bb173a1ee08202d15
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>Migrar bancos de dados do SAP ASE para o SQL Server - banco de dados do SQL do Azure (SybaseToSQL)
Migração Assistente SSMA (SQL Server) para o SAP Adaptive Server Enterprise (ASE) é um ambiente abrangente que ajuda a migrar rapidamente bancos de dados SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados do SQL Azure. Usando o SSMA para SAP ASE, você pode examinar os dados e objetos de banco de dados, avaliar bancos de dados para migração, migrar objetos de banco de dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados SQL Azure, e, em seguida, migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados do SQL Azure.  
  
## <a name="recommended-migration-process"></a>Processo de migração recomendado  
Para migrar com êxito os objetos e dados de bancos de dados SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados SQL, use o seguinte processo:  
  
1.  [Criar um novo projeto SSMA](http://msdn.microsoft.com/en-us/11091d95-c488-48c3-891a-743cac94ac93).  
  
    Depois de criar o projeto, você pode definir opções de mapeamento de tipo, a migração e a conversão de projeto. Para obter informações sobre configurações de projeto, consulte [definindo opções de projeto &#40; SybaseToSQL &#41; ](../../ssma/sybase/setting-project-options-sybasetosql.md). Para obter informações sobre como personalizar mapeamentos de tipo de dados, consulte [mapeamento Sybase ASE e tipos de dados do SQL Server &#40; SybaseToSQL &#41; ](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
2.  [Conectar ao servidor de banco de dados do SAP ASE](http://msdn.microsoft.com/en-us/a45a2330-9175-4c9e-af38-ef920e350614).  
  
3.  [Conectar a uma instância do SQL Server](http://msdn.microsoft.com/en-us/dd368a1a-45b0-40e9-b4d3-5cdb48c26606) ou [conectar-se a uma instância do banco de dados do SQL Azure](http://msdn.microsoft.com/en-us/9e77e4b0-40c0-455c-8431-ca5d43849aa7).  
  
4.  [Mapear os esquemas de banco de dados do SAP ASE para o SQL Server / banco de dados do banco de dados do SQL Azure esquemas](http://msdn.microsoft.com/en-us/2c927003-c49d-4fe1-8e3e-5b2899166268).  
  
5.  Opcionalmente, [criar relatórios de avaliação](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c) para avaliar os objetos de banco de dados para a conversão e estimar o tempo de conversão.  
  
6.  [Converter os esquemas de banco de dados do SAP ASE em SQL Server / esquemas de banco de dados do Azure SQL](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3).  
  
7.  [Carregar os objetos de banco de dados convertido no SQL Server / banco de dados do SQL Azure](http://msdn.microsoft.com/en-us/4c59256f-99a8-4351-9559-a455813dbd06).  
  
    Ou salvar um script e executá-lo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados SQL Azure, ou sincronizar os objetos de banco de dados.  
  
8.  [Migrar dados para o SQL Server / banco de dados do SQL Azure](http://msdn.microsoft.com/en-us/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
9. Se necessário, atualize seus aplicativos de banco de dados.  
  
## <a name="see-also"></a>Consulte também  
[Instalando o SSMA para SAP ASE &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[Guia de Introdução com o SSMA para SAP ASE &#40; SybaseToSQL &#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
