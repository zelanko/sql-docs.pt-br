---
title: Criar consultas de inserir valores
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting values
- queries [SQL Server], types
- adding values
- row additions [SQL Server], Insert Values query
- inserting rows
- Insert Values query
- adding rows
- table values [SQL Server]
ms.assetid: 2d4b2f6d-cc09-434b-8a0e-ccce40628064
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 77ec3649542b0c449735df6a5a065638eeffbd45
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75254342"
---
# <a name="create-insert-values-queries-visual-database-tools"></a>Criar consultas Insert Values (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Você pode criar uma nova linha na tabela atual usando uma consulta Insert Values. Ao criar uma consulta Insert Values, você especifica:  
  
-   A tabela de banco de dados à qual a linha será adicionada.  
  
-   As colunas cujo conteúdo você deseja adicionar.  
  
-   O valor ou a expressão a ser inserida nas colunas individuais.  
  
Por exemplo, a seguinte consulta adiciona uma linha à tabela `titles` especificando valores para o título, tipo, editora e preço:  
  
```  
INSERT INTO titles  
         (title_id, title, type, pub_id, price)  
VALUES   ('BU9876', 'Creating Web Pages', 'business', '1389', '29.99')  
```  
  
Quando você cria uma consulta Insert Values, o painel Critérios muda para refletir somente as opções disponíveis para inserir uma nova linha: o nome da coluna e o valor a ser inserido.  
  
> [!CAUTION]  
> Você não pode desfazer a ação de execução de uma consulta Insert Values. Como precaução, faça backup de seus dados antes de executar a consulta.  
  
### <a name="to-create-an-insert-values-query"></a>Para criar uma consulta Insert Values  
  
1.  Adicione a tabela que deseja atualizar ao painel Diagrama.  
  
2.  No menu **Designer de Consultas** , aponte para **Alterar Tipo**e clique em **Insert Values**.  
  
    > [!NOTE]  
    > Se mais de uma tabela for exibida no painel Diagrama quando você iniciar a consulta Insert Values, o Designer de Consulta e Exibição exibirá a caixa de diálogo [Escolher Tabela de Destino para Inserir Valores](../../ssms/visual-db-tools/choose-target-table-for-insert-values-dialog-box-visual-database-tools.md) que solicitará o nome da tabela a ser atualizada.  
  
3.  No painel Diagrama, clique na caixa de seleção de cada coluna para a qual você deseja fornecer novos valores. Essas colunas serão exibidas no painel Critérios. As colunas só serão atualizadas se você as adicionar à consulta.  
  
4.  Na coluna **Novo Valor** do painel Critérios, insira o novo valor para a coluna. Você pode inserir valores literais, nomes de coluna ou expressões. O valor deve corresponder (ou ser compatível com) ao tipo de dados da coluna que você está atualizando.  
  
    > [!CAUTION]  
    > O Designer de Consulta e Exibição não pode verificar se um valor é adequado ao comprimento da coluna que você está inserindo. Se você fornecer um valor muito longo, ele poderá ser truncado sem aviso. Por exemplo, se uma coluna `name` tiver 20 caracteres, mas você especificar um valor de inserção de 25 caracteres, os últimos 5 caracteres poderão ser truncados.  
  
Se você executar uma consulta Insert Values, nenhum resultado será relatado no painel de [Resultados](../../ssms/visual-db-tools/results-pane-visual-database-tools.md). Em vez disso, será exibida uma mensagem indicando quantas linhas foram alteradas.  
  
## <a name="see-also"></a>Consulte Também  
[Tipos de consulta com suporte &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Executar operações básicas com consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
