---
title: "Avaliar os objetos de banco de dados Sybase ASE para conversão (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: eb996b7c-1eef-4f73-b5e6-2fa6faf7336c
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9683542427256511b961ad8f6ffd74af43eb23d5
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="assessing-sybase-ase-database-objects-for-conversion-sybasetosql"></a>Avaliar os objetos do Sybase ASE banco de dados de conversão (SybaseToSQL)
Antes de carregar objetos e migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, você deve determinar como complexo será a migração e quanto tempo levará a migração. O SSMA pode criar um relatório de avaliação que mostra o percentual de objetos e procedimentos que serão convertidos com êxito em [!INCLUDE[tsql](../../includes/tsql_md.md)]. O SSMA permite exibir os problemas específicos que causarão falhas de conversão.  
  
## <a name="creating-assessment-reports"></a>Criando relatórios de avaliação  
Ao criar este relatório de avaliação, o SSMA converte os objetos de banco de dados do Sybase Adaptive Server Enterprise (ASE) selecionados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou sintaxe de SQL Azure e, em seguida, mostra os resultados.  
  
**Para criar um relatório de avaliação**  
  
1.  No Gerenciador de metadados do Sybase, selecione os bancos de dados que você deseja avaliar.  
  
2.  Para omitir a objetos individuais, desmarque as caixas de seleção ao lado dos objetos que você não deseja avaliar.  
  
3.  Clique com botão direito **bancos de dados**e, em seguida, selecione **criar relatório**.  
  
    Você também pode analisar os objetos individuais, clicando duas vezes um objeto e, em seguida, selecionando **criar relatório**.  
  
    O SSMA mostrará o andamento na barra de status na parte inferior da janela. Se o painel de saída estiver visível, você também verá mensagens no painel de saída.  
  
    Quando a avaliação for concluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Assistente de migração para Sybase: janela de relatório de avaliação será exibida.  
  
## <a name="using-assessment-reports"></a>Usando relatórios de avaliação  
A janela de relatório de avaliação contém três painéis:  
  
-   O painel esquerdo contém a hierarquia de objetos que estão incluídos no relatório de avaliação. Você pode procurar a hierarquia e selecionar objetos e as categorias de objetos para exibir estatísticas de conversão e código.  
  
-   O conteúdo do painel direito depende do item selecionado no painel esquerdo.  
  
    Se um grupo de objetos é selecionado, nesse esquema, ou uma tabela é selecionado o painel direito contém um painel de estatísticas de conversão e objetos pelo painel Categorias. O painel de estatísticas de conversão mostra as estatísticas de conversão para os objetos selecionados. Os objetos pelo painel categorias mostra as estatísticas de conversão para o objeto ou as categorias de objetos.  
  
    Se um procedimento armazenado, exibição ou gatilho for selecionado, o painel direito contém estatísticas, o código-fonte e o código de destino.  
  
    -   A área superior mostra as estatísticas gerais para o objeto. Talvez você precise expandir **estatísticas** para exibir essas informações.  
  
    -   A área de origem mostra o código-fonte do objeto selecionado no painel esquerdo. As áreas realçadas mostram código-fonte problemático.  
  
    -   A área de destino mostra o código convertido. Texto vermelho mostra mensagens de erro e de código problemáticas.  
  
-   O painel inferior mostra mensagens de conversão, agrupadas por número de mensagem. Você pode clicar em **erros**, **avisos**, ou **informações** para exibir categorias de mensagens e, em seguida, expanda um grupo de mensagens. Clique em uma mensagem individual para selecionar o objeto no painel esquerdo e exibir os detalhes no painel direito.  
  
## <a name="analyzing-conversion-problems-using-the-assessment-report"></a>Analisar problemas de conversão, usando o relatório de avaliação  
Os painéis de estatísticas de conversão mostram as estatísticas de conversão. Se a porcentagem para qualquer categoria é menor que 100%, você deve determinar por que a conversão não foi bem-sucedida.  
  
**Para exibir os problemas de conversão**  
  
1.  Crie o relatório de avaliação usando as instruções no procedimento anterior.  
  
2.  No painel esquerdo, expanda esquemas ou pastas que têm um ícone de erro vermelho. Continue expandindo itens até que você selecione um item individual que falha na conversão.  
  
3.  Na parte superior do painel de origem, clique em **próximo problema**.  
  
    O código problemática é realçado, conforme é o código relacionado no painel de navegação de destino.  
  
4.  Examine as mensagens de erro e, em seguida, determinar o que você deseja fazer com o objeto que causou o problema de conversão:  
  
    -   Atualize a sintaxe de ASE em SSMA. Você pode atualizar a sintaxe apenas para procedimentos armazenados e gatilhos. Para atualizar a sintaxe, selecione o objeto no painel Explorador de metadados do Sybase, clique o **SQL** guia e, em seguida, edite o código SQL. Quando você sair do item, você será solicitado para salvar a sintaxe atualizada. Você pode exibir os erros relatados para o objeto no **relatório** guia.  
  
    -   Em ASE, você pode alterar o objeto ASE para remover ou revisar código problemática. Para carregar o código atualizado no SSMA, você terá que atualizar os metadados. Para obter mais informações, consulte [conectando para Sybase ASE &#40; SybaseToSQL &#41; ](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
    -   Você pode excluir o objeto de migração. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados do SQL Azure e o Gerenciador de metadados do Sybase, desmarque a caixa de seleção ao lado do item antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure e migrar dados de ASE.  
  
## <a name="next-step"></a>Próxima etapa  
[Converter objetos do Sybase ASE banco de dados &#40; SybaseToSQL &#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Migrando Sybase ASE bancos de dados do SQL Server - banco de dados SQL do Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

