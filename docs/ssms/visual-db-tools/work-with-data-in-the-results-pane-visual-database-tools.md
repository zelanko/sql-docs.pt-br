---
title: Trabalhar com os dados no painel de resultados (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- queries [Visual Database Tools]
- result sets [SQL Server], queries
- Query Designer [SQL Server], Results pane
- results [SQL Server], query
- Visual Database Tools [SQL Server], queries
- queries [SQL Server], results
- Results pane
ms.assetid: 4f8a0080-91ef-4442-83ae-53be2f478c54
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4b8860af3af85b004da53a7fd218032e65d732f3
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105297"
---
# <a name="work-with-data-in-the-results-pane-visual-database-tools"></a>Trabalhar com dados no painel de resultados (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Depois que você executa ou exibe uma consulta, os resultados são mostrados no painel Resultados. Em seguida, você pode trabalhar com esses resultados. Por exemplo, você pode adicionar e excluir linhas, inserir ou alterar dados e navegar facilmente por grandes conjuntos de resultados.  
  
As informações a seguir podem ajudá-lo a evitar problemas e a trabalhar de maneira eficaz com os seus conjuntos de resultados.  
  
## <a name="returning-the-results-set"></a>Retornando os conjuntos de resultados  
Você pode retornar os resultados de uma consulta ou uma exibição e optar por abrir apenas o painel de resultados ou todos os painéis. Em ambos os casos a consulta ou exibição abrirá o Designer de Consulta e Exibição. A diferença é que um abre mostrando apenas o painel Resultados, enquanto o outro abre com todas as janelas que foram selecionadas na caixa de diálogo Opções. Os quatro painéis (Resultados, SQL, Diagrama e Critérios) são o padrão.  
  
Para obter mais informações, consulte [Abrir consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/open-queries-visual-database-tools.md).  
  
Para alterar o design da consulta ou da exibição para que ela retorne um conjunto de resultados diferente ou retorne os registros em ordem diferente, consulte os tópicos listados em [Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md).  
  
Você também pode determinar se deseja retornar todos ou parte dos conjuntos de resultados, de duas formas: parar a consulta que está em execução ou selecionar a quantidade de resultados a serem retornados antes da execução da consulta.  
  
## <a name="navigating-in-the-results-pane"></a>Navegando no painel de resultados  
Você pode navegar rapidamente pelos registros, utilizando a barra de navegação da parte inferior do painel Resultados.  
  
Há botões para seguir até o primeiro e o último registro, registros anteriores e posteriores, e para seguir até determinado registro.  
  
Para ir até um registro específico, digite o número da linha na caixa de texto da barra de navegação e pressione ENTER.  
  
Para obter informações sobre como usar atalhos de teclado no Designer de Consulta e Exibição, veja [Navegar no Designer de Consulta e Exibição &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/navigate-in-the-query-and-view-designer-visual-database-tools.md).  
  
## <a name="committing-changes-to-the-database"></a>Confirmando alterações do banco de dados  
O painel Resultados usa controle de simultaneidade otimista, de modo que a grade mostra uma cópia dos dados do banco de dados, em lugar de uma exibição totalmente ao vivo. Dessa forma, as alterações só são confirmadas no banco de dados depois que se sai de uma linha. Isso permite que mais de um usuário trabalhe simultaneamente com o banco de dados. Se houver conflitos (por exemplo, se outro usuário alterar a mesma linha que você alterou e confirmá-la no banco de dados antes de você) você receberá uma mensagem informando sobre o conflito e oferecendo soluções.  
  
## <a name="undo-changes-using-esc"></a>Desfazer alterações usando ESC  
Só é possível desfazer alterações que tenham sido confirmadas no banco de dados. Os dados não são confirmados se você não tiver saído do registro, ou logo que você saia do registro obterá uma mensagem de erro indicando que a alteração não será confirmada. Se a alteração não tiver sido confirmada você poderá desfazê-la usando a tecla ESC.  
  
Para desfazer todas as alterações de uma linha, vá para uma célula da linha que não tenha sido editada, e pressione a tecla ESC.  
  
Para desfazer alterações de uma determinada célula que você editou, vá para essa célula e pressione a tecla ESC.  
  
## <a name="adding-or-deleting-data-in-the-database"></a>Adicionando ou excluindo dados do banco de dados  
Para verificar como está funcionando o design do banco de dados, talvez seja necessário adicionar dados de exemplo ao banco de dados. É possível inseri-los diretamente no painel de resultados, ou copiá-los de outro programa, como do Bloco de notas ou Excel, depois os colando no painel de resultados.  
  
Além de copiar linhas no painel Resultados, você poderá adicionar registros novos, modificando ou excluindo os existentes. Para obter mais informações, consulte [Adicionar novas linhas no painel de Resultados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-new-rows-in-the-results-pane-visual-database-tools.md), [Excluir linhas no painel de Resultados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/delete-rows-in-the-results-pane-visual-database-tools.md) e [Editar linhas no painel de Resultados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/edit-rows-in-the-results-pane-visual-database-tools.md).  
  
## <a name="tips-for-working-with-null-values-and-empty-cells"></a>Dicas para trabalhar com valores NULL e células vazias  
Quando você clica em uma linha vazia para adicionar um novo registro, o valor inicial de todas as colunas é *NULL*. A coluna que permitir valores nulos pode ser deixada como está.  
  
Para substituir um valor não nulo por um nulo, digite NULL em letras maiúsculas. O painel Resultados colocará a palavra em itálico para indicar que o valor deve ser reconhecido como nulo e não como cadeia de caracteres.  
  
Para digitar a cadeia de caracteres "nula" digite as letras sem aspas. Quando pelo menos uma das letras estiver em minúscula, o valor será tratado como cadeia de caracteres e não como valor nulo.  
  
Valores de colunas com tipo de dados binário terão valores NULL por padrão. Esses valores não podem ser alterados no painel Resultados.  
  
Para inserir um espaço vazio em vez de usar valor nulo, exclua o texto existente e saia da célula.  
  
## <a name="validating-data"></a>Validando dados  
O Designer de Consulta e Exibição pode validar alguns tipos de dados segundo as propriedades de colunas. Por exemplo, se você digitar "abc" em uma coluna de tipo de dados flutuante, receberá uma mensagem de erro e a alteração não será confirmada no banco de dados.  
  
O modo mais rápido de visualizar o tipo de dados de uma coluna quando se está no painel Resultados é abrir o painel Diagrama e passar o mouse por cima do nome da coluna da tabela ou objeto com valor de tabela.  
  
> [!NOTE]  
> O comprimento máximo que o painel Resultados pode mostrar de um tipo de dados de texto é 2.147.483.647.  
  
## <a name="keeping-the-results-set-synchronized-with-the-query-definition"></a>Como manter o conjunto de resultados sincronizado com a definição de consulta  
Enquanto se está trabalhando nos resultados de uma consulta ou exibição, é possível que os registros do painel de resultados percam a sincronização com a definição de consultas. Por exemplo, se você executar uma consulta para quatro entre cinco colunas de uma tabela, depois usar o painel Diagrama para adicionar a quinta coluna à definição da consulta, os dados da quinta coluna não serão adicionados automaticamente ao painel Resultados. Para fazer com que o painel de resultados reflita a nova definição de consulta, execute novamente a consulta.  
  
É possível confirmar se isso ocorre, se um ícone de alerta e o texto "Consulta alterada" aparecerem no canto inferior direito do painel de resultados, e o ícone for repetido no canto superior esquerdo do painel.  
  
## <a name="reconciling-changes-made-by-multiple-users"></a>Reconciliando alterações feitas por vários usuários  
Enquanto se está trabalhando nos resultados de uma consulta ou exibição, é possível que os registros sejam alterados por outro usuário que também esteja trabalhando com o banco de dados.  
  
Caso isso ocorra, você receberá um aviso assim que sair da célula com conflito. Você poderá, assim, substituir a alteração do outro usuário, atualizar o seu painel de resultados com a alteração do outro usuário, ou continuar editando o seu painel de resultados sem reconciliar as diferenças. Se optar por não reconciliar as diferenças, suas alterações não serão confirmadas no banco de dados.  
  
## <a name="limitations-in-the-results-pane"></a>Limitações do painel Resultados  
  
### <a name="what-can-not-be-updated"></a>O que não pode ser atualizado  
Estas dicas podem ajudá-lo a trabalhar bem, com os dados, no painel Resultados.  
  
-   As consultas que incluem colunas de mais de uma tabela ou exibição não podem ser atualizadas.  
  
-   As exibições só poderão ser atualizadas com permissão das restrições do banco de dados.  
  
-   Os resultados retornados por um procedimento armazenado não podem ser atualizados.  
  
-   Consultas ou exibições que usam cláusulas GROUP BY, DISTINCT ou TO XML não são atualizáveis.  
  
-   Em alguns casos, somente os resultados retornados por funções com valor de tabela podem ser atualizados.  
  
-   Dados em colunas que resultam de expressão da consulta.  
  
-   Dados que não foram traduzidos corretamente pelo provedor.  
  
### <a name="what-can-not-be-represented-fully"></a>O que não pode ser totalmente representado  
O que é retornado do banco de dados para o painel Resultados é em grande parte controlado pelo provedor da fonte de dados em uso. O painel Resultados não pode traduzir sempre os dados de todos os sistemas de gerenciamento de banco de dados. A seguir, alguns casos onde isso ocorre.  
  
-   Os tipos de dados binários, muitas vezes, não são úteis para pessoas que trabalham no painel Resultados, além de gastar muito tempo para serem baixados. Por isso, são representados por *<Binary data>* ou *Null*.  
  
-   A precisão e a escala nem sempre podem ser preservadas. Por exemplo, o painel Resultados dá suporte à precisão de 27. Se os dados forem de um tipo de maior precisão, eles poderão ficar truncados ou poderão ser representados por *<Unable to read data>*.  
  
## <a name="see-also"></a>Consulte Também  
[Executar operações básicas com consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
