---
title: Avaliando os esquemas do DB2 para conversão (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 8892f5a4-72ba-4406-8649-7a9d67f4c1d9
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8760cb01f1180908b4cd543a212316f402aaf998
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="assessing-db2-schemas-for-conversion-db2tosql"></a>Avaliando os esquemas do DB2 para conversão (DB2ToSQL)
Antes de carregar objetos e migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você deve determinar o quão complexo será a migração e quanto tempo levará a migração. O SSMA pode criar um relatório de avaliação que mostra o percentual de objetos que serão convertidos com êxito. O SSMA permite exibir os problemas específicos que causam falhas de conversão.  
  
## <a name="creating-assessment-reports"></a>Criando relatórios de avaliação  
Ao criar este relatório de avaliação, o SSMA converte os objetos de banco de dados do DB2 selecionados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxe e mostra os resultados.  
  
**Para criar um relatório de avaliação**  
  
1.  No Gerenciador de metadados do DB2, selecione os esquemas para avaliar.  
  
2.  Para omitir a objetos individuais, desmarque as caixas de seleção próximas a elas.  
  
3.  Clique com botão direito **esquemas**e, em seguida, selecione **criar relatório**.  
  
    Você também pode analisar os objetos individuais, clicando duas vezes um objeto e, em seguida, selecionando **criar relatório**.  
  
    O SSMA mostrará o andamento na barra de status na parte inferior da janela. Se o painel de saída estiver visível, você também verá mensagens no painel de saída.  
  
    Quando a avaliação for concluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Assistente de migração para DB2: janela de relatório de avaliação será exibida.  
  
## <a name="using-assessment-reports"></a>Usando relatórios de avaliação  
A janela de relatório de avaliação contém três painéis:  
  
-   O painel esquerdo contém a hierarquia de objetos que estão incluídos no relatório de avaliação. Você pode procurar a hierarquia e selecionar objetos e as categorias de objetos para exibir o código e as estatísticas de conversão.  
  
-   O conteúdo do painel direito depende do item selecionado no painel esquerdo.  
  
    Se um grupo de objetos estiver selecionado, esquema, ou se uma tabela for selecionada, o painel direito contém um painel de estatísticas de conversão e objetos pelo painel Categorias. O painel de estatísticas de conversão mostra as estatísticas de conversão para os objetos selecionados. Os objetos pelo painel categorias mostra as estatísticas de conversão para o objeto ou as categorias de objetos.  
  
    Se uma função, pacote, procedimento, sequência ou exibição for selecionada, o painel direito contém estatísticas, o código-fonte e o código de destino.  
  
    -   A área superior mostra as estatísticas gerais para o objeto. Talvez você precise expandir **estatísticas** para exibir essas informações.  
  
    -   A área de origem mostra o código-fonte do objeto selecionado no painel esquerdo. As áreas realçadas mostram código-fonte problemático.  
  
    -   A área de destino mostra o código convertido. Texto vermelho mostra mensagens de erro e de código problemáticas.  
  
-   O painel inferior mostra mensagens de conversão, agrupadas por número de mensagem. Você pode clicar em **erros**, **avisos**, ou **informações** para exibir categorias de mensagens e, em seguida, expanda um grupo de mensagens. Clique em uma mensagem individual para selecionar o objeto no painel esquerdo e exibir os detalhes no painel direito.  
  
## <a name="analyzing-conversion-problems-by-using-the-assessment-report"></a>Analisar problemas de conversão, usando o relatório de avaliação  
O painel de estatísticas de conversão mostra as estatísticas de conversão. Se a porcentagem para qualquer categoria é menor que 100%, você deve determinar por que a conversão não foi bem-sucedida.  
  
**Para exibir os problemas de conversão**  
  
1.  Crie o relatório de avaliação usando as instruções no procedimento anterior.  
  
2.  No painel esquerdo, expanda esquemas ou pastas que têm um ícone de erro vermelho. Continue expandindo itens até que você selecione um item individual que falha na conversão.  
  
3.  Na parte superior do painel de origem, clique em **próximo problema**.  
  
    O código problemática é realçado, conforme é o código relacionado no painel de navegação de destino.  
  
4.  Examine as mensagens de erro e, em seguida, determinar o que você deseja fazer com o objeto que causou o problema de conversão:  
  
    -   Atualize a sintaxe do DB2 em SSMA. Você pode atualizar a sintaxe para procedimentos, funções, gatilhos, funções de pacotes e pacotes. Para atualizar a sintaxe, selecione o objeto no painel Explorador de metadados do DB2, clique o **SQL** guia e, em seguida, modifique o código do SQL. Quando você sair do item, você será solicitado para salvar a sintaxe atualizada. Você pode exibir os erros relatados para o objeto no **relatório** guia.  
  
    -   No DB2, você pode modificar o objeto do DB2 para remover ou revisar código problemática. Para carregar o código atualizado no SSMA, você terá que atualizar os metadados. Para obter mais informações, consulte [se conectar ao banco de dados DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md).  
  
    -   Você pode excluir o objeto de migração. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados e o Gerenciador de metadados do DB2, desmarque a caixa de seleção ao lado do item antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e migrar dados do DB2.  
  
## <a name="next-step"></a>Próxima etapa  
[Convertendo esquemas DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Bancos de dados DB2 migrando para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
