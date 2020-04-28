---
title: Avaliando bancos de dados MySQL para conversão (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Assessment reports
ms.assetid: 2a56a003-3b0f-453a-963c-00c9e40933ec
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: ae9210444311267569d5f240d40252d4fe024877
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68139213"
---
# <a name="assessing-mysql-databases-for-conversion-mysqltosql"></a>Avaliar os bancos de dados MySQL para conversão (MySQLToSQL)
Antes de carregar objetos e migrar dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o ou SQL Azure, você deve determinar qual será a complexidade da migração e quanto tempo a migração levará. O SSMA pode criar um relatório de avaliação que mostra a porcentagem de objetos que serão convertidos com êxito. O SSMA também permite que você exiba os problemas específicos que causam falhas de conversão.  
  
## <a name="creating-assessment-reports"></a>Criando relatórios de avaliação  
Quando ele cria esse relatório de avaliação, o SSMA converte os objetos de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados MySQL selecionados em ou SQL Azure sintaxe e, em seguida, mostra os resultados.  
  
**Para criar um relatório de avaliação**  
  
1.  No Gerenciador de metadados do MySQL, selecione os esquemas a serem avaliados.  
  
2.  Para omitir objetos individuais, desmarque as caixas de seleção ao lado delas.  
  
3.  Clique com o botão direito do mouse em **esquemas**e selecione **criar relatório**.  
  
    Clique com o botão direito do mouse em um objeto para analisar objetos individuais. Em seguida, selecione **criar relatório**.  
  
    O SSMA mostrará o progresso na barra de status na parte inferior da janela. Se o painel de saída estiver visível, você também verá mensagens no painel de saída.  
  
    Quando a avaliação for concluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assistente de migração para MySQL, janela relatório de avaliação será exibido.  
  
## <a name="using-assessment-reports"></a>Usando relatórios de avaliação  
A janela relatório de avaliação contém três painéis:  
  
-   O painel esquerdo contém a hierarquia de objetos que são incluídos no relatório de avaliação. Você pode procurar a hierarquia e selecionar objetos e categorias de objetos para exibir estatísticas e código de conversão.  
  
-   O conteúdo do painel direito depende do item selecionado no painel esquerdo.  
  
    Se um grupo de objetos estiver selecionado, como esquema, o painel direito conterá um painel de estatísticas de conversão e objetos por painel de categorias. O painel estatísticas de conversão mostra as estatísticas de conversão para os objetos selecionados. O painel objetos por categorias mostra as estatísticas de conversão para o objeto ou as categorias de objetos.  
  
    Se uma função, um procedimento, uma tabela ou uma exibição estiver selecionada, o painel direito conterá estatísticas, código-fonte e código de destino.  
  
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
  
4.  Revise Todas as mensagens de erro e determine o que você deseja fazer com o objeto que causou o problema de conversão.  
  
-   Atualize a sintaxe do MySQL no SSMA. Você pode atualizar a sintaxe somente para procedimentos e funções. Para atualizar a sintaxe, selecione o objeto no painel do explorador de metadados do MySQL, clique na guia **SQL** e modifique o código SQL. Ao sair do item, você será solicitado a salvar a sintaxe atualizada. Você pode exibir os erros relatados para o objeto na guia **relatório** .  
  
-   No MySQL, você pode modificar o objeto MySQL para remover ou revisar o código problemático. Para carregar o código atualizado no SSMA, você precisará atualizar os metadados. Para obter mais informações, consulte [conectando-se ao MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md).  
  
-   Você pode excluir o objeto da migração. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure Gerenciador de metadados e Gerenciador de metadados MySQL, desmarque a caixa de seleção ao lado do item antes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carregar os objetos no ou SQL Azure e migrar dados do MySQL.  
  
## <a name="next-step"></a>Próxima etapa  
[Convertendo bancos de dados MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados MySQL para SQL Server-BD SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
