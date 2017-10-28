---
title: "Avaliando os bancos de dados MySQL para conversão (MySQLToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Assessment reports
ms.assetid: 2a56a003-3b0f-453a-963c-00c9e40933ec
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 24e18761f50997b32da67a8ed2277259f5d53516
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="assessing-mysql-databases-for-conversion-mysqltosql"></a>Avaliando os bancos de dados MySQL para conversão (MySQLToSQL)
Antes de carregar objetos e migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, você deve determinar como complexo será a migração e quanto tempo levará a migração. O SSMA pode criar um relatório de avaliação que mostra o percentual de objetos que serão convertidos com êxito. O SSMA permite exibir os problemas específicos que causam falhas de conversão.  
  
## <a name="creating-assessment-reports"></a>Criando relatórios de avaliação  
Ao criar este relatório de avaliação, o SSMA converte os objetos de banco de dados MySQL selecionados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou sintaxe de SQL Azure e, em seguida, mostra os resultados.  
  
**Para criar um relatório de avaliação**  
  
1.  No Gerenciador de metadados do MySQL, selecione os esquemas para avaliar.  
  
2.  Para omitir a objetos individuais, desmarque as caixas de seleção próximas a elas.  
  
3.  Clique com botão direito **esquemas**e, em seguida, selecione **criar relatório**.  
  
    Clique um objeto para analisar objetos individuais. Em seguida, selecione **criar relatório**.  
  
    O SSMA mostrará o andamento na barra de status na parte inferior da janela. Se o painel de saída estiver visível, você também verá mensagens no painel de saída.  
  
    Quando a avaliação for concluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Assistente de migração para MySQL, a janela de relatório de avaliação será exibida.  
  
## <a name="using-assessment-reports"></a>Usando relatórios de avaliação  
A janela de relatório de avaliação contém três painéis:  
  
-   O painel esquerdo contém a hierarquia de objetos que estão incluídos no relatório de avaliação. Você pode procurar a hierarquia e selecionar objetos e as categorias de objetos para exibir o código e as estatísticas de conversão.  
  
-   O conteúdo do painel direito depende do item selecionado no painel esquerdo.  
  
    Se um grupo de objetos for selecionado, como o esquema, o painel direito contém um painel de estatísticas de conversão e objetos pelo painel Categorias. O painel de estatísticas de conversão mostra as estatísticas de conversão para os objetos selecionados. Os objetos pelo painel categorias mostra as estatísticas de conversão para o objeto ou as categorias de objetos.  
  
    Se uma função, o procedimento, a tabela ou a exibição for selecionada, o painel direito contém estatísticas, o código-fonte e o código de destino.  
  
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
  
4.  Examine as mensagens de erro e, em seguida, determinar o que você deseja fazer com o objeto que causou o problema de conversão.  
  
-   Atualize a sintaxe do MySQL em SSMA. Você pode atualizar a sintaxe apenas para procedimentos e funções. Para atualizar a sintaxe, selecione o objeto no painel Explorador de metadados do MySQL, clique o **SQL** guia e, em seguida, modifique o código do SQL. Quando você sair do item, você será solicitado para salvar a sintaxe atualizada. Você pode exibir os erros relatados para o objeto no **relatório** guia.  
  
-   No MySQL, você pode modificar o objeto do MySQL para remover ou revisar código problemática. Para carregar o código atualizado no SSMA, você terá que atualizar os metadados. Para obter mais informações, consulte [se conectar ao MySQL &#40; MySQLToSQL &#41; ](../../ssma/mysql/connecting-to-mysql-mysqltosql.md).  
  
-   Você pode excluir o objeto de migração. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados do SQL Azure e o Gerenciador de metadados do MySQL, desmarque a caixa de seleção ao lado do item antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure e migrar dados do MySQL.  
  
## <a name="next-step"></a>Próxima etapa  
[Conversão de bancos de dados MySQL &#40; MySQLToSQL &#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados MySQL para o SQL Server - banco de dados SQL do Azure &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

