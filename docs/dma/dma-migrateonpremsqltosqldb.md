---
title: Migrar SQL Server no local ou o SQL Server em VMs do Azure para o banco de dados SQL usando o Assistente de migração de dados | Microsoft Docs
description: Saiba como usar o Assistente de migração de dados para migrar um SQL Server no local para o banco de dados SQL
ms.custom: ''
ms.date: 07/15/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: 37e0065ed711c3cf550fec4bafe9aa08be8398e6
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262309"
---
# <a name="migrate-on-premises-sql-server-or-sql-server-on-azure-vms-to-azure-sql-database-using-the-data-migration-assistant"></a>Migrar SQL Server no local ou o SQL Server em VMs do Azure para banco de dados do SQL Azure usando o Assistente de migração de dados

O Assistente de migração de dados fornece perfeitas avaliações do SQL Server local e as atualizações para versões posteriores do SQL Server ou as migrações para o SQL Server em VMs do Azure ou banco de dados SQL.

Este artigo fornece instruções passo a passo para migração do SQL Server local para o banco de dados SQL usando o Assistente de migração de dados.

## <a name="create-a-new-migration-project"></a>Criar um novo projeto de migração

1. No painel esquerdo, selecione **New** (+) e, em seguida, selecione o **migração** tipo de projeto.

2. Defina o tipo de origem como **SQL Server** e o servidor de destino de tipo para **banco de dados SQL**.

3. Selecione **Criar**.

   ![Criar projeto de migração](../dma/media/NewCreate1.png)

## <a name="specify-the-source-server-and-database"></a>Especifique o servidor de origem e o banco de dados

1. Para a fonte, sob **conectar-se ao servidor de origem**, no **nome do servidor** texto, digite o nome da instância do SQL Server de origem.

2. Selecione o **tipo de autenticação** com suporte na instância do SQL Server de origem.

   > [!NOTE]
   > É recomendável que você criptografe a conexão selecionando o **criptografar conexão** caixa de seleção sob **Conexão poperties**.

    ![Selecione o servidor de origem](../dma/media/select-source-server.png)

3. Selecione **Conectar**.

4. Selecione um banco de dados de origem único para migrar para o banco de dados SQL.

   > [!NOTE]
   > Se você gostaria de avaliar o banco de dados e a exibição e aplicar recomendável correções antes da migração, selecione a **banco de dados de avaliação antes da migração?** caixa de seleção.

    ![Selecione o banco de dados de origem](../dma/media/select-source-database.png)

5. Selecione **Avançar**.

## <a name="specify-the-target-server-and-database"></a>Especifique o servidor de destino e o banco de dados

1. Para o destino, sob **conectar ao servidor de destino**, no **nome do servidor** texto, digite o nome da instância do banco de dados SQL. 

2. Selecione o **tipo de autenticação** com suporte na instância de banco de dados SQL de destino.

   > [!NOTE]
   > É recomendável que você criptografe a conexão selecionando o **criptografar conexão** caixa de seleção sob **Conexão poperties**.

     ![Selecione o servidor de destino](../dma/media/select-target-server.png)

3. Selecione **Conectar**.

4. Selecione um banco de dados de destino único para o qual a migração.

   > [!NOTE]
   > Se você pretende migrar usuários do Windows, nos **nome de domínio de usuário externo de destino** texto caixa, certifique-se de que o nome de domínio do usuário externo visem está especificado corretamente.

    ![Selecione o banco de dados de destino](../dma/media/select-target-database.png)

5. Selecione **Avançar**.

## <a name="select-schema-objects"></a>Selecione os objetos de esquema

1. Selecione os objetos de esquema do banco de dados fonte que você deseja migrar para o banco de dados SQL.

    ![Selecione os objetos de esquema](../dma/media/select-schema-objects.png)

       > [!NOTE]
       > Some of the objects that cannot be converted as-is are presented with automatic fix opportunities. Clicking these objects on the left pane displays the suggested fixes on the right pane. Review the fixes and choose to either apply or ignore all changes, object by object. Note that applying or ignoring all changes for one object does not affect changes to other database objects. Statements that cannot be converted or automatically fixed are reproduced to the target database and commented.

    ![Correção sugerida](../dma/media/suggested-fix.png)

2. Selecione **script SQL geral**.

3. Examine o script gerado.

    ![Script gerado](../dma/media/generated-script.png)

## <a name="deploy-schema"></a>Implantar esquema

1. Selecione **implantar esquema**.

2. Examine os resultados da implantação do esquema.

    ![Resultados de implantação de esquema](../dma/media/schema-deployment-results.png)

3. Selecione **migrar dados** para iniciar o processo de migração de dados.

4. Selecione as tabelas com os dados que você deseja migrar.

    ![Selecionar tabelas para migração](../dma/media/select-tables-to-migrate.png) 

5. Selecione **começar a migração de dados**.

A tela final mostra o status geral.

   ![Status da migração](../dma/media/migration-status.png) 

## <a name="see-also"></a>Confira também

* [Assistente de migração de dados (DMA)](../dma/dma-overview.md)
* [Assistente de migração de dados: Definições de configuração](../dma/dma-configurationsettings.md)
* [Assistente de migração de dados: Práticas recomendadas](../dma/dma-bestpractices.md)
