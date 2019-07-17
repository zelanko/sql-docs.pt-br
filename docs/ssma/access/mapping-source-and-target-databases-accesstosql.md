---
title: Mapeamento de origem e bancos de dados de destino (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- database schemas
- mapping, databases
- schemas, mapping to
- schemas, SQL Azure
- schemas, SQL Server
- source database
- target database
ms.assetid: 69bee937-7b2c-49ee-8866-7518c683fad4
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 192db2e6c074305ca258d76652351175c8a82751
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907152"
---
# <a name="mapping-source-and-target-databases-accesstosql"></a>Fonte de mapeamento e bancos de dados de destino (AccessToSQL)
Quando você se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, você precisa especificar um banco de dados de destino para migração. Se você tiver vários bancos de dados de acesso você pode mapeá-los a vários [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados (ou esquemas) ou a vários esquemas no banco de dados do SQL Azure conectado.  
  
## <a name="sql-server-or-sql-azure-database-schemas"></a>SQL Server ou esquemas de banco de dados do SQL Azure  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados usam o conceito de esquemas para separar os objetos dentro de um banco de dados em grupos lógicos. Por exemplo, um banco de dados de biblioteca pode usar três esquemas chamados **livros**, **áudio**, e **vídeo** para separar os objetos de catálogo, áudio e vídeo uns dos outros. Por padrão, o banco de dados é mapeado para **mestre** banco de dados e **dbo** esquema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e para o banco de dados conectado e **dbo** esquema no SQL Azure.  
  
A menos que você personalize o mapeamento entre cada banco de dados do Access e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados e esquema, o SSMA migrará todos os esquemas e dados associados com o banco de dados do access para o banco de dados padrão mapeado.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificando o esquema e banco de dados de destino  
O SSMA permite que você mapeie cada banco de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o banco de dados do SQL Azure e o esquema. O procedimento a seguir descreve como personalizar o mapeamento de por banco de dados.  
  
**Para modificar o esquema e banco de dados de destino**  
  
1.  No painel Gerenciador de metadados de acesso, selecione **acessar metadados**.  
  
    Mapeamento de esquema também está disponível quando você seleciona os **bancos de dados** nó ou qualquer nó do banco de dados. A lista de mapeamento de esquema é personalizada para o objeto selecionado.  
  
2.  No painel direito, clique no **esquema de mapeamento** guia.  
  
    Você verá uma tabela contendo acesso nomes de banco de dados e seu ssNoVersion correspondente ou o esquema do Sql Azure. O esquema de destino é indicado em uma notação de duas partes (database.schema).  
  
3.  Selecione a linha que contém o mapeamento que você deseja personalizar e, em seguida, clique em **modificar**.  
  
4.  No **escolha o esquema de destino** caixa de diálogo, você pode navegar para o banco de dados de destino disponíveis e o esquema ou o tipo de banco de dados e esquema de nome na caixa de texto em uma notação de duas partes (database.schema) e, em seguida, clique em **Okey**.  
  
**Modos de mapeamento**  
  
-   Mapeamento para o SQL Server  
  
Você pode mapear o banco de dados de origem para qualquer banco de dados de destino. Por padrão o banco de dados de origem é mapeado para o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados com o qual você se conectou usando o SSMA. Se o banco de dados de destino que está sendo mapeado não existe no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], em seguida, você receberá uma mensagem **"o banco de dados e/ou o esquema não existe no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados. Ele seria criado durante a sincronização. Você deseja continuar?"** Clique em Sim. Da mesma forma, você pode mapear o esquema para o esquema não existente no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados que será criado durante a sincronização.  
  
-   Mapeamento para o SQL Azure  
  
Você pode mapear o banco de dados de origem para o destino conectado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados ou para qualquer esquema de destino conectado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados. Se você mapear esquema de origem para qualquer esquema não existente no banco de dados de destino conectados, você receberá uma mensagem **"esquema não existe nos metadados de destino. Ele seria criado durante a sincronização. Deseja continuar? "** Clique em Sim.  
  
## <a name="reverting-to-your-initial-database-and-schema"></a>Revertendo para seu banco de dados inicial e o esquema  
Se você personalizar o mapeamento entre um banco de dados e uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o banco de dados do SQL Azure e o esquema, você poderá reverter o mapeamento de volta para o banco de dados que você especificou quando conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.  
  
**Para redefinir a esquema e banco de dados padrão**  
  
1.  Na guia mapeamento de esquema, selecione qualquer linha e clique em **Redefinir para padrão** para reverter para o banco de dados padrão e o esquema.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [converter objetos de banco de dados](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
