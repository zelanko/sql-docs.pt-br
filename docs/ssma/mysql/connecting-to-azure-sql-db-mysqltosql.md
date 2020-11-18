---
description: Conectando-se ao banco de dados SQL do Azure (MySQLToSQL)
title: Conectando-se ao banco de dados SQL do Azure (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 11/16/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to Azure SQL Database, SQL Azure permissions
- Connecting to Azure SQL Database, synchronization
ms.assetid: d0b6f16a-1880-459d-a0c7-28b7ef15c56a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 6604d35058c9e8876638beee3ec6d73a9cd7a491
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870084"
---
# <a name="connecting-to-azure-sql-database-mysqltosql"></a>Conectando-se ao banco de dados SQL do Azure (MySQLToSQL)

Para migrar bancos de dados MySQL para [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] o, você deve se conectar à instância de destino do [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] . Quando você se conecta, o SSMA obtém metadados sobre todos os bancos de dados na instância do [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] e exibe os metadados do banco de dados no **Gerenciador de metadados do banco de dados SQL do Azure**. O SSMA armazena informações da instância do à [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] qual você está conectado, mas não armazena senhas.

Sua conexão [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] permanecerá ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] se quiser uma conexão ativa com o servidor. Você pode trabalhar offline até carregar os objetos de banco [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] de dados no e migrar.

Os metadados sobre a instância do [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] não são sincronizados automaticamente. Em vez disso, para atualizar os metadados no **Gerenciador de metadados do banco de dados SQL do Azure**, você deve atualizar os [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] metadados manualmente. Para obter mais informações, consulte a seção "sincronizando metadados do banco de dados SQL do Azure" mais adiante neste tópico.

## <a name="required-azure-sql-database-permissions"></a>Permissões necessárias do banco de dados SQL do Azure

A conta usada para se conectar ao [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] requer permissões diferentes dependendo das ações que a conta executa:

- Para converter objetos MySQL em [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe, atualizar metadados do [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ou salvar a sintaxe convertida em scripts, a conta deve ter permissão para fazer logon na instância do [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] .

- Para carregar objetos de banco de dados no [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] , a conta deve ser membro da função de banco de dados **db_ddladmin** .

- Para migrar dados para [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] o, a conta deve ser um membro da função de banco de dado **db_owner** .

## <a name="establishing-an-azure-sql-database-connection"></a>Estabelecendo uma conexão de banco de dados SQL do Azure

Antes de converter objetos do banco de dados MySQL em [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] sintaxe, você deve estabelecer uma conexão com a instância do [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] em que você deseja migrar o banco de dados MySQL ou bancos.

Ao definir as propriedades de conexão, você também especifica o banco de dados em que os objetos e data serão migrados. Você pode personalizar esse mapeamento no nível de esquema do MySQL depois de se conectar ao [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] . Para obter mais informações, consulte [mapeando bancos de dados MySQL para esquemas de SQL Server &#40;&#41;MySQLToSQL ](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md).

> [!IMPORTANT]
> Antes de tentar se conectar ao [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] , verifique se o endereço IP é permitido por meio do [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] Firewall.

Para conectar-se ao [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]:

1. No menu **arquivo** , selecione **conectar ao banco de dados SQL do Azure** (essa opção é habilitada após a criação de um projeto).
   Se você tiver se conectado anteriormente ao [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] , o nome do comando será **reconectado ao banco de dados SQL do Azure**.

2. Na caixa de diálogo conexão, insira ou selecione o nome do servidor de [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] .

3. Insira, selecione ou **procure** o nome do banco de dados.

4. Insira ou selecione o **nome de usuário**.

5. Insira a **senha**.

6. O SSMA recomenda a conexão criptografada com o [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] .

7. Clique em **Conectar**.
  
## <a name="synchronizing-azure-sql-database-metadata"></a>Sincronizando metadados do banco de dados SQL do Azure

Metadados sobre bancos de dados no [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] não são atualizados automaticamente. Os metadados no **Gerenciador de metadados do banco de dados SQL do Azure** são um instantâneo dos metadados quando você se conecta pela primeira vez ao [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] , ou na última atualização dos metadados. Você pode atualizar os metadados manualmente para todos os bancos de dados ou para qualquer banco de dados ou objeto de banco de dados individual. Para sincronizar metadados:

1. Certifique-se de que você está conectado ao [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] .

2. No **Gerenciador de metadados do banco de dados SQL do Azure**, marque a caixa de seleção ao lado do banco de dados ou esquema de banco de dados que você deseja atualizar.
   Por exemplo, para atualizar os metadados de todos os bancos de dados, selecione a caixa ao lado de **bancos de dados**.

3. Clique com o botão direito do mouse em **bancos** de dados ou em um esquema ou banco de dados individual e selecione **sincronizar com Banco de dados**.

## <a name="next-step"></a>Próxima etapa

A próxima etapa na migração depende de suas necessidades de projeto:

- Para personalizar o mapeamento entre os esquemas do MySQL e o [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] , consulte [mapeando bancos de dados mysql para SQL Server esquemas &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md).
- Para personalizar as opções de configuração para os projetos, consulte [definindo opções de projeto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md).
- Para personalizar o mapeamento de tipos de dados de origem e de destino, consulte [mapeando MySQL e SQL Server tipos de dados &#40;&#41;MySQLToSQL ](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md).
- Se você não precisar executar nenhuma dessas tarefas, poderá converter as definições do objeto de banco de dados MySQL em [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] definições de objeto. Para obter mais informações, consulte [convertendo bancos de dados MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md).

## <a name="see-also"></a>Consulte Também

[Migrando bancos de dados MySQL para SQL Server-banco de MySQLToSql SQL do Azure &#40;&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)
