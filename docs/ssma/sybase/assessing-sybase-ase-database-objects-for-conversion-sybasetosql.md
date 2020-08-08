---
title: Avaliando objetos de banco de dados SAP ASE para conversão (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eb996b7c-1eef-4f73-b5e6-2fa6faf7336c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: fba4692780b9f9f2c556634bf1676bc00bbba169
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87932607"
---
# <a name="assessing-sap-ase-database-objects-for-conversion-sybasetosql"></a>Avaliando objetos de banco de dados SAP ASE para conversão (SybaseToSQL)
Antes de carregar objetos e migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o ou SQL do Azure, você deve determinar como a complexidade da migração e quanto tempo deve levar. O SSMA pode criar um relatório de avaliação que mostra a porcentagem de objetos e procedimentos que serão convertidos com êxito em [!INCLUDE[tsql](../../includes/tsql-md.md)] . O SSMA também permite que você exiba os problemas específicos que podem causar falhas de conversão.  
  
## <a name="create-assessment-reports"></a>Criar relatórios de avaliação  
Ao criar esse relatório de avaliação, o SSMA converte os objetos de banco de dados do ASE (SAP Adaptive Server Enterprise) selecionados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou na sintaxe SQL do Azure e, em seguida, mostra os resultados.  
  
**Para criar um relatório de avaliação**  
  
1.  No Gerenciador de metadados do Sybase, selecione os bancos de dados que você deseja avaliar.  
  
2.  Para omitir objetos individuais, desmarque as caixas de seleção ao lado dos objetos que você não deseja avaliar.  
  
3.  Clique com o botão direito do mouse em **bancos de dados**e selecione **criar relatório**.  
  
    Você também pode analisar objetos individuais clicando com o botão direito do mouse em um objeto e selecionando **criar relatório**.  
  
    O SSMA mostra o progresso na barra de status na parte inferior da janela. Se o painel de saída estiver visível, você também verá todas as mensagens relacionadas.  
  
    Quando a avaliação for concluída, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] janela Assistente de migração for Sybase: relatório de avaliação será exibida.  
  
## <a name="use-assessment-reports"></a>Usar relatórios de avaliação  
A janela relatório de avaliação contém três painéis:  
  
-   O painel esquerdo contém a hierarquia de objetos que são incluídos no relatório de avaliação. Você pode procurar a hierarquia e selecionar objetos e categorias de objeto para exibir estatísticas e código de conversão.  
  
-   O conteúdo do painel direito varia de acordo com o item selecionado no painel esquerdo.  
  
    Se um grupo de objetos (como um esquema) ou uma tabela for selecionada, o painel direito exibirá dois painéis. O painel **Estatísticas de conversão** mostra as estatísticas de conversão para os objetos selecionados. O painel **objetos por categorias** mostra as estatísticas de conversão para o objeto ou as categorias de objetos.  
  
    Se um procedimento armazenado, modo de exibição ou gatilho for selecionado, o painel direito conterá estatísticas, código-fonte e código de destino.  
  
    -   A área superior mostra as estatísticas gerais do objeto. Talvez seja necessário expandir as **estatísticas** para exibir essas informações. 
    -   A área de origem mostra o código-fonte do objeto selecionado no painel esquerdo. As áreas realçadas mostram o código-fonte problemático.  
    -   A área de destino mostra o código convertido. Texto vermelho mostra código problemático e mensagens de erro.  
  
-   O painel inferior mostra as mensagens de conversão, agrupadas por número de mensagem. Selecione **erros**, **avisos**ou **informações** para exibir categorias de mensagens e, em seguida, expanda um grupo de mensagens. Clique em uma mensagem individual para selecionar o objeto no painel esquerdo e, em seguida, exiba os detalhes no painel direito.  
  
## <a name="analyze-conversion-problems-by-using-the-assessment-report"></a>Analisar problemas de conversão usando o relatório de avaliação  
Os **painéis de estatísticas de conversão** mostram as estatísticas de conversão. Se a porcentagem de qualquer categoria for menor que 100%, você deverá determinar por que a conversão não foi bem-sucedida.  
  
**Para exibir problemas de conversão**  
  
1.  Crie o relatório de avaliação usando as instruções no procedimento anterior.  
  
2.  No painel esquerdo, expanda esquemas ou pastas que têm um ícone de erro vermelho. Continue expandindo itens até selecionar um item individual que falhou na conversão.  
  
3.  Na parte superior do painel de origem, selecione **próximo problema**.  
    O código problemático é realçado, assim como o código relacionado no painel de **navegação de destino** .  
  
4.  Revise Todas as mensagens de erro e determine o que você deseja fazer com o objeto que causou o problema de conversão:  
  
    -   Atualize a sintaxe do ASE no SSMA. Você pode atualizar a sintaxe somente para procedimentos armazenados e gatilhos. Para atualizar a sintaxe, selecione o objeto no painel Gerenciador de metadados do Sybase, clique na guia **SQL** e edite o código SQL. Ao sair do item, você será solicitado a salvar a sintaxe atualizada. Exiba os erros relatados para o objeto na guia **relatório** .  
  
    -   No ASE, você pode alterar o objeto ASE para remover ou revisar o código problemático. Para carregar o código atualizado no SSMA, você precisará atualizar os metadados. Para obter mais informações, consulte [conectando-se ao Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
    -   Você pode excluir o objeto da migração. No ou no Gerenciador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados do SQL do Azure e no Gerenciador de metadados Sybase, desmarque a caixa de seleção ao lado do item antes de carregar os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL do Azure e migrar dados do ase.
  
## <a name="next-steps"></a>Próximas etapas  
[Convertendo objetos de banco de dados SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Migrar bancos de dados do SAP ASE para o SQL Server-Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
