---
title: Mapeando esquemas do ASE do Sybase para esquemas de SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Schema Mapping
ms.assetid: 2c927003-c49d-4fe1-8e3e-5b2899166268
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 212b5719c1ef8bac3e44ec33b786a032acef1d9f
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87865324"
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>Mapear esquemas ASE do Sybase para esquemas do SQL Server (SybaseToSQL)
No Sybase Adaptive Server Enterprise (ASE), cada banco de dados tem um ou mais esquemas. Por padrão, o SSMA migra todos os objetos dentro de um banco de dados e esquema para o mesmo banco de dados e esquema no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. No entanto, você pode personalizar o mapeamento entre os esquemas e bancos de dados do ASE e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure.  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>Esquemas ASE e SQL Server ou SQL Azure  
ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] or SQL Azure especificar bancos de dados e seus esquemas usando a notação de duas partes como *Database. Schema*. Por exemplo, em um banco de dados de **demonstração** do ase, pode haver um esquema **dbo** . Esse par de banco de dados e esquema é especificado como **demo. dbo**. Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure tiver o mesmo banco de dados e esquema, o par também será especificado como **demo. dbo**.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificando o esquema e o banco de dados de destino  
No SSMA, você pode mapear um esquema ASE para qualquer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquema disponível ou SQL Azure.  
  
**Para modificar o banco de dados e o esquema**  
  
1.  No Gerenciador de metadados do Sybase, selecione **bancos de dados**.  
  
    A guia **mapeamento de esquema** também está disponível quando você seleciona um banco de dados individual, a pasta **esquemas** ou esquemas individuais. A lista na guia **mapeamento de esquema** é personalizada para o objeto selecionado.  
  
2.  No painel direito, clique na guia **mapeamento de esquema** .  
  
    Você verá uma lista de todos os bancos de dados ASE com seus esquemas, seguidos por um valor de destino. Esse destino é indicado em uma notação de duas partes (*Database. Schema*) no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure onde seus objetos e dados serão migrados.  
  
3.  Selecione a linha que contém o mapeamento que você deseja alterar e clique em **Modificar**.  
  
4.  Na caixa de diálogo **escolher esquema de destino** , você pode procurar o banco de dados de destino e o esquema disponíveis ou digitar o banco de dados e o nome do esquema na caixa de texto em uma notação de duas partes (Database. Schema) e clicar em **OK**.  
  
5.  O destino é alterado na guia **mapeamento de esquema** .  
  
**Modos de mapeamento**  
  
-   Mapeando para SQL Server  
  
Você pode mapear o banco de dados de origem para qualquer banco de dados de destino. Por padrão, banco de dados de origem é mapeado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o banco de dados de destino com o qual você se conectou usando o SSMA. Se o banco de dados de destino que está sendo mapeado não for existente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você será solicitado com uma mensagem **"o banco de dados e/ou esquema não existe nos metadados de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ele seria criado durante a sincronização. Deseja continuar? "** Clique em Sim. Da mesma forma, você pode mapear o esquema para um esquema não existente no banco de dados de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que será criado durante a sincronização.  
  
-   Mapeando para SQL Azure  
  
Você pode mapear o banco de dados de origem para o destino conectado SQL Azure banco de dados ou para qualquer esquema no banco de dados de SQL Azure de destino conectado. Se você mapear o esquema de origem para qualquer esquema não existente no banco de dados de destino conectado, será exibida uma mensagem **"o esquema não existe nos metadados de destino. Ele seria criado durante a sincronização. Deseja continuar? "** Clique em Sim.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Revertendo para o banco de dados e esquema padrão  
Se você personalizar o mapeamento entre um esquema ASE e um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquema ou SQL Azure, você poderá reverter o mapeamento para os valores padrão.  
  
**Para reverter para o banco de dados e o esquema padrão**  
  
1.  Na guia mapeamento de esquema, selecione qualquer linha e clique em **Redefinir para padrão** para reverter para o banco de dados e o esquema padrão.  
  
## <a name="next-steps"></a>Próximas etapas  
Se você quiser analisar a conversão de objetos do Sybase ASE no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure objetos, poderá [criar um relatório de conversão](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md). Caso contrário, você pode [converter as definições de objeto de banco de dados ase](converting-sybase-ase-database-objects-sybasetosql.md) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure definições de objeto.  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Sybase ASE para o SQL Server-banco de SybaseToSQL SQL do Azure &#40;o&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
