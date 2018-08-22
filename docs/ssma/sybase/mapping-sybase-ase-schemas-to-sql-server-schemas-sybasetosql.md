---
title: Mapear esquemas ASE do Sybase para esquemas do SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Schema Mapping
ms.assetid: 2c927003-c49d-4fe1-8e3e-5b2899166268
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7d0f5e75e487b17873a49df25cbf4b4b359ea82b
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394583"
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>Mapear esquemas ASE do Sybase para esquemas do SQL Server (SybaseToSQL)
No Sybase Adaptive Server Enterprise (ASE), cada banco de dados tem um ou mais esquemas. Por padrão, o SSMA migra todos os objetos dentro de um banco de dados e esquema para o mesmo banco de dados e esquema em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. No entanto, você pode personalizar o mapeamento entre o ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou bancos de dados do SQL Azure e esquemas.  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>ASE e o SQL Server ou SQL Azure esquemas  
ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure especificar bancos de dados e seus esquemas usando a notação de parte dois como *database.schema*. Por exemplo, em um ASE **demonstração** do banco de dados, pode haver um **dbo** esquema. Que o par de banco de dados e esquema é especificado como **demo.dbo**. Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure tem o mesmo banco de dados e o esquema, o par também é especificado como **demo.dbo**.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificando o esquema e banco de dados de destino  
No SSMA, você pode mapear um esquema de ASE para alguma disponível [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o esquema do SQL Azure.  
  
**Para modificar o esquema e banco de dados**  
  
1.  No Gerenciador de metadados do Sybase, selecione **bancos de dados**.  
  
    O **esquema de mapeamento** guia também está disponível quando você seleciona um banco de dados individual, o **esquemas** pasta ou esquemas individuais. Na lista de **esquema de mapeamento** guia personalizada para o objeto selecionado.  
  
2.  No painel direito, clique no **esquema de mapeamento** guia.  
  
    Você verá uma lista de todos os bancos de dados do ASE com seus esquemas, seguidos por um valor de destino. Este destino é indicado em uma notação de duas partes (*database.schema*) no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure no qual seus objetos e dados serão migrados.  
  
3.  Selecione a linha que contém o mapeamento que você deseja alterar e, em seguida, clique em **modificar**.  
  
4.  No **escolha o esquema de destino** caixa de diálogo, você pode navegar para o banco de dados de destino disponíveis e o esquema ou o tipo de banco de dados e esquema de nome na caixa de texto em uma notação de duas partes (database.schema) e, em seguida, clique em **Okey**.  
  
5.  O destino é alterado na **esquema de mapeamento** guia.  
  
**Modos de mapeamento**  
  
-   Mapeamento para o SQL Server  
  
Você pode mapear o banco de dados de origem para qualquer banco de dados de destino. Por padrão o banco de dados de origem é mapeado para o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados com o qual você se conectou usando o SSMA. Se o banco de dados de destino que está sendo mapeado é não existente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], em seguida, você receberá uma mensagem **"o banco de dados e/ou o esquema não existe no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados. Ele seria criado durante a sincronização. Você deseja continuar?"** Clique em Sim. Da mesma forma, você pode mapear o esquema para o esquema não existente no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados que será criado durante a sincronização.  
  
-   Mapeamento para o SQL Azure  
  
Você pode mapear o banco de dados de origem para o banco de dados do SQL Azure de destino conectados ou para qualquer esquema no banco de dados SQL Azure de destino conectados. Se você mapear esquema de origem para qualquer esquema não existente no banco de dados de destino conectados, você receberá uma mensagem **"esquema não existe nos metadados de destino. Ele seria criado durante a sincronização. Deseja continuar? "** Clique em Sim.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Revertendo para o banco de dados padrão e o esquema  
Se você personalizar o mapeamento entre um esquema de ASE e um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o esquema do SQL Azure, você poderá reverter o mapeamento de volta para os valores padrão.  
  
**Para reverter para o banco de dados padrão e o esquema**  
  
1.  Na guia mapeamento de esquema, selecione qualquer linha e clique em **Redefinir para padrão** para reverter para o banco de dados padrão e o esquema.  
  
## <a name="next-steps"></a>Próximas etapas  
Se você deseja analisar a conversão de objetos do Sybase ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos do SQL Azure, você pode [criar um relatório de conversão](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md). Caso contrário, você pode [converter as definições de objeto de banco de dados ASE](converting-sybase-ase-database-objects-sybasetosql.md) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou definições de objeto do SQL Azure.  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Sybase ASE para o SQL Server – BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
