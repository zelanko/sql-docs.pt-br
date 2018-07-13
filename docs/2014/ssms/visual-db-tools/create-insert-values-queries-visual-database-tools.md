---
title: Criar consultas Insert Values (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
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
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9501d3d35f35195112c328af22daf4948d115966
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157607"
---
# <a name="create-insert-values-queries-visual-database-tools"></a>Criar consultas Insert Values (Visual Database Tools)
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
>  Você não pode desfazer a ação de execução de uma consulta Insert Values. Como precaução, faça backup de seus dados antes de executar a consulta.  
  
### <a name="to-create-an-insert-values-query"></a>Para criar uma consulta Insert Values  
  
1.  Adicione a tabela que deseja atualizar ao painel Diagrama.  
  
2.  No menu **Designer de Consultas** , aponte para **Alterar Tipo**e clique em **Insert Values**.  
  
    > [!NOTE]  
    >  Se mais de uma tabela for exibida no painel Diagrama quando você iniciar a consulta Insert Values, o Designer de Consulta e Exibição exibirá a caixa de diálogo [Escolher Tabela de Destino para Inserir Valores](visual-database-tools.md) que solicitará o nome da tabela a ser atualizada.  
  
3.  No painel Diagrama, clique na caixa de seleção de cada coluna para a qual você deseja fornecer novos valores. Essas colunas serão exibidas no painel Critérios. As colunas só serão atualizadas se você as adicionar à consulta.  
  
4.  Na coluna **Novo Valor** do painel Critérios, insira o novo valor para a coluna. Você pode inserir valores literais, nomes de coluna ou expressões. O valor deve corresponder (ou ser compatível com) ao tipo de dados da coluna que você está atualizando.  
  
    > [!CAUTION]  
    >  O Designer de Consulta e Exibição não pode verificar se um valor é adequado ao comprimento da coluna que você está inserindo. Se você fornecer um valor muito longo, ele poderá ser truncado sem aviso. Por exemplo, se uma coluna `name` tiver 20 caracteres, mas você especificar um valor de inserção de 25 caracteres, os últimos 5 caracteres poderão ser truncados.  
  
 Se você executar uma consulta Insert Values, nenhum resultado será relatado no painel de [Resultados](results-pane-visual-database-tools.md). Em vez disso, será exibida uma mensagem indicando quantas linhas foram alteradas.  
  
## <a name="see-also"></a>Consulte também  
 [Suporte para tipos de consulta &#40;Visual Database Tools&#41;](supported-query-types-visual-database-tools.md)   
 [Tópicos explicativos de consultas e exibições de design &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Executar operações básicas com consultas &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
