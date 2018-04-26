---
title: Mapeando esquemas Sybase ASE para esquemas SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
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
- Schema Mapping
ms.assetid: 2c927003-c49d-4fe1-8e3e-5b2899166268
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fd5d975a3dced6f19cf867c453469d25f727912a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>Mapeando Sybase ASE esquemas para esquemas SQL Server (SybaseToSQL)
Em Sybase Adaptive Server Enterprise (ASE), cada banco de dados tem um ou mais esquemas. Por padrão, o SSMA migra todos os objetos em um banco de dados e o esquema para o mesmo banco de dados e esquema [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. No entanto, você pode personalizar o mapeamento entre ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou bancos de dados do SQL Azure e esquemas.  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>ASE e do SQL Server ou SQL Azure esquemas  
ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure especificar bancos de dados e seus esquemas usando a notação de parte dois como *database.schema*. Por exemplo, em uma ASE **demonstração** banco de dados, pode haver um **dbo** esquema. Se o par de banco de dados e esquema é especificado como **demo.dbo**. Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure tem o mesmo banco de dados e o esquema, o par também é especificado como **demo.dbo**.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificando o esquema e banco de dados de destino  
No SSMA, você pode mapear um esquema ASE para qualquer disponível [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou esquema do SQL Azure.  
  
**Para modificar o banco de dados e o esquema**  
  
1.  No Gerenciador de metadados do Sybase, selecione **bancos de dados**.  
  
    O **mapeamento de esquema** guia também está disponível quando você seleciona um banco de dados individual, o **esquemas** pasta ou esquemas individuais. Na lista de **esquema de mapeamento** guia personalizada para o objeto selecionado.  
  
2.  No painel direito, clique no **mapeamento de esquema** guia.  
  
    Você verá uma lista de todos os bancos de dados de ASE com seus esquemas, seguidos por um valor de destino. Esse destino é indicado em uma notação de duas partes (*database.schema*) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure em que seus objetos e os dados serão migrados.  
  
3.  Selecione a linha que contém o mapeamento que você deseja alterar e, em seguida, clique em **modificar**.  
  
4.  No **esquema de destino escolha** caixa de diálogo, você pode navegar para o banco de dados de destino disponíveis e o esquema ou o tipo de banco de dados e esquema de nome na caixa de texto em uma notação de duas partes (database.schema) e, em seguida, clique em **Okey**.  
  
5.  O destino é alterado no **mapeamento de esquema** guia.  
  
**Modos de mapeamento**  
  
-   Mapeamento para o SQL Server  
  
Você pode mapear o banco de dados de origem para qualquer banco de dados de destino. Por padrão o banco de dados de origem é mapeado para o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados com o qual você se conectou usando o SSMA. Se o banco de dados de destino que está sendo mapeado é inexistente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], em seguida, você receberá uma mensagem **"o banco de dados e/ou o esquema não existe no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] metadados. Ele deve ser criado durante a sincronização. Deseja continuar?"** Clique em Sim. Da mesma forma, você pode mapear o esquema para o esquema não existente no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados que será criado durante a sincronização.  
  
-   Mapeamento para o SQL Azure  
  
Você pode mapear o banco de dados de origem para o banco de dados do SQL Azure de destino conectado ou para qualquer esquema no banco de dados do SQL Azure destino conectado. Se você mapear o esquema de origem nenhum esquema não existente no banco de dados de destino conectados, você receberá uma mensagem **"esquema não existe nos metadados de destino. Ele deve ser criado durante a sincronização. Deseja continuar? "** Clique em Sim.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Revertendo para o banco de dados padrão e o esquema  
Se você personalizar o mapeamento entre um esquema ASE e um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou esquema do SQL Azure, você poderá reverter o mapeamento de volta para os valores padrão.  
  
**Para reverter para o banco de dados padrão e o esquema**  
  
1.  Na guia mapeamento de esquema, selecione qualquer linha e clique em **Redefinir para padrão** para reverter para o banco de dados padrão e o esquema.  
  
## <a name="next-steps"></a>Próximas etapas  
Se você deseja analisar a conversão de objetos do Sybase ASE em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos do SQL Azure, você pode [criar um relatório de conversão](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c). Caso contrário, você pode [converter as definições de objeto de banco de dados ASE](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou definições de objeto do SQL Azure.  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados Sybase ASE para o SQL Server - banco de dados SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
