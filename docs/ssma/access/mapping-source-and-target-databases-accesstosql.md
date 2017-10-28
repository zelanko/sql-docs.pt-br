---
title: Mapeamento de origem e bancos de dados de destino (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- database schemas
- mapping, databases
- schemas, mapping to
- schemas, SQL Azure
- schemas, SQL Server
- source database
- target database
ms.assetid: 69bee937-7b2c-49ee-8866-7518c683fad4
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8bc9bde868aa615c2e78ace576394a9d1f782e3e
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="mapping-source-and-target-databases-accesstosql"></a>Mapeamento de origem e bancos de dados de destino (AccessToSQL)
Quando você se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, é necessário especificar um banco de dados de destino para migração. Se você tiver vários bancos de dados do Access mapeá-los a vários [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bancos de dados (ou esquemas) ou para vários esquemas no banco de dados do SQL Azure conectado.  
  
## <a name="sql-server-or-sql-azure-database-schemas"></a>SQL Server ou esquemas de banco de dados do Azure SQL  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]bancos de dados usam o conceito de esquemas para separar os objetos dentro de um banco de dados em grupos lógicos. Por exemplo, um banco de dados de biblioteca pode usar três esquemas chamados **manuais**, **áudio**, e **vídeo** para separar os objetos de áudio e vídeo do catálogo, uns dos outros. Por padrão, o banco de dados é mapeado para **mestre** banco de dados e **dbo** esquema [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e ao banco de dados conectado e **dbo** esquema no SQL Azure.  
  
A menos que você personalize o mapeamento entre cada banco de dados do Access e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados e esquema, o SSMA migrará todos os esquemas e dados associados com o banco de dados para o banco de dados mapeado.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificando o esquema e banco de dados de destino  
O SSMA permite que você mapeie cada banco de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou o banco de dados do SQL Azure e o esquema. O procedimento a seguir descreve como personalizar o mapeamento por banco de dados.  
  
**Para modificar o banco de dados de destino e o esquema**  
  
1.  No painel Explorador de metadados de acesso, selecione **acessar metadados**.  
  
    Mapeamento de esquema também está disponível quando você seleciona o **bancos de dados** nó ou qualquer banco de dados. A lista de mapeamento de esquema é personalizada para o objeto selecionado.  
  
2.  No painel direito, clique no **mapeamento de esquema** guia.  
  
    Você verá uma tabela contendo acesso nomes de banco de dados e seu ssNoVersion correspondente ou o esquema do Sql Azure. O esquema de destino é indicado em uma notação de duas partes (database.schema).  
  
3.  Selecione a linha que contém o mapeamento que você deseja personalizar e, em seguida, clique em **modificar**.  
  
4.  No **esquema de destino escolha** caixa de diálogo, você pode navegar para o banco de dados de destino disponíveis e o esquema ou o tipo de banco de dados e esquema de nome na caixa de texto em uma notação de duas partes (database.schema) e, em seguida, clique em **Okey**.  
  
**Modos de mapeamento**  
  
-   Mapeamento para o SQL Server  
  
Você pode mapear o banco de dados de origem para qualquer banco de dados de destino. Por padrão o banco de dados de origem é mapeado para o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados com o qual você se conectou usando o SSMA. Se o banco de dados de destino que está sendo mapeado não existe no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], em seguida, você receberá uma mensagem **"o banco de dados e/ou o esquema não existe no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] metadados. Ele deve ser criado durante a sincronização. Deseja continuar?"** Clique em Sim. Da mesma forma, você pode mapear o esquema para o esquema não existente no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados que será criado durante a sincronização.  
  
-   Mapeamento para o SQL Azure  
  
Você pode mapear o banco de dados de origem para o destino conectado [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados ou para qualquer esquema no destino conectado [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados. Se você mapear o esquema de origem nenhum esquema não existente no banco de dados de destino conectados, você receberá uma mensagem **"esquema não existe nos metadados de destino. Ele deve ser criado durante a sincronização. Deseja continuar? "** Clique em Sim.  
  
## <a name="reverting-to-your-initial-database-and-schema"></a>Revertendo para o banco de dados inicial e o esquema  
Se você personalizar o mapeamento entre um banco de dados e um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou o banco de dados do SQL Azure e o esquema, você poderá reverter o mapeamento de volta para o banco de dados que você especificou quando conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.  
  
**Para redefinir a esquema e banco de dados padrão**  
  
1.  Na guia mapeamento de esquema, selecione qualquer linha e clique em **Redefinir para padrão** para reverter para o banco de dados padrão e o esquema.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [converter objetos de banco de dados](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  

