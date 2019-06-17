---
title: Avaliar os bancos de dados MySQL para conversão (MySQLToSQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 9983edb500e424be6bbb4f85ff005af00fd65aaf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63253244"
---
# <a name="assessing-mysql-databases-for-conversion-mysqltosql"></a>Avaliar os bancos de dados MySQL para conversão (MySQLToSQL)
Antes de carregar objetos e migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, você deve determinar quão complexo será a migração e quanto tempo levará a migração. O SSMA pode criar um relatório de avaliação que mostra o percentual de objetos que serão convertidos com êxito. O SSMA também permite que você exiba os problemas específicos que causam falhas de conversão.  
  
## <a name="creating-assessment-reports"></a>Criando relatórios de avaliação  
Quando ele cria esse relatório de avaliação, o SSMA converte os objetos de banco de dados MySQL selecionados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou sintaxe de SQL Azure e, em seguida, mostra os resultados.  
  
**Para criar um relatório de avaliação**  
  
1.  No Gerenciador de metadados do MySQL, selecione os esquemas para avaliar.  
  
2.  Para omitir objetos individuais, desmarque as caixas de seleção ao lado daqueles.  
  
3.  Clique com botão direito **esquemas**e, em seguida, selecione **criar relatório**.  
  
    Clique com botão direito a um objeto para analisar objetos individuais. Em seguida, selecione **criar relatório**.  
  
    O SSMA mostrará o progresso na barra de status na parte inferior da janela. Se o painel de saída estiver visível, você também verá mensagens no painel de saída.  
  
    Quando a avaliação for concluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de migração para MySQL, a janela relatório de avaliação será exibida.  
  
## <a name="using-assessment-reports"></a>Usando relatórios de avaliação  
A janela de relatório de avaliação contém três painéis:  
  
-   O painel esquerdo contém a hierarquia de objetos que estão incluídos no relatório de avaliação. Você pode procurar a hierarquia e selecionar objetos e as categorias de objetos para exibir o código e estatísticas de conversão.  
  
-   O conteúdo do painel direito depende do item selecionado no painel esquerdo.  
  
    Se um grupo de objetos for selecionado, como o esquema, o painel direito contém um painel de estatísticas de conversão e objetos pelo painel de categorias. O painel de estatísticas de conversão mostra as estatísticas de conversão para os objetos selecionados. Os objetos pelo painel de categorias mostra as estatísticas de conversão para o objeto ou categorias de objetos.  
  
    Se uma função, o procedimento, a tabela ou a exibição for selecionada, o painel direito contém estatísticas, o código-fonte e o código de destino.  
  
    -   A área superior mostra as estatísticas gerais para o objeto. Talvez você precise expandir **estatísticas** para exibir essas informações.  
  
    -   A área de origem mostra o código-fonte do objeto selecionado no painel esquerdo. As áreas destacadas mostram o código-fonte problemático.  
  
    -   A área de destino mostra o código convertido. Texto vermelho mostra mensagens de erro e de código problemáticas.  
  
-   O painel inferior mostra mensagens de conversão, agrupadas por número da mensagem. Você pode clicar em **erros**, **avisos**, ou **informações** exibir categorias de mensagens e, em seguida, expanda um grupo de mensagens. Clique em uma mensagem individual para selecionar o objeto no painel esquerdo e exibir os detalhes no painel direito.  
  
## <a name="analyzing-conversion-problems-by-using-the-assessment-report"></a>Analisar problemas de conversão, usando o relatório de avaliação  
O painel de estatísticas de conversão mostra as estatísticas de conversão. Se a porcentagem para qualquer categoria for menor que 100%, você deve determinar por que a conversão não foi bem-sucedida.  
  
**Para exibir os problemas de conversão**  
  
1.  Crie o relatório de avaliação usando as instruções no procedimento anterior.  
  
2.  No painel esquerdo, expanda esquemas ou pastas que têm um ícone vermelho de erro. Continue expandindo itens até que você selecione um item individual que falha na conversão.  
  
3.  Na parte superior do painel de código-fonte, clique em **próximo problema**.  
  
    O código problemático é realçado, assim como é o código relacionado no painel de navegação de destino.  
  
4.  Examine as mensagens de erro e, em seguida, determinar o que você deseja fazer com o objeto que causou o problema de conversão.  
  
-   Atualize a sintaxe do MySQL no SSMA. Você pode atualizar a sintaxe apenas para procedimentos e funções. Para atualizar a sintaxe, selecione o objeto no painel Gerenciador de metadados do MySQL, clique o **SQL** guia e, em seguida, modifique o código SQL. Quando você navegar para fora o item, você será solicitado para salvar a sintaxe atualizada. Você pode exibir os erros relatados para o objeto sobre o **relatório** guia.  
  
-   No MySQL, você pode modificar o objeto do MySQL para remover ou revisar o código problemático. Para carregar o código atualizado no SSMA, você terá que atualizar os metadados. Para obter mais informações, consulte [conectando ao MySQL a &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md).  
  
-   Você pode excluir o objeto da migração. Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Gerenciador de metadados do SQL Azure e o Gerenciador de metadados do MySQL, desmarque a caixa de seleção próxima ao item antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure e migrar dados do MySQL.  
  
## <a name="next-step"></a>Próxima etapa  
[Converter bancos de dados MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Migrando MySQL bancos de dados para o SQL Server – BD SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
