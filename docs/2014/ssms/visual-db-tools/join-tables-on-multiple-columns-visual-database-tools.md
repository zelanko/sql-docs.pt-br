---
title: Unir tabelas em várias colunas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiple column joins
- joins [SQL Server], multiple columns
ms.assetid: 56a158bc-a42a-4b78-baad-4721d2d22cd3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e26030a201087f8e99126760296659a3e7f04fe8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63306074"
---
# <a name="join-tables-on-multiple-columns-visual-database-tools"></a>Unir tabelas em várias colunas (Visual Database Tools)
  Você pode unir tabelas em várias colunas. Quer dizer, você poderá criar uma consulta que corresponde às linhas de duas tabelas apenas se elas satisfizerem várias condições. Se o banco de dados contiver uma relação, que corresponda a várias colunas de chave estrangeira, em uma tabela para uma chave primária de multicolunas na outra tabela, você poderá usar esta relação para criar uma junção de multicolunas. Para obter detalhes, consulte [Unir tabelas automaticamente &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
 Mesmo que o banco de dados não contenha nenhuma relação de chave estrangeira de multicolunas, você poderá criar a junção manualmente.  
  
### <a name="to-manually-create-a-multicolumn-join"></a>Para criar uma junção de multicolunas manualmente  
  
1.  Adicione ao [Painel de Diagrama](diagram-pane-visual-database-tools.md) as tabelas que deseja unir.  
  
2.  Arraste o nome da primeira coluna de junção, na janela da primeira tabela, e solte sobre a coluna relacionada, na janela da segunda tabela. Você não pode basear uma junção em texto, ntext ou colunas de imagem.  
  
    > [!NOTE]  
    >  Em geral, as colunas de junção devem ser com os mesmos tipos de dados (ou compatíveis). Por exemplo, se a coluna de junção na primeira tabela for uma data, você deve relacionar isto a uma coluna de data na segunda tabela. Por outro lado, se a primeira coluna de junção for um inteiro, a coluna de junção relacionada também deverá ser do tipo de dados inteiro, mas poderá ser de um tamanho diferente. Entretanto, podem haver casos onde as conversões de tipos de dados implícitos poderão unir colunas aparentemente incompatíveis, que funcionarão.  
    >   
    >  O [Designer de Consulta e Exibição](query-and-view-designer-tools-visual-database-tools.md) não verificará os tipos de dados das colunas que você usa para criar uma junção, mas, quando você executar a consulta, o banco de dados exibirá um erro se os tipos de dados não forem compatíveis.  
  
3.  Arraste o nome da segunda coluna de junção na janela da primeira tabela e solte sobre a coluna relacionada na janela da segunda tabela.  
  
4.  Repita a etapa 3 para cada par adicional de colunas de junção, nas duas tabelas.  
  
5.  Executa a consulta.  
  
## <a name="see-also"></a>Consulte também  
 [Consultar com junções &#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)  
  
  
