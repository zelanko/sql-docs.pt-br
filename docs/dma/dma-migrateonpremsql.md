---
title: Atualizar SQL Server usando o Assistente de Migração de Dados
description: Saiba como usar Assistente de Migração de Dados para atualizar um SQL Server local para uma versão posterior do SQL Server ou para SQL Server em VMs do Azure
ms.custom: seo-lt-2019
ms.date: 05/18/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.openlocfilehash: 00d27decc533d33056a7cc0cb19c2584fea564fb
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82885864"
---
# <a name="upgrade-sql-server-using-the-data-migration-assistant"></a>Atualizar SQL Server usando o Assistente de Migração de Dados

O Assistente de Migração de Dados fornece avaliações diretas de SQL Server locais e atualizações para versões posteriores de SQL Server ou migrações para SQL Server em VMs do Azure ou banco de dados SQL do Azure.

Este artigo fornece instruções passo a passo para atualizar SQL Server locais para versões posteriores do SQL Server ou para SQL Server em VMs do Azure usando o Assistente de Migração de Dados.

## <a name="create-a-new-migration-project"></a>Criar um novo projeto de migração

1. No painel esquerdo, selecione **novo** (+) e, em seguida, o tipo de projeto de **migração** .

2. Defina o tipo de servidor de origem e de destino como **SQL Server** se você estiver atualizando um SQL Server local para uma versão posterior do SQL Server local.

3. Selecione **Criar**.

   ![Criar projeto de migração](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>Especificar a origem e o destino

1. Para a origem, insira o SQL Server nome da instância no campo **nome do servidor** na seção detalhes do servidor de **origem** . 

2. Selecione o **Tipo de autenticação** compatível com a instância do SQL Server de origem.

3. Para o destino, insira o SQL Server nome da instância no campo **nome do servidor** na seção detalhes do servidor de **destino** . 

4. Selecione o **tipo de autenticação** com suporte na instância de SQL Server de destino.

5. É recomendável criptografar a conexão selecionando **criptografar conexão** na seção **Propriedades da conexão** .

6. Clique em **Avançar**.

   ![Especificar página de origem e de destino](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>Adicionar bancos de dados

1. Escolha os bancos de dados específicos que você deseja migrar selecionando apenas os bancos de dados, no painel esquerdo da página **Adicionar bancos de dados** .

   Por padrão, todos os bancos de dados de usuário na instância de SQL Server de origem são selecionados para migração

2. Use as configurações de migração no lado direito da página para definir as opções de migração que são aplicadas aos bancos de dados, fazendo o seguinte.

   > [!NOTE]
   > Você pode aplicar as configurações de migração a todos os bancos de dados que você está migrando, selecionando o servidor no painel esquerdo. Você também pode configurar um banco de dados individual com configurações específicas selecionando o banco de dados no painel esquerdo.

    a. Especifique o **local compartilhado acessível pelos SQL Servers de origem e de destino para a operação de backup**. Verifique se a conta de serviço que executa a instância de SQL Server de origem tem privilégios de gravação no local compartilhado e se a conta de serviço de destino tem privilégios de leitura no local compartilhado.

    b. Especifique o local para restaurar os dados e os arquivos de log transacionais no servidor de destino.

    ![Página Adicionar bancos de dados](../dma/media/AddDatabases.png)

3. Insira um local compartilhado ao qual as instâncias de SQL Server de origem e destino tenham acesso, na caixa de **Opções de local de compartilhamento** .

4. Se você não puder fornecer um local compartilhado ao qual os SQL Servers de origem e de destino tenham acesso, selecione **copiar os backups de banco de dados em um local diferente do qual o servidor de destino pode ler e restaurar**. Em seguida, insira um valor para a caixa de **opção local para backups para restauração** . 

   Certifique-se de que a conta de usuário que executa o Assistente de Migração de Dados tenha privilégios de leitura para o local de backup e privilégios de gravação no local do qual o servidor de destino restaura.

   ![Opção para copiar backups de banco de dados para um local diferente](../dma/media/CopyDatabaseDifferentLocation.png)

5. Selecione **Avançar**.

O Assistente de Migração de Dados executa validações nas pastas de backup, dados e locais do arquivo de log. Se alguma validação falhar, corrija as opções e, em seguida, selecione **Avançar**.

## <a name="select-logins"></a>Selecionar logons

1. Selecione logons específicos para a migração.

   > [!IMPORTANT]
   > Certifique-se de selecionar os logons mapeados para um ou mais usuários nos bancos de dados selecionados para migração.   

   Por padrão, todos os SQL Server e logons do Windows qualificados para migração são selecionados para migração.

2. Selecione **Iniciar migração**.

   ![Selecionar logons e iniciar a migração](../dma/media/SelectLogins.png)

## <a name="view-results"></a>Exibir os resultados

Você pode monitorar o progresso da migração na página **exibir resultados** .

![Exibir página de resultados](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>Exportar resultados da migração

1. Clique em **Exportar relatório** na parte inferior da página **exibir resultados** para salvar os resultados da migração em um arquivo CSV.

2. Examine o arquivo salvo para obter detalhes sobre a migração de logon e, em seguida, verifique as alterações.

## <a name="see-also"></a>Confira também

- [AMD (Assistente de Migração de Dados)](../dma/dma-overview.md)
- [Assistente de Migração de Dados: definições de configuração](../dma/dma-configurationsettings.md)
- [Assistente de Migração de Dados: práticas recomendadas](../dma/dma-bestpractices.md)
