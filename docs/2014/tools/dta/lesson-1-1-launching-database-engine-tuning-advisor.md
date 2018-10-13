---
title: Orientador de Otimização do Mecanismo de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- tuning databases [SQL Server]
- Database Engine Tuning Advisor [SQL Server], starting
ms.assetid: 4abc0e10-96fd-4e46-93d6-d7ee03eec844
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ad6b28f2e133abcc872186adc57fdd422687ddc5
ms.sourcegitcommit: 110e5e09ab3f301c530c3f6363013239febf0ce5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48906246"
---
# <a name="launching-database-engine-tuning-advisor"></a>Iniciando o Orientador de Otimização do Mecanismo de Banco de Dados
  Para começar, abra a GUI (interface gráfica do usuário) do Orientador de Otimização do Mecanismo de Banco de Dados. Ao usá-lo pela primeira vez, um membro da função de servidor fixa **sysadmin** deve iniciar o Orientador de Otimização do Mecanismo de Banco de Dados para inicializar o aplicativo. Após a inicialização, os membros da função de banco de dados fixa **db_owner** podem usar o Orientador de Otimização do Mecanismo de Banco de Dados para ajustar seus bancos de dados. Para obter mais informações sobre como inicializar o Orientador de Otimização do Mecanismo de Banco de Dados, consulte [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/database-engine-tuning-advisor.md).  
  
### <a name="open-the-database-engine-tuning-advisor-gui"></a>Abra a GUI do Orientador de Otimização do Mecanismo de Banco de Dados.  
  
1.  No menu **Iniciar** do Windows, aponte para **Todos os Programas**, para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], para **Ferramentas de Desempenho**e clique em **Orientador de Otimização do Mecanismo de Banco de Dados**.  
  
2.  Na caixa de diálogo **Conectar ao Servidor** , verifique as configurações padrão e clique em **Conectar**.  
  
 Por padrão, o Orientador de Otimização do Mecanismo de Banco de Dados é aberto para configuração na seguinte ilustração:  
  
 ![Janela de padrão do Orientador de otimização do mecanismo de banco de dados](media/defaultdtagui.gif "janela padrão do Orientador de otimização do mecanismo de banco de dados")  
  
> [!NOTE]  
>  Na guia e **nome da sessão** caixa Exibir o nome do seu computador e a instância que você está conectado. A guia e a caixa também exibem a data e a hora atuais.  
  
 Dois painéis principais são exibidos na GUI do Orientador de Otimização do Mecanismo de Banco de Dados quando ele é aberto pela primeira vez.  
  
-   O painel esquerdo contém o Monitor de Sessão, que lista todas as sessões de ajuste que foram executadas nessa instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ao abrir o Orientador de Otimização do Mecanismo de Banco de Dados, ele exibe uma sessão nova na parte superior do painel. Você pode nomear essa sessão no painel adjacente. Inicialmente, apenas uma sessão padrão é listada. Essa é a sessão padrão que o Orientador de Otimização do Mecanismo de Banco de Dados cria automaticamente para você. Depois que você tiver ajustado os bancos de dados, são listadas todas as sessões de ajuste para a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a qual você está conectado na sessão nova. Você pode clicar com o botão direito em uma sessão de ajuste para que ela seja renomeada, fechada, excluída ou clonada. Ao clicar na lista com o botão direito do mouse, é possível classificar as sessões por nome, status ou hora de criação, ou criar uma sessão nova. Na seção inferior desse painel, são exibidos detalhes da sessão de ajuste selecionada. Você pode optar pela exibição dos detalhes organizados em categorias com o botão **Categorizado** ou exibi-los em uma lista em ordem alfabética usando o botão **Alfabético** . Você também pode ocultar o Monitor de Sessão arrastando a borda direita do painel para o lado esquerdo da janela. Para exibi-lo novamente, arraste a borda do painel de volta para a direita. O Monitor de Sessão lhe permite exibir sessões de ajuste anteriores ou usá-las para criar sessões novas com definições semelhantes. Você também pode usar o Monitor de Sessão para avaliar recomendações de ajuste Para obter mais informações, veja [Exibir e trabalhar com a saída do Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md). Use o botão **Voltar** do navegador para retornar a este tutorial.  
  
-   O painel direito contém as guias **Geral** e **Opções de Ajuste** . É aí que você pode definir sua sessão de Otimização do Mecanismo de Banco de Dados. Na guia **Geral** , você digita o nome de sua sessão de ajuste, especifica o arquivo de carga de trabalho ou tabela a ser usada e seleciona os bancos de dados e tabelas que deseja ajustar nesta sessão. A carga de trabalho é um conjunto de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas em um ou mais bancos de dados a serem ajustados. O Orientador de Otimização do Mecanismo de Banco de Dados utiliza arquivos de rastreamento, tabelas de rastreamento, scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] ou arquivos XML como entrada de carga de trabalho ao ajustar bancos de dados. Na guia **Opções de Ajuste** , você pode selecionar as estruturas de design de banco de dados físicas (índices ou exibições indexadas) e a estratégia de particionamento que deseja que o Orientador de Otimização do Mecanismo de Banco de Dados considere durante a análise. Nessa guia, você pode especificar também o tempo máximo que o Orientador de Otimização do Mecanismo de Banco de Dados leva para ajustar uma carga de trabalho. Por padrão, o Orientador de Otimização do Mecanismo de Banco de Dados ajustará uma carga de trabalho durante uma hora.  
  
> [!NOTE]  
>  O Orientador de Otimização do Mecanismo de Banco de Dados pode usar arquivos XML como entrada quando um script [!INCLUDE[tsql](../../includes/tsql-md.md)] é importado do Editor de Consultas do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . Para obter mais informações, consulte a seção sobre como iniciar o Orientador de Otimização do Mecanismo de Banco de Dados no Editor de Consultas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] em [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/database-engine-tuning-advisor.md).  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Definindo o layout e opções de ferramentas](lesson-1-2-setting-tool-options-and-layout.md)  
  
  
