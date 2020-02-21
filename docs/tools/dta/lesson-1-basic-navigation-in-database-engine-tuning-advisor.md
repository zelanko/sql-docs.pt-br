---
title: Navegação básica no DTA
description: O DTA (Orientador de Otimização do Mecanismo de Banco de Dados) fornece um modo baseado em GUI (interface gráfica do usuário) para exibir sessões de ajuste e relatórios de recomendações de ajuste.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], tutorials
ms.assetid: ad49b2e0-a5e3-49d2-80fd-9f4eaa3652cb
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-dt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 9bb0911a0aa678ee160894e6297e5636644bf475
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75307651"
---
# <a name="lesson-1-basic-navigation-in-database-engine-tuning-advisor-dta"></a>Lição 1: Navegação básica no DTA (Orientador de Otimização do Mecanismo de Banco de Dados)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O Orientador de Otimização do Mecanismo de Banco de Dados fornece um modo baseado em GUI (Interface gráfica do usuário) para exibir sessões de ajuste e relatórios de recomendações. Esta lição mostra como iniciar a ferramenta e como configurar a exibição. Ao término desta lição, você saberá as diversas maneiras de iniciar a ferramenta e como configurar sua exibição para dar suporte às tarefas de ajuste que você executa regularmente.  

## <a name="prerequisites"></a>Prerequisites 

Para concluir este tutorial, você precisará do SQL Server Management Studio, bem como acesso a um servidor que executa o SQL Server e um banco de dados do AdventureWorks.

