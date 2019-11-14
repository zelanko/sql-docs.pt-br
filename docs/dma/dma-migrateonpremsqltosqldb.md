---
title: Migrar SQL Server para o banco de dados SQL do Azure usando o Assistente de Migração de Dados
description: Saiba como usar Assistente de Migração de Dados para migrar um SQL Server local para o banco de dados SQL do Azure
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
ms.custom: seo-lt-2019
ms.openlocfilehash: cc87b541b2b6ebf2f6a9068ba35ae0f62f8e9988
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056610"
---
# <a name="migrate-on-premises-sql-server-or-sql-server-on-azure-vms-to-azure-sql-database-using-the-data-migration-assistant"></a>Migrar SQL Server locais ou SQL Server em VMs do Azure para o banco de dados SQL do Azure usando o Assistente de Migração de Dados

O Assistente de Migração de Dados fornece avaliações diretas de SQL Server locais e atualizações para versões posteriores de SQL Server ou migrações para SQL Server em VMs do Azure ou banco de dados SQL do Azure.

Este artigo fornece instruções passo a passo para migrar SQL Server no local para o banco de dados SQL do Azure usando o Assistente de Migração de Dados.

## <a name="create-a-new-migration-project"></a>Criar um novo projeto de migração

1. No painel esquerdo, selecione **novo** (+) e, em seguida, selecione o tipo de projeto de **migração** .

2. Defina o tipo de fonte como **SQL Server** e o tipo de servidor de destino como **banco de dados SQL do Azure**.

3. Selecione **Criar**.

   ![Criar projeto de migração](../dma/media/NewCreate1.png)

## <a name="specify-the-source-server-and-database"></a>Especificar o servidor de origem e o banco de dados

1. Para a origem, em **conectar-se ao servidor de origem**, na caixa de texto **nome do servidor** , digite o nome da instância de SQL Server de origem.

2. Selecione o **tipo de autenticação** com suporte na instância de SQL Server de origem.

   > [!NOTE]
   > É recomendável criptografar a conexão marcando a caixa de seleção **criptografar conexão** em **poperties de conexão**.

    ![Selecionar servidor de origem](../dma/media/select-source-server.png)

3. Selecione **Conectar**.

4. Selecione um banco de dados de origem único para migrar para o banco de dados SQL do Azure.

   > [!NOTE]
   > Se você quiser avaliar o banco de dados e exibir e aplicar as correções recomendadas antes da migração, marque a caixa de seleção **avaliar o banco de dados antes da migração?** .

    ![Selecionar Banco de dados de origem](../dma/media/select-source-database.png)

5. Selecione **Avançar**.

## <a name="specify-the-target-server-and-database"></a>Especificar o servidor de destino e o banco de dados

1. Para o destino, em **conectar ao servidor de destino**, na caixa de texto **nome do servidor** , digite o nome da instância do banco de dados SQL do Azure. 

2. Selecione o **tipo de autenticação** com suporte na instância de banco de dados SQL do Azure de destino.

   > [!NOTE]
   > É recomendável criptografar a conexão marcando a caixa de seleção **criptografar conexão** em **poperties de conexão**.

     ![Selecionar servidor de destino](../dma/media/select-target-server.png)

3. Selecione **Conectar**.

4. Selecione um único banco de dados de destino para o qual deseja migrar.

   > [!NOTE]
   > Se você pretende migrar usuários do Windows, na caixa de texto **nome de domínio de usuário externo de destino** , verifique se o nome de domínio do usuário externo meta está especificado corretamente.

    ![Selecionar Banco de dados de destino](../dma/media/select-target-database.png)

5. Selecione **Avançar**.

## <a name="select-schema-objects"></a>Selecionar objetos de esquema

1. Selecione os objetos de esquema do banco de dados de origem que você deseja migrar para o banco de dados SQL do Azure.

    ![Selecionar objetos de esquema](../dma/media/select-schema-objects.png)

       > [!NOTE]
       > Some of the objects that cannot be converted as-is are presented with automatic fix opportunities. Clicking these objects on the left pane displays the suggested fixes on the right pane. Review the fixes and choose to either apply or ignore all changes, object by object. Note that applying or ignoring all changes for one object does not affect changes to other database objects. Statements that cannot be converted or automatically fixed are reproduced to the target database and commented.

    ![Correção sugerida](../dma/media/suggested-fix.png)

2. Selecione **script SQL geral**.

3. Examine o script gerado.

    ![Script gerado](../dma/media/generated-script.png)

## <a name="deploy-schema"></a>Implantar esquema

1. Selecione **implantar esquema**.

2. Examine os resultados da implantação do esquema.

    ![Resultados da implantação de esquema](../dma/media/schema-deployment-results.png)

3. Selecione **migrar dados** para iniciar o processo de migração de dados.

4. Selecione as tabelas com os dados que você deseja migrar.

    ![Selecionar tabelas para migrar](../dma/media/select-tables-to-migrate.png) 

5. Selecione **Iniciar migração de dados**.

A tela final mostra o status geral.

   ![Status da migração](../dma/media/migration-status.png) 

## <a name="see-also"></a>Confira também

* [Assistente de Migração de Dados (DMA)](../dma/dma-overview.md)
* [Assistente de Migração de Dados: definições de configuração](../dma/dma-configurationsettings.md)
* [Assistente de Migração de Dados: práticas recomendadas](../dma/dma-bestpractices.md)
