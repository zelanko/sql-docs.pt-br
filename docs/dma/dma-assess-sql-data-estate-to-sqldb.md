---
title: Avaliar SQL Server prontidão para migrar para o banco de dados SQL do Azure
titleSuffix: Data Migration Assistant
description: Saiba como usar Assistente de Migração de Dados para migrar um espaço de dados de SQL Server para a migração para o Azure SQL Database
ms.date: 12/19/2019
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
manager: jroth
ms.custom: seo-lt-2019
ms.openlocfilehash: 30f840c9fe558382c5a0549f09657c917c69c3d4
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82886183"
---
# <a name="assess-the-readiness-of-a-sql-server-data-estate-migrating-to-azure-sql-database-using-the-data-migration-assistant"></a>Avaliar a prontidão de um SQL Server banco de dados migrando para o Azure SQL usando o Assistente de Migração de Dados

A migração de centenas de instâncias de SQL Server e de milhares de bancos de dados para o Azure SQL Database, nossa oferta de PaaS (plataforma como serviço), é uma tarefa considerável. Para simplificar o processo o máximo possível, você precisa se sentir confiante sobre a preparação relativa para a migração. Identificação de frutas de baixa interrupções, incluindo os servidores e bancos de dados que estão totalmente prontos ou que exigem esforço mínimo para se preparar para a migração, facilitar e acelerar seus esforços.

Este artigo fornece instruções passo a passo para aproveitar os [Assistente de migração de dados](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017) para resumir os resultados de preparação e Surface-los no Hub de [migrações para Azure](https://portal.azure.com/?feature.customPortal=false#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview) .

>
> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Data-Migration-Assistant/player?WT.mc_id=dataexposed-c9-niner]

## <a name="create-a-project-and-add-a-tool"></a>Criar um projeto e adicionar uma ferramenta

Configure um novo projeto de migrações para Azure em uma assinatura do Azure e, em seguida, adicione uma ferramenta.

Um projeto de migrações para Azure é usado para armazenar metadados de descoberta, avaliação e migração coletados do ambiente que você está avaliando ou migrando. Você também usa um projeto para acompanhar os ativos descobertos e orquestrar a avaliação e a migração.

1. Entre no portal do Azure, selecione **todos os serviços**e, em seguida, procure migrações para Azure.
2. Em **Serviços**, selecione **Migrações para Azure**.

   ![Migrações para Azure – selecionar serviço](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-services.png)

