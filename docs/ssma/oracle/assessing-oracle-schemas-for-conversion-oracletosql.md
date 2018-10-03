---
title: Avaliar esquemas Oracle para conversão (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Analyzing Conversion Problems
ms.assetid: 4de9bcf6-1346-4740-87f9-7f24a8226357
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: acf31c29b498562708c7cb049e89a0a7425fd31f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47631194"
---
# <a name="assessing-oracle-schemas-for-conversion-oracletosql"></a>Avaliação de esquemas Oracle para conversão (OracleToSQL)
Antes de carregar objetos e migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você deve determinar o quão complexo será a migração e quanto tempo levará a migração. O SSMA pode criar um relatório de avaliação que mostra o percentual de objetos que serão convertidos com êxito. O SSMA também permite que você exiba os problemas específicos que causam falhas de conversão.  
  
## <a name="creating-assessment-reports"></a>Criando relatórios de avaliação  
Quando ele cria esse relatório de avaliação, o SSMA converte os objetos de banco de dados Oracle selecionados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe e, em seguida, mostra os resultados.  
  
**Para criar um relatório de avaliação**  
  
1.  No Gerenciador de metadados do Oracle, selecione os esquemas para avaliar.  
  
2.  Para omitir objetos individuais, desmarque as caixas de seleção ao lado daqueles.  
  
3.  Clique com botão direito **esquemas**e, em seguida, selecione **criar relatório**.  
  
    Você também pode analisar os objetos individuais, clicando duas vezes um objeto e, em seguida, selecionando **criar relatório**.  
  
    O SSMA mostrará o progresso na barra de status na parte inferior da janela. Se o painel de saída estiver visível, você também verá mensagens no painel de saída.  
  
    Quando a avaliação for concluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Oracle: janela de relatório de avaliação será exibida.  
  
## <a name="using-assessment-reports"></a>Usando relatórios de avaliação  
A janela de relatório de avaliação contém três painéis:  
  
-   O painel esquerdo contém a hierarquia de objetos que estão incluídos no relatório de avaliação. Você pode procurar a hierarquia e selecionar objetos e as categorias de objetos para exibir o código e estatísticas de conversão.  
  
-   O conteúdo do painel direito depende do item selecionado no painel esquerdo.  
  
    Se um grupo de objetos for selecionado, esquema, ou se uma tabela for selecionada, o painel direito contém um painel de estatísticas de conversão e objetos pelo painel de categorias. O painel de estatísticas de conversão mostra as estatísticas de conversão para os objetos selecionados. Os objetos pelo painel de categorias mostra as estatísticas de conversão para o objeto ou categorias de objetos.  
  
    Se uma função, pacote, procedimento, sequência ou exibição for selecionada, o painel direito contém estatísticas, o código-fonte e o código de destino.  
  
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
  
4.  Examine as mensagens de erro e, em seguida, determinar o que você deseja fazer com o objeto que causou o problema de conversão:  
  
    -   Atualize a sintaxe do Oracle no SSMA. Você pode atualizar a sintaxe para procedimentos, funções, gatilhos, funções empacotadas e empacotados. Para atualizar a sintaxe, selecione o objeto no painel Gerenciador de metadados do Oracle, clique no **SQL** guia e, em seguida, modifique o código SQL. Quando você navegar para fora o item, você será solicitado para salvar a sintaxe atualizada. Você pode exibir os erros relatados para o objeto sobre o **relatório** guia.  
  
    -   No Oracle, você pode modificar o objeto do Oracle para remover ou revisar o código problemático. Para carregar o código atualizado no SSMA, você terá que atualizar os metadados. Para obter mais informações, consulte [conectar-se ao banco de dados Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
    -   Você pode excluir o objeto da migração. Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados e o Gerenciador de metadados do Oracle, desmarque a caixa de seleção próxima ao item antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e migrar dados do Oracle.  
  
## <a name="next-step"></a>Próxima etapa  
[Converter esquemas Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Migrando do Oracle bancos de dados para o SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
