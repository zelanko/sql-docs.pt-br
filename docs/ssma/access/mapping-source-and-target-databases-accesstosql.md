---
title: Mapeando bancos de dados de origem e de destino (AccessToSQL) | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67907152"
---
# <a name="mapping-source-and-target-databases-accesstosql"></a>Mapeando bancos de dados de origem e de destino (AccessToSQL)
Ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, você precisa especificar um banco de dados de destino para migração. Se você tiver vários bancos de dados do Access, você poderá mapeá- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los para vários bancos de dados (ou esquemas) ou para vários esquemas no banco de dados SQL Azure conectado.  
  
## <a name="sql-server-or-sql-azure-database-schemas"></a>SQL Server ou SQL Azure esquemas de banco de dados  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]os bancos de dados usam o conceito de esquemas para separar objetos dentro de um banco de dados em grupos lógicos. Por exemplo, um banco de dados de biblioteca poderia usar três esquemas denominados **livros**, **áudio**e **vídeo** para separar os objetos de livro, áudio e vídeo uns dos outros. Por padrão, o banco de dados do Access é mapeado para o banco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados **mestre** e o esquema **dbo** no e para o banco de dados conectado e o esquema **dbo** no SQL Azure.  
  
A menos que você personalize o mapeamento entre cada banco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados do Access e o banco de dados e o esquema, o SSMA migrará todos os esquemas e dados associados ao banco de dado do Access para o banco de dados padrão mapeado.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificando o esquema e o banco de dados de destino  
O SSMA permite mapear cada banco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados do Access para ou SQL Azure banco de dados e esquema. O procedimento a seguir descreve como personalizar o mapeamento por banco de dados.  
  
**Para modificar o esquema e o banco de dados de destino**  
  
1.  No painel Access Metadata Explorer, selecione **Access-Metadata**.  
  
    O mapeamento de esquema também está disponível quando você seleciona o nó **bancos** de dados ou qualquer nó de banco de dados. A lista de mapeamento de esquema é personalizada para o objeto selecionado.  
  
2.  No painel direito, clique na guia **mapeamento de esquema** .  
  
    Você verá uma tabela que contém nomes de banco de dados de acesso e seu esquema do ssNoVersion ou do SQL Azure correspondente. O esquema de destino é indicado em uma notação de duas partes (Database. Schema).  
  
3.  Selecione a linha que contém o mapeamento que você deseja personalizar e clique em **Modificar**.  
  
4.  Na caixa de diálogo **escolher esquema de destino** , você pode procurar o banco de dados de destino e o esquema disponíveis ou digitar o banco de dados e o nome do esquema na caixa de texto em uma notação de duas partes (Database. Schema) e clicar em **OK**.  
  
**Modos de mapeamento**  
  
-   Mapeando para SQL Server  
  
Você pode mapear o banco de dados de origem para qualquer banco de dados de destino. Por padrão, banco de dados de origem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é mapeado para o banco de dados de destino com o qual você se conectou usando o SSMA. Se o banco de dados de destino que está sendo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]mapeado não existir em, você será solicitado com uma mensagem **"o banco de dados e/ou esquema não existe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nos metadados de destino. Ele seria criado durante a sincronização. Deseja continuar? "** Clique em Sim. Da mesma forma, você pode mapear o esquema para um esquema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não existente no banco de dados de destino que será criado durante a sincronização.  
  
-   Mapeando para SQL Azure  
  
Você pode mapear o banco de dados de origem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o banco de dados de destino conectado ou para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] qualquer esquema no banco de dados de destino conectado. Se você mapear o esquema de origem para qualquer esquema não existente no banco de dados de destino conectado, será exibida uma mensagem **"o esquema não existe nos metadados de destino. Ele seria criado durante a sincronização. Deseja continuar? "** Clique em Sim.  
  
## <a name="reverting-to-your-initial-database-and-schema"></a>Revertendo para o esquema e banco de dados inicial  
Se você personalizar o mapeamento entre um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Access e um banco de dados do ou do SQL Azure e o esquema, poderá reverter o mapeamento de volta para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados que você especificou quando se conectou ao ou SQL Azure.  
  
**Para redefinir para o esquema e banco de dados padrão**  
  
1.  Na guia mapeamento de esquema, selecione qualquer linha e clique em **Redefinir para padrão** para reverter para o banco de dados e o esquema padrão.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [converter objetos de banco de dados](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
