---
title: Atualização do SQL Server para SQL Server ou SQL Server em VMs do Azure usando o Assistente de migração de dados local | Microsoft Docs
description: Saiba como usar o Assistente de migração de dados para atualizar um SQL Server no local para uma versão posterior do SQL Server ou ao SQL Server em VMs do Azure
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 8a68205fe742f386241ab0653afce5b274077cbd
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2018
ms.locfileid: "37946950"
---
# <a name="upgrade-on-premises-sql-server-to-sql-server-or-sql-server-on-azure-vms-using-the-data-migration-assistant"></a>Atualizar o local SQL Server para SQL Server ou SQL Server em VMs do Azure usando o Assistente de migração de dados

O Assistente de migração de dados fornece perfeitas avaliações do SQL Server local e as atualizações para versões posteriores do SQL Server ou as migrações para o SQL Server em VMs do Azure ou banco de dados SQL.

Este artigo fornece instruções passo a passo para a atualização do SQL Server local para a versão mais recente do SQL Server ou ao SQL Server em VMs do Azure usando o Assistente de migração de dados.   

## <a name="create-a-new-migration-project"></a>Criar um novo projeto de migração

1. No painel esquerdo, selecione **New** (+) e, em seguida, o **migração** tipo de projeto.

2. Defina o tipo de servidor de origem e destino como **SQL Server** se você estiver atualizando um SQL Server no local para uma versão posterior do SQL Server no local.

3. Selecione **Criar**.

   ![Criar projeto de migração](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>Especificar a origem e destino

1. Para a fonte, insira o nome da instância do SQL Server no **nome do servidor** campo o **detalhes do servidor de origem** seção. 

2. Selecione o **tipo de autenticação** com suporte na instância do SQL Server de origem.

3. Para o destino, digite o nome da instância do SQL Server no **nome do servidor** campo o **detalhes do servidor de destino** seção. 

4. Selecione o **tipo de autenticação** com suporte na instância do SQL Server de destino.

5. É recomendável que você criptografe a conexão, selecionando **criptografar conexão** na **propriedades de Conexão** seção.

6. Clique em **Avançar**.

   ![Especifique a página de origem e destino](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>Adicionar bancos de dados

1. Escolha os bancos de dados específicos que você deseja migrar selecionando apenas os bancos de dados, no painel esquerdo do **adicionar bancos de dados** página.

   Por padrão, todos os banco de dados na instância do SQL Server de origem é selecionados para migração

2. Use as configurações de migração no lado direito da página para definir as opções de migração que são aplicadas aos bancos de dados, fazendo o seguinte.

   > [!NOTE]
   > Você pode aplicar as configurações de migração para todos os bancos de dados que você está migrando, selecionando o servidor no painel esquerdo. Você também pode configurar um banco de dados individual com configurações específicas, selecionando o banco de dados no painel esquerdo.

    A. Especifique o **compartilhado local acessível por servidores SQL de origem e destino para a operação de backup**. Certifique-se de que a conta de serviço executando o código-fonte tem de instância do SQL Server gravar privilégios em um local compartilhado e a conta de serviço de destino tem privilégios de leitura no local compartilhado.

    B. Especifique o local para restaurar os dados e arquivos de log transacional no servidor de destino.

    ![Adicionar página bancos de dados](../dma/media/AddDatabases.png)

3. Insira um local compartilhado que as instâncias do SQL Server de origem e destino têm acesso, na **opções de local de compartilhamento** caixa.

4. Se você não pode fornecer um local compartilhado que SQL os servidores de origem e destino têm acesso, selecione **copiar os backups de banco de dados para um local diferente que o servidor de destino pode ler e restaurar a partir de**. Em seguida, insira um valor para o **local para o backup para a opção de restauração** caixa. 

   Certifique-se de que a conta de usuário executando o Assistente de migração de dados leu privilégios para o local de backup e privilégios de gravação para o local do qual restaura o servidor de destino.

   ![Opção para copiar os backups de banco de dados para outro local](../dma/media/CopyDatabaseDifferentLocation.png)

5. Selecione **Avançar**.

O Assistente de migração de dados executa validações nas pastas de backup, dados e arquivos de log locais. Se qualquer validação falhar, corrija as opções e, em seguida, selecione **próxima**.

## <a name="select-logins"></a>Selecionar logons

1. Selecione os logons específicos para a migração.

   > [!IMPORTANT]
   > Certifique-se de selecionar os logons que são mapeados para um ou mais usuários em bancos de dados selecionados para migração.   

   Por padrão, os logons do SQL Server e Windows que se qualificam para migração são selecionados para migração.

2. Selecione **Iniciar migração**.

   ![Selecione os logons e iniciar a migração](../dma/media/SelectLogins.png)

## <a name="view-results"></a>Exibir resultados

Você pode monitorar o andamento da migração sobre a **exibir resultados** página.

![Página de resultados do modo de exibição](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>Exportar resultados da migração

1. Clique em **Exportar relatório** na parte inferior a **exibir resultados** página para salvar os resultados da migração para um arquivo CSV.

2. Examine o arquivo salvo para obter detalhes sobre a migração de logon e, em seguida, verifique se as alterações.

## <a name="see-also"></a>Confira também

- [Assistente de migração de dados (DMA)](../dma/dma-overview.md)
- [Assistente de migração de dados: Definições de configuração](../dma/dma-configurationsettings.md)
- [Assistente de migração de dados: Práticas recomendadas](../dma/dma-bestpractices.md)
