---
title: Avaliando os esquemas Oracle para conversão (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Analyzing Conversion Problems
ms.assetid: 4de9bcf6-1346-4740-87f9-7f24a8226357
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: f8aaa58da9e9ace704d6214dcc56cab997fe082e
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935057"
---
# <a name="assessing-oracle-schemas-for-conversion-oracletosql"></a>Avaliação de esquemas Oracle para conversão (OracleToSQL)
Antes de carregar objetos e migrar dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você deve determinar a complexidade da migração e a quantidade de tempo que a migração levará. O SSMA pode criar um relatório de avaliação que mostra a porcentagem de objetos que serão convertidos com êxito. O SSMA também permite que você exiba os problemas específicos que causam falhas de conversão.  
  
## <a name="creating-assessment-reports"></a>Criando relatórios de avaliação  
Quando ele cria esse relatório de avaliação, o SSMA converte os objetos de banco de dados Oracle selecionados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe e, em seguida, mostra os resultados.  
  
**Para criar um relatório de avaliação**  
  
1.  No Gerenciador de metadados Oracle, selecione os esquemas a serem avaliados.  
  
2.  Para omitir objetos individuais, desmarque as caixas de seleção ao lado delas.  
  
3.  Clique com o botão direito do mouse em **esquemas**e selecione **criar relatório**.  
  
    Você também pode analisar objetos individuais clicando com o botão direito do mouse em um objeto e selecionando **criar relatório**.  
  
    O SSMA mostrará o progresso na barra de status na parte inferior da janela. Se o painel de saída estiver visível, você também verá mensagens no painel de saída.  
  
    Quando a avaliação for concluída, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] janela Assistente de migração para Oracle: relatório de avaliação será exibida.  
  
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
  
    -   Atualize a sintaxe do Oracle no SSMA. Você pode atualizar a sintaxe para procedimentos, funções, gatilhos, funções empacotadas e procedimentos empacotados. Para atualizar a sintaxe, selecione o objeto no painel do Gerenciador de metadados Oracle, clique na guia **SQL** e, em seguida, modifique o código SQL. Ao sair do item, você será solicitado a salvar a sintaxe atualizada. Você pode exibir os erros relatados para o objeto na guia **relatório** .  
  
    -   No Oracle, você pode modificar o objeto Oracle para remover ou revisar o código problemático. Para carregar o código atualizado no SSMA, você precisará atualizar os metadados. Para obter mais informações, consulte [conectando-se a Oracle Database &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
    -   Você pode excluir o objeto da migração. No Gerenciador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados e no Gerenciador de metadados Oracle, desmarque a caixa de seleção ao lado do item antes de carregar os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e migrar dados do Oracle.  
  
## <a name="next-step"></a>Próxima etapa  
[Convertendo esquemas Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados Oracle para SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