3. Na página **visão geral** , selecione **avaliar e migrar bancos de dados**.

   ![Migrações para Azure – Iniciar avaliação](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

4. Em **bancos de dados**, em **introdução**, selecione **Adicionar ferramentas**.

   ![Migrações para Azure – adicionar ferramentas](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tools.png)

5. Na guia **migrar projeto** , selecione sua assinatura do Azure e o grupo de recursos (se você ainda não tiver um grupo de recursos, crie um).
6. Em **detalhes do projeto**, especifique o nome do projeto e a geografia em que você deseja criar o projeto.

    ![Migrações para Azure – adicionar uma caixa de diálogo de ferramenta](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tool-dialog.png)

    Você pode criar um projeto de Migrações para Azure em qualquer uma dessas regiões.

    | **Geografia**  | **Região do local de armazenamento** |
    | ------------- | ------------- |
    | Ásia | Sudeste Asiático ou Leste da Ásia |
    | Europa | Sul da Europa ou Europa Ocidental |
    | Reino Unido | Sul do Reino Unido ou Oeste do Reino Unido |
    | Estados Unidos | EUA Central ou oeste dos EUA 2 |

    A localização geográfica especificada para o projeto só é usada para armazenar os metadados coletados das VMs locais. Você pode selecionar qualquer região de destino para a migração real.

7. Selecione **Avançar**e, em seguida, adicionar uma ferramenta de avaliação.

   > [!NOTE]
   > Ao criar um projeto do, você deve adicionar pelo menos uma ferramenta de avaliação ou migração.

8. Na guia **selecionar ferramenta de avaliação** , **migrações para Azure: avaliação de banco de dados** aparece como a ferramenta de avaliação a ser adicionada. Se, no momento, você não precisar de uma ferramenta de avaliação, marque a caixa de seleção **ignorar a ferramenta de avaliação para agora** . Selecione **Avançar**.

    ![Migrações para Azure – guia selecionar ferramenta de avaliação](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-assessment-tool.png)

9. Na guia **selecionar ferramenta de migração** , **migrações para Azure: migração de banco de dados** aparece como a ferramenta de migração a ser adicionada. Se, no momento, você não precisar de uma ferramenta de migração, selecione a **ferramenta ignorar adição de uma migração por enquanto**. Selecione **Avançar**.

    ![Migrações para Azure – selecione a guia ferramenta de migração](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-migration-tool.png)

10. Em **examinar + adicionar ferramentas**, examine as configurações e selecione **Adicionar ferramentas**.

    ![Migrações para Azure – examinar + adicionar ferramenta (s)](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-tools.png)

    Depois de criar o projeto, você pode selecionar ferramentas adicionais para avaliação e migração de servidores e cargas de trabalho, bancos de dados e aplicativos Web.

## <a name="assess-and-upload-assessment-results"></a>Avaliar e carregar resultados da avaliação

Depois de criar com êxito um projeto de migração, em **ferramentas de avaliação**, na caixa **migrações para Azure: avaliação de banco de dados** , instruções para baixar e usar a exibição da ferramenta assistente de migração de dados.

   ![Migração do Azure – ferramenta de avaliação adicionada](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessment-tool-added.png)

1. Baixe Assistente de Migração de Dados usando o link fornecido e, em seguida, instale-o em um computador com acesso às instâncias de SQL Server de origem.
2. Inicie o Assistente de Migração de Dados.

### <a name="create-an-assessment"></a>Criar uma avaliação

1. À esquerda, selecione o **+** ícone e, em seguida, selecione o **tipo de projeto** de avaliação
2. Especifique o nome do projeto e, em seguida, selecione o servidor de origem e os tipos de servidor de destino.

    Se você estiver atualizando sua instância de SQL Server local para uma versão posterior do SQL Server ou para SQL Server hospedada em uma VM do Azure, defina o tipo de servidor de origem e de destino como **SQL Server**. Defina o tipo de servidor de destino como **instância gerenciada do banco de dados SQL do Azure** para uma avaliação de prontidão de destino do banco de dados SQL do Azure (PaaS).

3. Selecione **Criar**.

   ![Migração do Azure-Assistente de Migração de Dados interface](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-interface.png)

### <a name="choose-assessment-options"></a>Escolher opções de avaliação

1. Selecione o tipo de relatório.

    Você pode escolher um ou os dois tipos de relatório a seguir:
    * Determinar compatibilidade do banco de dados
    * Verificação de paridade de recursos

   ![Migração do Azure – tela de opções de Assistente de Migração de Dados de avaliação](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-options-screen.png)

2. Selecione **Avançar**.

### <a name="add-databases-to-assess"></a>Adicionar os bancos de dados a serem avaliados

1. Selecione **adicionar fontes** para abrir o menu suspenso de conexão.
2. Insira o nome da instância do SQL Server, escolha o tipo de autenticação, defina as propriedades de conexão corretas e, em seguida, selecione **conectar**.
3. Selecione os bancos de dados a serem avaliados e, em seguida, selecione **Adicionar**.

   > [!NOTE]
   > Você pode remover vários bancos de dados selecionando-os enquanto mantém a tecla Shift ou CTRL pressionada e clicando em remover fontes. Você também pode adicionar bancos de dados de várias instâncias de SQL Server usando o botão adicionar fontes.

4. Selecione **Avançar** para iniciar a avaliação.

   ![Migração do Azure – tela Assistente de Migração de Dados selecionar fontes](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-select-sources-screen.png)

5. Após a conclusão da avaliação, selecione **carregar para migrações para Azure**.

   ![Migração do Azure-tela de resultados de Assistente de Migração de Dados de análise](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-review-results-screen.png)

6. Entre no portal do Azure.

   ![Migração do Azure-tela de resultados de Assistente de Migração de Dados de análise](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-signin.png)

7. Selecione a assinatura e o projeto de migrações para Azure no qual você deseja carregar os resultados da avaliação e, em seguida, selecione **carregar**.

   Aguarde a confirmação do upload de avaliação.

## <a name="view-target-readiness-assessment-results"></a>Exibir resultados da avaliação de prontidão de destino

1. Entre no portal do Azure, procure migrações para Azure e selecione **migrações para Azure**.

   ![Azure migrar-portal do Azure-pesquisa de serviço](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-search.png)

2. Selecione **avaliar e migrar bancos de dados** para obter os resultados da avaliação.

   ![Migrações para Azure – analisar resultados da avaliação](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

    Você pode exibir o resumo de preparação de SQL Server, verifique se você está no projeto de migração certo, caso contrário, use a opção alterar para selecionar um projeto de migração diferente.

    Cada vez que você atualiza os resultados da avaliação para o projeto de migrações para Azure, o Hub de migrações para Azure consolida todos os resultados e fornece o relatório de resumo.  Você pode executar várias avaliações de Assistente de Migração de Dados em paralelo e carregar os resultados para o projeto de migração única para obter o relatório de prontidão consolidado.

   ![Migrações para Azure – analisar resultados de preparação](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-readiness.png)

    **Instâncias de banco de dados avaliadas**: o número de instâncias de SQL Server avaliadas até agora.
    **Bancos de dados avaliados**: o número total de bancos de dados avaliados em uma ou mais instâncias de SQL Server avaliação **de bancos de dados estão prontas para o BD SQL**: número de banco de dados prontos para migrar para o Azure SQL Database (PaaS).
    **Bancos de dados prontos para a VM do SQL do Azure**: o número de bancos de dados consiste em um ou mais bloqueadores de migração para o Azure SQL Database (PaaS), mas pronto para migrar para as VMs SQL Server do Azure.

3. Selecione **instâncias de banco de dados avaliadas** para obter SQL Server exibição de nível de instância.

   ![Migração do Azure – preparação da instância de revisão](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-instances.png)

    Você pode encontrar o status de preparação de percentual de cada instância de SQL Server migrando para o banco de dados SQL do Azure (PaaS).

4. Selecione uma instância específica para acessar a exibição de preparação do banco de dados.

   ![Migrações para Azure – examinar preparação do banco de dados](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-databases.png)

    Você pode ver o número de bloqueadores de migração por cada banco de dados, o destino recomendado por cada banco de dados na exibição acima.

5. Examine os resultados da avaliação de DMA para obter mais detalhes sobre os bloqueadores de migração.

   ![Migrações para Azure – examinar bloqueadores de migração](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-migration-blockers.png)

## <a name="see-also"></a>Confira também

* [AMD (Assistente de Migração de Dados)](../dma/dma-overview.md)
* [Assistente de Migração de Dados: definições de configuração](../dma/dma-configurationsettings.md)
* [Assistente de Migração de Dados: práticas recomendadas](../dma/dma-bestpractices.md)