- Instalar o [SQL Server Management Studio.](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)
- Instalar o [SQL Server 2017 Developer Edition.](https://www.microsoft.com/sql-server/sql-server-downloads)
- Baixar o [Bancos de dados de exemplo do AdventureWorks2017.](https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017)


Instruções para restaurar bancos de dados no SSMS são encontradas aqui: [Restaurar um banco de dados.](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms?view=sql-server-2017)

  >[!NOTE]
  > Este tutorial destina-se a um usuário familiarizado com o uso de SQL Server Management Studio e com as tarefas básicas de administração de banco de dados. 
  

## <a name="launch-database-tuning-advisor"></a>Inicializar o Orientador de Otimização de Banco de Dados 
Para começar, abra a GUI (interface gráfica do usuário) do DTA (Orientador de Otimização do Mecanismo de Banco de Dados). Ao usá-lo pela primeira vez, um membro da função de servidor fixa **sysadmin** deve iniciar o Orientador de Otimização do Mecanismo de Banco de Dados para inicializar o aplicativo. Após a inicialização, os membros da função de banco de dados fixa **db_owner** podem usar o Orientador de Otimização do Mecanismo de Banco de Dados para ajustar seus bancos de dados. Para obter mais informações sobre como inicializar o Orientador de Otimização do Mecanismo de Banco de Dados, consulte [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
1. Inicie o SSMS (Start SQL Server Management Studio). No **menu Iniciar** do Windows, aponte para **Todos os Programas** e localize o **SQL Server Management Studio**. 
2. Depois que o SSMS estiver aberto, selecione o menu **Ferramentas** e selecione **Orientador de Otimização de Banco de Dados**. 

  ![iniciar o DTA usando o SSMS](media/dta-tutorials/launch-dta.png)

3. O Orientador de Otimização de Banco de Dados é iniciado e abre a caixa de diálogo **Conectar-se ao Servidor**. Verifique as configurações padrão e, em seguida, selecione **Conectar** para conectar-se ao seu SQL Server.  
  
Por padrão, o Orientador de Otimização do Mecanismo de Banco de Dados é aberto para configuração na seguinte ilustração:  
  
![Janela padrão do Orientador de Otimização do Mecanismo de Banco de Dados](media/dta-tutorials/dta-default-gui.png)
  
> [!NOTE]  
> A guia **Monitor de Sessão** exibe o nome da sessão, que é o nome do usuário conectado e os dados atuais. 
  
Dois painéis principais são exibidos na GUI do Orientador de Otimização do Mecanismo de Banco de Dados quando ele é aberto pela primeira vez.  
  
-   O painel esquerdo contém o Monitor de Sessão, que lista todas as sessões de ajuste que foram executadas nessa instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao abrir o Orientador de Otimização do Mecanismo de Banco de Dados, ele exibe uma sessão nova na parte superior do painel. Você pode nomear essa sessão no painel adjacente. Inicialmente, apenas uma sessão padrão é listada. Essa é a sessão padrão que o Orientador de Otimização do Mecanismo de Banco de Dados cria automaticamente para você. Depois que você tiver ajustado os bancos de dados, são listadas todas as sessões de ajuste para a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a qual você está conectado na sessão nova. Você pode clicar com o botão direito em uma sessão de ajuste para que ela seja renomeada, fechada, excluída ou clonada. Ao clicar na lista com o botão direito do mouse, é possível classificar as sessões por nome, status ou hora de criação, ou criar uma sessão nova. Na seção inferior desse painel, são exibidos detalhes da sessão de ajuste selecionada. Você pode optar pela exibição dos detalhes organizados em categorias com o botão **Categorizado** ou exibi-los em uma lista em ordem alfabética usando o botão **Alfabético** . Você também pode ocultar o Monitor de Sessão arrastando a borda direita do painel para o lado esquerdo da janela. Para exibi-lo novamente, arraste a borda do painel de volta para a direita. O Monitor de Sessão lhe permite exibir sessões de ajuste anteriores ou usá-las para criar sessões novas com definições semelhantes. Você também pode usar o Monitor de Sessão para avaliar recomendações de ajuste Para obter mais informações, veja [Exibir e trabalhar com a saída do Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md). Use o botão **Voltar** do navegador para retornar a este tutorial.  
  
-   O painel direito contém as guias **Geral** e **Opções de Ajuste** . É aí que você pode definir sua sessão de Otimização do Mecanismo de Banco de Dados. Na guia **Geral** , você digita o nome de sua sessão de ajuste, especifica o arquivo de carga de trabalho ou tabela a ser usada e seleciona os bancos de dados e tabelas que deseja ajustar nesta sessão. A carga de trabalho é um conjunto de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas em um ou mais bancos de dados a serem ajustados. O Orientador de Otimização do Mecanismo de Banco de Dados utiliza arquivos de rastreamento, tabelas de rastreamento, scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] ou arquivos XML como entrada de carga de trabalho ao ajustar bancos de dados. Na guia **Opções de Ajuste** , você pode selecionar as estruturas de design de banco de dados físicas (índices ou exibições indexadas) e a estratégia de particionamento que deseja que o Orientador de Otimização do Mecanismo de Banco de Dados considere durante a análise. Nessa guia, você pode especificar também o tempo máximo que o Orientador de Otimização do Mecanismo de Banco de Dados leva para ajustar uma carga de trabalho. Por padrão, o Orientador de Otimização do Mecanismo de Banco de Dados ajustará uma carga de trabalho durante uma hora.  
  
> [!NOTE]
> O Orientador de Otimização do Mecanismo de Banco de Dados pode usar arquivos XML como entrada quando um script [!INCLUDE[tsql](../../includes/tsql-md.md)] é importado do Editor de Consultas do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . Para obter mais informações, consulte a seção sobre como iniciar o Orientador de Otimização do Mecanismo de Banco de Dados no Editor de Consultas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] em [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
## <a name="configure-tool-options-and-layout"></a>Configurar as opções e o layout das ferramentas 

1.  No menu **Ferramentas** , clique em **Opções**.  

   ![Opções do DTA](media/dta-tutorials/dta-settings.png) 
  
2.  Na caixa de diálogo **Opções** , exiba as seguintes opções:  
  
    -   Expanda a lista **Na inicialização** para exibir o que o Orientador de Otimização do Mecanismo de Banco de Dados pode exibir ao ser iniciado. Por padrão, está selecionado **Mostrar uma nova sessão** .  
  
    -   Clique em **Alterar Fonte** para consultar quais fontes você pode escolher para as listas de bancos de dados e tabelas na guia **Geral** . As fontes escolhidas para essa opção também serão usadas nos relatórios e grades de recomendação do Orientador de Otimização do Mecanismo de Banco de Dados após a execução do ajuste. Por padrão, o Orientador de Otimização do Mecanismo de Banco de Dados usa fontes de sistema.  
  
    -   O **Número de itens nas listas usadas mais recentemente** pode ser definido entre **1** e **10**. Isso define o número máximo de itens nas listas exibidas ao se clicar em **Sessões Recentes** ou **Arquivos Recentes** no menu **Arquivo** . Por padrão, essa opção está definida como **4**.  
  
    -   Quando **Lembrar minhas últimas opções de ajuste** está marcada, por padrão, o Orientador de Otimização do Mecanismo de Banco de Dados usa as opções de ajuste especificadas em sua última sessão de ajuste para a próxima sessão. Desmarque essa caixa de seleção para usar as opções de ajuste padrão do Orientador de Otimização do Mecanismo de Banco de Dados. Por padrão, essa opção é selecionada.  
  
    -   Por padrão, **Perguntar antes de excluir permanentemente as sessões** está marcada para evitar excluir sessões de ajuste acidentalmente.  
  
    -   Por padrão, **Perguntar antes de parar a análise da sessão** está marcada para evitar parar uma sessão de ajuste acidentalmente antes que o Orientador de Otimização do Mecanismo de Banco de Dados termine de analisar uma carga de trabalho.  
  
## <a name="next-lesson"></a>Próxima lição  
[Lição 2: Usando o Orientador de Otimização do Mecanismo de Banco de Dados](../../tools/dta/lesson-2-using-database-engine-tuning-advisor.md)  
  
  
  
