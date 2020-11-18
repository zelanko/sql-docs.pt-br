---
description: Conectando-se ao banco de dados SQL do Azure (SybaseToSQL)
title: Conectando-se ao banco de dados SQL do Azure (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: f88b7b5357a61708910846f78c09f80e7c783957
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870410"
---
# <a name="connecting-to-azure-sql-database-sybasetosql"></a>Conectando-se ao banco de dados SQL do Azure (SybaseToSQL)

Para migrar bancos de dados Sybase para [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] o, você deve se conectar à instância de destino do [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] . Quando você se conecta, o SSMA obtém metadados sobre todos os bancos de dados na instância do [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] e exibe os metadados do banco de dados no **Gerenciador de metadados do banco de dados SQL do Azure**. O SSMA armazena informações da instância do à [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] qual você está conectado, mas não armazena senhas.

Sua conexão [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] permanecerá ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] se quiser uma conexão ativa com o servidor. Você pode trabalhar offline até carregar os objetos de banco [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] de dados no e migrar.

Os metadados sobre a instância do [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] não são sincronizados automaticamente. Em vez disso, para atualizar os metadados no **Gerenciador de metadados do banco de dados SQL do Azure**, você deve atualizar os [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] metadados manualmente. Para obter mais informações, consulte a seção "sincronizando metadados do banco de dados SQL do Azure" mais adiante neste tópico.

## <a name="required-azure-sql-database-permissions"></a>Permissões necessárias do banco de dados SQL do Azure

A conta usada para se conectar ao [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] requer permissões diferentes dependendo das ações que a conta executa:

- Para converter objetos do ASE em [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe, atualizar metadados do [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ou salvar a sintaxe convertida em scripts, a conta deve ter permissão para fazer logon na instância do [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] .

- Para carregar objetos de banco de dados no [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] , a conta deve ser membro da função de banco de dados **db_ddladmin** .

- Para migrar dados para [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] o, a conta deve ser um membro da função de banco de dado **db_owner** .

- Para executar o código gerado pelo SSMA, a conta deve ter `EXECUTE` permissões para todas as funções definidas pelo usuário no esquema de **ssma_syb** do banco de dados de destino. Essas funções fornecem funcionalidade equivalente às funções do sistema ASE e são usadas por objetos convertidos.

## <a name="establishing-an-azure-sql-database-connection"></a>Estabelecendo uma conexão de banco de dados SQL do Azure

Antes de converter objetos de banco de dados Sybase em [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] sintaxe, você deve estabelecer uma conexão com a instância do [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] onde você deseja migrar o banco de dados ou bancos de dados Sybase.

Ao definir as propriedades de conexão, você também especifica o banco de dados em que os objetos e data serão migrados. Você pode personalizar esse mapeamento no nível de esquema do Sybase depois de se conectar ao banco de dados SQL do Azure. Para obter mais informações, consulte [mapeando esquemas do ase do Sybase para esquemas de SQL Server &#40;&#41;SybaseToSQL ](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).

> [!IMPORTANT]
> Antes de tentar se conectar ao [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] , verifique se o endereço IP é permitido por meio do [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] Firewall.

Para conectar-se ao [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]:

1. No menu **arquivo** , selecione **conectar ao banco de dados SQL do Azure**(essa opção é habilitada após a criação de um projeto).
   Se você tiver se conectado anteriormente ao [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] , o nome do comando será **reconectado ao banco de dados SQL do Azure**.

2. Na caixa de diálogo conexão, insira ou selecione o nome do servidor de [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] .

3. Insira, selecione ou **procure** o nome do banco de dados.

4. Insira ou selecione o **nome de usuário**.

5. Insira a **senha**.

6. O SSMA recomenda a conexão criptografada com o [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] .

7. Clique em **Conectar**.

## <a name="synchronizing-azure-sql-database-metadata"></a>Sincronizando metadados do banco de dados SQL do Azure

Metadados sobre [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] bancos de dados não são atualizados automaticamente. Os metadados no Gerenciador de metadados do banco de dados SQL do Azure são um instantâneo dos metadados quando você se conecta pela primeira vez ao banco de dados SQL do Azure ou na última vez que você atualizou os metadados. Você pode atualizar os metadados manualmente para todos os bancos de dados ou para qualquer banco de dados ou objeto de banco de dados individual. Para sincronizar metadados:

1. Certifique-se de que você está conectado ao [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] .

2. No **Gerenciador de metadados do banco de dados SQL do Azure**, marque a caixa de seleção ao lado do banco de dados ou esquema de banco de dados que você deseja atualizar.
   Por exemplo, para atualizar os metadados de todos os bancos de dados, selecione a caixa ao lado de **bancos de dados**.

3. Clique com o botão direito do mouse em **bancos** de dados ou em um esquema ou banco de dados individual e selecione **sincronizar com Banco de dados**.

## <a name="next-step"></a>Próxima etapa

A próxima etapa na migração depende de suas necessidades de projeto:

- Para personalizar o mapeamento entre esquemas e bancos de [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] dados e esquemas do Sybase, consulte [mapeando esquemas do ase do sybase para SQL Server esquemas &#40;&#41;do SybaseToSQL ](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).
- Para personalizar as opções de configuração para os projetos, consulte [definindo opções de projeto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md).
- Para personalizar o mapeamento de tipos de dados de origem e de destino, consulte [mapeando Sybase ase e SQL Server tipos de dados &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).
- Se você não precisar executar nenhuma dessas tarefas, poderá converter as definições de objeto do banco de dados Sybase em [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] definições de objeto. Para obter mais informações, consulte [convertendo objetos de banco de dados do Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).

## <a name="see-also"></a>Consulte Também

[Migrando bancos de dados do Sybase ASE para o SQL Server-banco de SybaseToSQL SQL do Azure &#40;o&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)
