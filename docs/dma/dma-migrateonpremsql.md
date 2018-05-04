---
title: Migrar do SQL Server local (Assistente de migração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
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
ms.openlocfilehash: fd4c8e57b0854fb56eafa3d90b31bfddbe6455a3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="migrate-on-premises-sql-server-using-data-migration-assistant"></a>Migrar do SQL Server no local usando o Assistente de migração de dados

Este artigo fornece instruções passo a passo para migração do SQL Server usando o Assistente de migração de dados.

Assistente de migração de dados fornece avaliações contínua e migrações de plataformas de dados do SQL Server e SQL Azure VM local modernos.  

Conclua as seguintes tarefas para executar a migração.

- [Criar um novo projeto de migração](#create-a-new-migration-project)
- [Especificar a origem e destino](#specify-source-and-target)
- [Adicionar bancos de dados](#add-databases)
- [Selecione logons](#select-logins)

## <a name="create-a-new-migration-project"></a>Criar um novo projeto de migração

1. Clique em **novo** (+) no painel esquerdo e selecione o **migração** tipo de projeto.

1. Definir o tipo de servidor de origem e destino **do SQL Server** se você estiver atualizando um SQL Server no local para um moderno local do SQL Server.

1. Clique em **Criar**.

   ![Criar o projeto de migração](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>Especificar a origem e destino

1. Para a fonte, insira o nome da instância do SQL Server no **nome do servidor** campo o **detalhes do servidor de origem** seção. 

1. Selecione o **tipo de autenticação** com suporte na instância do SQL Server de origem.

1. Para o destino, digite o nome da instância do SQL Server no **nome do servidor** campo o **detalhes do servidor de destino** seção. 

1. Selecione o **tipo de autenticação** com suporte na instância do SQL Server de destino.

1. É recomendável que você criptografe a conexão selecionando **criptografar conexão** no **propriedades de Conexão** seção.

1. Clique em **Avançar**.

   ![Especifique a página de origem e destino](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>Adicionar bancos de dados

1. Escolha os bancos de dados específicos que você deseja migrar selecionando apenas os bancos de dados, no painel esquerdo do **adicionar bancos de dados** página.

   Por padrão, todos os banco de dados na instância do SQL Server de origem é selecionados para migração

1. Use as configurações de migração no lado direito da página para definir as opções de migração que são aplicadas aos bancos de dados, fazendo o seguinte.

   > [!NOTE]
   > Você pode aplicar as configurações de migração para todos os bancos de dados que você está migrando, selecionando o servidor no painel esquerdo. Você também pode configurar um banco de dados individual com configurações específicas, selecionando o banco de dados no painel esquerdo.


 1. Especifique o **compartilhado local acessível por servidores SQL de origem e destino para a operação de backup**. Certifique-se de que a conta de serviço que executa o código-fonte tem de instância do SQL Server gravar privilégios no local compartilhado e a conta de serviço de destino tem leitura privilégios no local compartilhado.

 1. Especifique o local para restaurar os dados e arquivos de log transacional no servidor de destino.

    ![Adicionar página bancos de dados](../dma/media/AddDatabases.png)

1. Insira um local compartilhado que as instâncias do SQL Server de origem e destino têm acesso, no **compartilham opções local** caixa.

1. Se você não pode fornecer um local compartilhado que SQL os servidores de origem e de destino têm acesso, selecione **copiar os backups de banco de dados para um local diferente que o servidor de destino pode ler e restaurar a partir de**. Em seguida, insira um valor para o **local para backups para a opção de restauração** caixa. 

   Certifique-se de que a conta de usuário executando o Assistente de migração de dados tem privilégios para o local de backup de leitura e privilégios de gravação para o local do qual restaura o servidor de destino.

   ![Opção para copiar backups do banco de dados em outro local](../dma/media/CopyDatabaseDifferentLocation.png)

1. Clique em **Avançar**.

Assistente de migração de dados executa validações nas pastas de backup, dados e log locais de arquivo. Se nenhuma validação falhar, corrija as opções e clique em **próximo**.

## <a name="select-logins"></a>Selecione logons

1. Selecione logons específicos para a migração.

   > [!IMPORTANT]
   > Certifique-se de selecionar os logons que são mapeados para um ou mais usuários nos bancos de dados selecionados para migração.   

   Por padrão, os logons do SQL Server e Windows que se qualificam para migração são selecionados para migração.

1. Clique em **Iniciar migração**.

   ![Selecione logons e iniciar a migração](../dma/media/SelectLogins.png)

## <a name="view-results"></a>Exibir resultados

Você pode monitorar o andamento da migração no **exibir resultados** página.

![Página de exibição de resultados](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>Exportar resultados da migração

1. Clique em **Exportar relatório** na parte inferior do **exibir resultados** página para salvar os resultados de migração para um arquivo CSV.

1. Examine o arquivo salvo para obter detalhes sobre a migração de logon e, em seguida, verifique se as alterações.

## <a name="see-also"></a>Consulte também

[Assistente de migração de dados (DMA)](../dma/dma-overview.md)

[Assistente de migração de dados: Definições de configuração](../dma/dma-configurationsettings.md)

[Assistente de migração de dados: Práticas recomendadas](../dma/dma-bestpractices.md)
