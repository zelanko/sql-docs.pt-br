---
title: Avaliar os objetos de banco de dados do SAP ASE para conversão (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: eb996b7c-1eef-4f73-b5e6-2fa6faf7336c
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7f28d8f35adacfa4443ed804e1233386f3794606
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="assessing-sap-ase-database-objects-for-conversion-sybasetosql"></a>Avaliar os objetos de banco de dados do SAP ASE para conversão (SybaseToSQL)
Antes de carregar objetos e migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, você deve determinar como complexidade da migração e quanto tempo deve demorar. O SSMA pode criar um relatório de avaliação que mostra o percentual de objetos e procedimentos com êxito serão convertidos em [!INCLUDE[tsql](../../includes/tsql_md.md)]. O SSMA permite exibir os problemas específicos que podem causar falhas de conversão.  
  
## <a name="create-assessment-reports"></a>Criar relatórios de avaliação  
Ao criar este relatório de avaliação, o SSMA converte os objetos de banco de dados SAP Adaptive Server Enterprise (ASE) selecionados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou sintaxe de SQL do Azure e, em seguida, mostra os resultados.  
  
**Para criar um relatório de avaliação**  
  
1.  No Gerenciador de metadados do Sybase, selecione os bancos de dados que você deseja avaliar.  
  
2.  Para omitir a objetos individuais, desmarque as caixas de seleção ao lado dos objetos que você não deseja avaliar.  
  
3.  Clique com botão direito **bancos de dados**e, em seguida, selecione **criar relatório**.  
  
    Você também pode analisar os objetos individuais, clicando duas vezes um objeto e, em seguida, selecionando **criar relatório**.  
  
    O SSMA mostra o progresso na barra de status na parte inferior da janela. Se o painel de saída estiver visível, você também verá todas as mensagens relacionadas.  
  
    Quando a avaliação for concluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Assistente de migração para Sybase: janela de relatório de avaliação será exibida.  
  
## <a name="use-assessment-reports"></a>Usar relatórios de avaliação  
A janela de relatório de avaliação contém três painéis:  
  
-   O painel esquerdo contém a hierarquia de objetos que estão incluídos no relatório de avaliação. Você pode procurar a hierarquia e selecionar objetos e categorias de objeto para exibir o código e as estatísticas de conversão.  
  
-   O conteúdo do painel direito varia com base no item selecionado no painel esquerdo.  
  
    Se um grupo de objetos (como um esquema) ou uma tabela for selecionado, o painel direito exibe dois painéis. O **estatísticas de conversão** painel mostra as estatísticas de conversão para os objetos selecionados. O **objetos por categorias** painel mostra as estatísticas de conversão para o objeto ou as categorias de objetos.  
  
    Se um procedimento armazenado, exibição ou gatilho for selecionado, o painel direito contém estatísticas, o código-fonte e o código de destino.  
  
    -   A área superior mostra as estatísticas gerais para o objeto. Talvez você precise expandir **estatísticas** para exibir essas informações. 
    -   A área de origem mostra o código-fonte do objeto selecionado no painel esquerdo. As áreas realçadas mostram código-fonte problemático.  
    -   A área de destino mostra o código convertido. Texto vermelho mostra mensagens de erro e de código problemáticas.  
  
-   O painel inferior mostra mensagens de conversão, agrupadas por número de mensagem. Selecione **erros**, **avisos**, ou **informações** para exibir categorias de mensagens e, em seguida, expanda um grupo de mensagens. Clique em uma mensagem individual, selecione o objeto no painel esquerdo e em seguida, exiba os detalhes no painel direito.  
  
## <a name="analyze-conversion-problems-by-using-the-assessment-report"></a>Analisar problemas de conversão, usando o relatório de avaliação  
O **painéis de estatísticas de conversão** mostrar as estatísticas de conversão. Se a porcentagem para qualquer categoria é menor que 100%, você deve determinar por que a conversão não foi bem-sucedida.  
  
**Para exibir os problemas de conversão**  
  
1.  Crie o relatório de avaliação usando as instruções no procedimento anterior.  
  
2.  No painel esquerdo, expanda esquemas ou pastas que têm um ícone de erro vermelho. Continue expandindo itens até que você selecione um item individual que falha na conversão.  
  
3.  Na parte superior do painel de fonte, selecione **próximo problema**.  
    O código problemática é realçado, conforme é o código relacionado a **navegação de destino** painel.  
  
4.  Examine as mensagens de erro e, em seguida, determinar o que você deseja fazer com o objeto que causou o problema de conversão:  
  
    -   Atualize a sintaxe de ASE em SSMA. Você pode atualizar a sintaxe apenas para procedimentos armazenados e gatilhos. Para atualizar a sintaxe, selecione o objeto no painel Explorador de metadados do Sybase, clique o **SQL** guia e, em seguida, edite o código SQL. Quando você sair do item, você precisará salvar a sintaxe atualizada. Exibir os erros relatados para o objeto no **relatório** guia.  
  
    -   Em ASE, você pode alterar o objeto ASE para remover ou revisar código problemática. Para carregar o código atualizado no SSMA, você terá que atualizar os metadados. Para obter mais informações, consulte [conectando para Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
    -   Você pode excluir o objeto de migração. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados do SQL Azure e o Gerenciador de metadados do Sybase, desmarque a caixa de seleção ao lado do item antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure e migrar dados de ASE.
  
## <a name="next-steps"></a>Próximas etapas  
[Converter objetos de banco de dados ASE SAP &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Migrando SAP ASE bancos de dados do SQL Server - banco de dados SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
