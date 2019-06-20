---
title: Avaliar os objetos de banco de dados do SAP ASE para conversão (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eb996b7c-1eef-4f73-b5e6-2fa6faf7336c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e7d1b0b68835fe8b909369a87814a3d1c41e07d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240243"
---
# <a name="assessing-sap-ase-database-objects-for-conversion-sybasetosql"></a>Avaliar os objetos de banco de dados do SAP ASE para conversão (SybaseToSQL)
Antes de carregar objetos e migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, você deve determinar como complexidade da migração e quanto tempo deve levar. O SSMA pode criar um relatório de avaliação que mostra o percentual de objetos e procedimentos que serão convertidos com êxito para [!INCLUDE[tsql](../../includes/tsql-md.md)]. O SSMA também permite que você exiba os problemas específicos que podem causar falhas de conversão.  
  
## <a name="create-assessment-reports"></a>Criar relatórios de avaliação  
Ao criar este relatório de avaliação, o SSMA converte os objetos de banco de dados SAP Adaptive Server Enterprise (ASE) selecionados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou sintaxe SQL do Azure e, em seguida, mostra os resultados.  
  
**Para criar um relatório de avaliação**  
  
1.  No Gerenciador de metadados do Sybase, selecione os bancos de dados que você deseja avaliar.  
  
2.  Para omitir objetos individuais, desmarque as caixas de seleção ao lado de objetos que você não deseja avaliar.  
  
3.  Clique com botão direito **bancos de dados**e, em seguida, selecione **criar relatório**.  
  
    Você também pode analisar os objetos individuais, clicando duas vezes um objeto e, em seguida, selecionando **criar relatório**.  
  
    O SSMA mostra o progresso na barra de status na parte inferior da janela. Se o painel de saída estiver visível, você também verá quaisquer mensagens relacionadas.  
  
    Quando a avaliação for concluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Sybase: Janela de relatório de avaliação será exibida.  
  
## <a name="use-assessment-reports"></a>Usar relatórios de avaliação  
A janela de relatório de avaliação contém três painéis:  
  
-   O painel esquerdo contém a hierarquia de objetos que estão incluídos no relatório de avaliação. Você pode procurar a hierarquia e selecionar objetos e as categorias de objeto para exibir o código e estatísticas de conversão.  
  
-   O conteúdo do painel direito varia com base no qual o item está selecionado no painel esquerdo.  
  
    Se um grupo de objetos (como um esquema) ou uma tabela for selecionado, o painel direito exibe dois painéis. O **estatísticas de conversão** painel mostra as estatísticas de conversão para os objetos selecionados. O **objetos por categorias** painel mostra as estatísticas de conversão para o objeto ou categorias de objetos.  
  
    Se um procedimento armazenado, exibição ou gatilho for selecionado, o painel direito contém estatísticas, o código-fonte e o código de destino.  
  
    -   A área superior mostra as estatísticas gerais para o objeto. Talvez você precise expandir **estatísticas** para exibir essas informações. 
    -   A área de origem mostra o código-fonte do objeto selecionado no painel esquerdo. As áreas destacadas mostram o código-fonte problemático.  
    -   A área de destino mostra o código convertido. Texto vermelho mostra mensagens de erro e de código problemáticas.  
  
-   O painel inferior mostra mensagens de conversão, agrupadas por número da mensagem. Selecione **erros**, **avisos**, ou **informações** exibir categorias de mensagens e, em seguida, expanda um grupo de mensagens. Clique em uma mensagem individual para selecionar o objeto no painel esquerdo e, em seguida, exibir os detalhes no painel direito.  
  
## <a name="analyze-conversion-problems-by-using-the-assessment-report"></a>Analisar problemas de conversão, usando o relatório de avaliação  
O **painéis de estatísticas de conversão** mostram as estatísticas de conversão. Se a porcentagem para qualquer categoria for menor que 100%, você deve determinar por que a conversão não foi bem-sucedida.  
  
**Para exibir os problemas de conversão**  
  
1.  Crie o relatório de avaliação usando as instruções no procedimento anterior.  
  
2.  No painel esquerdo, expanda esquemas ou pastas que têm um ícone vermelho de erro. Continue expandindo itens até que você selecione um item individual que falha na conversão.  
  
3.  Na parte superior do painel de código-fonte, selecione **próximo problema**.  
    O código problemático é realçado, assim como é o código relacionado na **navegação de destino** painel.  
  
4.  Examine as mensagens de erro e, em seguida, determinar o que você deseja fazer com o objeto que causou o problema de conversão:  
  
    -   Atualize a sintaxe do ASE no SSMA. Você pode atualizar a sintaxe apenas para procedimentos armazenados e gatilhos. Para atualizar a sintaxe, selecione o objeto no painel Gerenciador de metadados do Sybase, clique o **SQL** guia e, em seguida, edite o código SQL. Quando você navegar para fora o item, você precisará salvar a sintaxe atualizada. Exibir os erros relatados para o objeto sobre o **relatório** guia.  
  
    -   Em ASE, você pode alterar o objeto de ASE para remover ou revisar o código problemático. Para carregar o código atualizado no SSMA, você terá que atualizar os metadados. Para obter mais informações, consulte [conectar-se ao Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
    -   Você pode excluir o objeto da migração. Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Gerenciador de metadados do SQL Azure e o Gerenciador de metadados do Sybase, desmarque a caixa de seleção próxima ao item antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o SQL Azure e migrar dados do ASE.
  
## <a name="next-steps"></a>Próximas etapas  
[Converter objetos de banco de dados ASE do SAP &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Migrando SAP ASE bancos de dados SQL Server – BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
