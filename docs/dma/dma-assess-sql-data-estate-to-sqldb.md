---
title: Avaliar a preparação de um acervo de dados do SQL Server migrando para o banco de dados SQL do Azure | Microsoft Docs
description: Saiba como usar o Assistente de migração de dados para migrar um acervo de dados do SQL Server para a migração para o banco de dados SQL
ms.custom: ''
ms.date: 07/16/2019
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
manager: jroth
ms.openlocfilehash: d317fb3f0c2227744318eeaead71514095afbdec
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68269378"
---
# <a name="assess-the-readiness-of-a-sql-server-data-estate-migrating-to-azure-sql-database-using-the-data-migration-assistant"></a>Avaliar a preparação de um acervo de dados do SQL Server migrando para o banco de dados do SQL Azure usando o Assistente de migração de dados

Migrando centenas de instâncias do SQL Server e milhares de bancos de dados para o banco de dados SQL, nossa oferta de plataforma como serviço (PaaS) são uma tarefa considerável. Para simplificar o processo tanto quanto possível, você precisa se sentir confiante sobre a preparação de sua relativa para a migração. Identificação de parte, incluindo os servidores e bancos de dados que estão totalmente pronto ou que exigem um mínimo de esforço para se preparar para migração, facilita e acelera a seus esforços.

