---
title: Avaliando os esquemas do DB2 para conversão (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8892f5a4-72ba-4406-8649-7a9d67f4c1d9
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 506b9a32b465c9006fe4030bd6fcbb8ba4d0f136
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67938335"
---
# <a name="assessing-db2-schemas-for-conversion-db2tosql"></a>Avaliando os esquemas do DB2 para conversão (DB2ToSQL)
Antes de carregar objetos e migrar dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]para o, você deve determinar a complexidade da migração e a quantidade de tempo que a migração levará. O SSMA pode criar um relatório de avaliação que mostra a porcentagem de objetos que serão convertidos com êxito. O SSMA também permite que você exiba os problemas específicos que causam falhas de conversão.  
  
## <a name="creating-assessment-reports"></a>Criando relatórios de avaliação  
Quando ele cria esse relatório de avaliação, o SSMA converte os objetos de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados DB2 selecionados em sintaxe e, em seguida, mostra os resultados.  
  
**Para criar um relatório de avaliação**  
  
1.  No Gerenciador de metadados do DB2, selecione os esquemas a serem avaliados.  
  
2.  Para omitir objetos individuais, desmarque as caixas de seleção ao lado delas.  
  
3.  Clique com o botão direito do mouse em **esquemas**e selecione **criar relatório**.  
  
    Você também pode analisar objetos individuais clicando com o botão direito do mouse em um objeto e selecionando **criar relatório**.  
  
    O SSMA mostrará o progresso na barra de status na parte inferior da janela. Se o painel de saída estiver visível, você também verá mensagens no painel de saída.  
  
    Quando a avaliação for concluída, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] janela Assistente de migração para DB2: relatório de avaliação será exibida.  
  
## <a name="using-assessment-reports"></a>Usando relatórios de avaliação  
A janela relatório de avaliação contém três painéis:  
  
-   O painel esquerdo contém a hierarquia de objetos que são incluídos no relatório de avaliação. Você pode procurar a hierarquia e selecionar objetos e categorias de objetos para exibir estatísticas e código de conversão.  
  
-   O conteúdo do painel direito depende do item selecionado no painel esquerdo.  
  
    Se um grupo de objetos estiver selecionado, como um esquema ou se uma tabela estiver selecionada, o painel direito conterá um painel de estatísticas de conversão e um painel objetos por categorias. O painel estatísticas de conversão mostra as estatísticas de conversão para os objetos selecionados. O painel objetos por categorias mostra as estatísticas de conversão para o objeto ou as categorias de objetos.  
  
    Se uma função, pacote, procedimento, sequência ou exibição for selecionada, o painel direito conterá estatísticas, código-fonte e código de destino.  
  
    -   A área superior mostra as estatísticas gerais do objeto. Talvez seja necessário expandir as **estatísticas** para exibir essas informações.  
  
    -   A área de origem mostra o código-fonte do objeto selecionado no painel esquerdo. As áreas realçadas mostram o código-fonte problemático.  
  
    -   A área de destino mostra o código convertido. Texto vermelho mostra código problemático e mensagens de erro.  
  
-   O painel inferior mostra as mensagens de conversão, agrupadas por número de mensagem. Você pode clicar em **erros**, **avisos**ou **informações** para exibir categorias de mensagens e, em seguida, expandir um grupo de mensagens. Clique em uma mensagem individual para selecionar o objeto no painel esquerdo e exibir os detalhes no painel direito.  
  
## <a name="analyzing-conversion-problems-by-using-the-assessment-report"></a>Analisando problemas de conversão usando o relatório de avaliação  
O painel estatísticas de conversão mostra as estatísticas de conversão. Se a porcentagem de qualquer categoria for menor que 100%, você deverá determinar por que a conversão não foi bem-sucedida.  
  
**Para exibir problemas de conversão**  
  
1.  Crie o relatório de avaliação usando as instruções no procedimento anterior.  
  
2.  No painel esquerdo, expanda esquemas ou pastas que têm um ícone de erro vermelho. Continue expandindo itens até selecionar um item individual que falhou na conversão.  
  
3.  Na parte superior do painel de origem, clique em **próximo problema**.  
  
    O código problemático é realçado, assim como o código relacionado no painel de navegação de destino.  
  
4.  Revise Todas as mensagens de erro e determine o que você deseja fazer com o objeto que causou o problema de conversão:  
  
    -   Atualize a sintaxe do DB2 no SSMA. Você pode atualizar a sintaxe para procedimentos, funções, gatilhos, funções empacotadas e procedimentos empacotados. Para atualizar a sintaxe, selecione o objeto no painel do Gerenciador de metadados do DB2, clique na guia **SQL** e modifique o código SQL. Ao sair do item, você será solicitado a salvar a sintaxe atualizada. Você pode exibir os erros relatados para o objeto na guia **relatório** .  
  
    -   No DB2, você pode modificar o objeto DB2 para remover ou revisar o código problemático. Para carregar o código atualizado no SSMA, você precisará atualizar os metadados. Para obter mais informações, consulte [conectando ao banco de dados DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md).  
  
    -   Você pode excluir o objeto da migração. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados e no Gerenciador de metadados DB2, desmarque a caixa de seleção ao lado do item antes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de carregar os objetos no e migrar dados do DB2.  
  
## <a name="next-step"></a>Próxima etapa  
[Convertendo esquemas do DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Migrar bancos de dados DB2 para SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