Este artigo fornece instruções passo a passo para aproveitar o [Assistente de migração de dados](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017) para resumir resultados da preparação e reproduzi-los na [migrações para Azure](https://portal.azure.com/?feature.customPortal=false#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview) hub.

## <a name="create-a-project-and-add-a-tool"></a>Criar um projeto e adicionar uma ferramenta

Configurar um novo projeto de migrações para Azure em uma assinatura do Azure e, em seguida, adicionar uma ferramenta.

Um projeto de migrações para Azure é usado para armazenar a descoberta, avaliação e coletados do ambiente você está avaliando ou migração de metadados de migração. Você também usar um projeto para rastrear ativos descobertos e orquestrar a avaliação e migração.

1. Entre no portal do Azure, selecione **todos os serviços**e, em seguida, pesquise por migrações para Azure.
2. Sob **Services**, selecione **migrações para Azure**.

   ![Migrações para Azure – selecione serviço](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-services.png)

3. Sobre o **visão geral** página, selecione **avaliar e migrar bancos de dados**.

   ![Migrações para Azure - Iniciar avaliação](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

4. Na **bancos de dados**, em **Introdução**, selecione **adicionar ferramentas**.

   ![As migrações para Azure - adicionar ferramentas](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tools.png)

5. Sobre o **projeto de migração** , selecione o grupo de recursos e assinatura do Azure (se você ainda não tiver um recurso de grupo, crie um).
6. Sob **detalhes do projeto**, especifique o nome do projeto e a localização geográfica na qual você deseja criar o projeto.

    ![As migrações para Azure - adicionar uma caixa de diálogo de ferramenta](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tool-dialog.png)

    Você pode criar um projeto de migrações para Azure em qualquer uma dessas regiões geográficas.

    | **Geography**  | **Região do local de armazenamento** |
    | ------------- | ------------- |
    | Ásia | Sudeste da Ásia ou na Ásia Oriental |
    | Europe | Sul da Europa ou Europa Ocidental |
    | United Kingdom | Sul do Reino Unido ou oeste do Reino Unido |
    | Estados Unidos | Centro dos EUA ou oeste dos EUA 2 |

    A localização geográfica especificada para o projeto só é usada para armazenar os metadados coletados das VMs locais. Você pode selecionar qualquer região de destino para a migração real.

7. Selecione **próxima**e, em seguida, adicione uma ferramenta de avaliação.

   > [!NOTE]
   > Quando você cria um projeto, você deve adicionar pelo menos uma ferramenta de avaliação ou migração.

8. Sobre o **ferramenta de avaliação Select** guia, **migrações para Azure: Avaliação do banco de dados** aparece como a ferramenta de avaliação para adicionar. Se uma ferramenta de avaliação no momento, não é necessário, selecione a **ignorar a adição de uma ferramenta de avaliação agora** caixa de seleção. Selecione **Avançar**.

    ![Migrações para Azure - guia da ferramenta de avaliação de Select](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-assessment-tool.png)

9. Sobre o **ferramenta de migração Select** guia, **migrações para Azure: Migração de banco de dados** aparece como a ferramenta de migração para adicionar. Se você não é necessário no momento, uma ferramenta de migração, selecione a **ignorar a adição de uma ferramenta de migração agora**. Selecione **Avançar**.

    ![Migrações para Azure - guia da ferramenta de migração de Select](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-migration-tool.png)

10. Na **revisar + adicionar ferramentas**, examine as configurações e selecione **adicionar ferramentas**.

    ![As migrações para Azure - revisão + Adicionar guia Ferramentas](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-tools.png)

    Depois de criar o projeto, você pode selecionar ferramentas adicionais de avaliação e migração de servidores e cargas de trabalho, os bancos de dados e aplicativos web.

## <a name="assess-and-upload-assessment-results"></a>Avaliar e carregar os resultados da avaliação

Depois que você cria com êxito um projeto de migração, sob **ferramentas de avaliação**, no **migrações para Azure: Avaliação do banco de dados** caixa, as instruções para baixar e usar a exibição da ferramenta Assistente de migração de dados.

   ![Migrações para Azure - ferramenta de avaliação adicionado](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessment-tool-added.png)

1. Baixe o Assistente de migração dados usando o link fornecido e, em seguida, instalá-lo em um computador com acesso às suas instâncias do SQL Server de origem.
2. Inicie o Assistente de migração de dados.

### <a name="create-an-assessment"></a>Criar uma avaliação

1. À esquerda, selecione o **+** ícone e, em seguida, selecione a avaliação **tipo de projeto**
2. Especifique o nome do projeto e, em seguida, selecione o servidor de origem e os tipos de servidor de destino.

    Se você estiver atualizando sua instância do SQL Server local para uma versão posterior do SQL Server ou SQL Server hospedado em uma VM do Azure, defina o tipo de servidor de origem e destino como **SQL Server**. Defina o tipo de servidor de destino como **banco de dados de instância gerenciada do SQL** para uma avaliação de prontidão de destino de banco de dados do SQL do Azure (PaaS).

3. Selecione **Criar**.

   ![Migrações para Azure - interface do Assistente de migração de dados](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-interface.png)

### <a name="choose-assessment-options"></a>Escolha as opções de avaliação

1. Selecione o tipo de relatório.

    Você pode escolher um ou ambos os tipos de relatórios a seguir:
    * Verificar a compatibilidade do banco de dados
    * Verificar paridade de recursos

   ![Tela de opções de avaliação - Assistente de migração de dados - as migrações do Azure](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-options-screen.png)

2. Selecione **Avançar**.

### <a name="add-databases-to-assess"></a>Adicionar bancos de dados para avaliar

1. Selecione **adicionar fontes** para abrir o menu desdobráveis de conexão.
2. Insira o nome de instância do SQL server, escolha o tipo de autenticação, defina as propriedades de conexão correta e, em seguida, selecione **Connect**.
3. Selecione os bancos de dados para avaliar e, em seguida, selecione **adicionar**.

   > [!NOTE]
   > Você pode remover vários bancos de dados, selecionando-os ao mesmo tempo mantendo pressionada a tecla Shift ou Ctrl e, em seguida, clicar em remover fontes. Você também pode adicionar bancos de dados de várias instâncias do SQL Server usando o botão Adicionar fontes.

4. Selecione **próxima** para iniciar a avaliação.

   ![Tela de seleção de fontes do Azure - Assistente de migração de dados - as migrações](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-select-sources-screen.png)

5. Depois que a avaliação for concluída, selecione **carregar para migrações para Azure**.

   ![Tela de resultados de análise - Assistente de migração de dados - as migrações do Azure](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-review-results-screen.png)

6. Entre no portal do Azure.

   ![Tela de resultados de análise - Assistente de migração de dados - as migrações do Azure](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-signin.png)

7. Selecione a assinatura e o projeto de migrações para Azure no qual você deseja carregar os resultados da avaliação e, em seguida, selecione **carregar**.

   Aguarde a confirmação de carregamento de avaliação.

## <a name="view-target-readiness-assessment-results"></a>Modo de exibição resultados da avaliação de prontidão de destino

1. Entrar no portal do Azure, pesquise por migrações para Azure e selecione **migrações para Azure**.

   ![Pesquisa de serviço - portal do Azure - as migrações do Azure](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-search.png)

2. Selecione **avaliar e migrar bancos de dados** para obter os resultados da avaliação.

   ![Migrações para Azure - examine os resultados da avaliação](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

    Você pode exibir o resumo de preparação do SQL Server, verifique se você estiver usando o projeto de migração à direita, caso contrário, use alterar a opção de selecionar um projeto de migração diferentes.

    Cada vez que você atualizar os resultados da avaliação para o Azure migrar o projeto, migrações para Azure hub consolidar todos os resultados e fornecer o relatório de resumo.  Você pode executar várias avaliações de Assistente de migração de dados em paralelo e carregar os resultados para o projeto de migração única para obter o relatório de prontidão consolidado.

   ![Migrações para Azure – resultados da revisão de preparação](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-readiness.png)

    **Avaliado instâncias de banco de dados**:  O número de instâncias do SQL Server avaliado até o momento.
    **Avaliado bancos de dados**: Número total de bancos de dados avaliados em um ou mais instâncias do SQL Server avaliadas **bancos de dados prontos para o banco de dados SQL**:  Número de bancos de dados prontos para migrar para o banco de dados do SQL do Azure (PaaS).
    **Bancos de dados estão prontos para a VM do SQL Azure**:  Número de bancos de dados consistem em um ou mais bloqueadores de migração para o banco de dados do SQL do Azure (PaaS), mas pronto para migrar para VMs do Azure SQL Server.

3. Selecione **avaliado instâncias de banco de dados** para chegar à exibição de nível de instância do SQL Server.

   ![Migrações para Azure - revisão de prontidão de instância](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-instances.png)

    Você pode encontrar o status de preparação do percentual de cada instância do SQL Server migrando para o banco de dados do SQL do Azure (PaaS).

4. Selecione uma instância específica para obter a exibição de preparação do banco de dados.

   ![Migrações para Azure - preparação do banco de dados de revisão](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-databases.png)

    Você pode ver o número do bloqueadores de migração por cada banco de dados, o destino recomendado por cada banco de dados no modo de exibição acima.

5. Examine os resultados da avaliação de DMA para obter mais detalhes sobre os bloqueadores de migração.

   ![Migrações para Azure - bloqueadores de migração de revisão](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-migration-blockers.png)

## <a name="see-also"></a>Confira também

* [Assistente de migração de dados (DMA)](../dma/dma-overview.md)
* [Assistente de migração de dados: Definições de configuração](../dma/dma-configurationsettings.md)
* [Assistente de migração de dados: Práticas recomendadas](../dma/dma-bestpractices.md)
