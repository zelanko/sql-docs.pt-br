---
title: Unir tabelas em várias colunas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiple column joins
- joins [SQL Server], multiple columns
ms.assetid: 56a158bc-a42a-4b78-baad-4721d2d22cd3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 88208446cbdde6643d65ec804ccddbd125dc1e5b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65096876"
---
# <a name="join-tables-on-multiple-columns-visual-database-tools"></a>Unir tabelas em várias colunas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Você pode unir tabelas em várias colunas. Quer dizer, você poderá criar uma consulta que corresponde às linhas de duas tabelas apenas se elas satisfizerem várias condições. Se o banco de dados contiver uma relação, que corresponda a várias colunas de chave estrangeira, em uma tabela para uma chave primária de multicolunas na outra tabela, você poderá usar esta relação para criar uma junção de multicolunas. Para obter detalhes, consulte [Unir tabelas automaticamente &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md).  
  
Mesmo que o banco de dados não contenha nenhuma relação de chave estrangeira de multicolunas, você poderá criar a junção manualmente.  
  
### <a name="to-manually-create-a-multicolumn-join"></a>Para criar uma junção de multicolunas manualmente  
  
1.  Adicione ao [Painel de Diagrama](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) as tabelas que deseja unir.  
  
2.  Arraste o nome da primeira coluna de junção, na janela da primeira tabela, e solte sobre a coluna relacionada, na janela da segunda tabela. Você não pode basear uma junção em texto, ntext ou colunas de imagem.  
  
    > [!NOTE]  
    > Em geral, as colunas de junção devem ser com os mesmos tipos de dados (ou compatíveis). Por exemplo, se a coluna de junção na primeira tabela for uma data, você deve relacionar isto a uma coluna de data na segunda tabela. Por outro lado, se a primeira coluna de junção for um inteiro, a coluna de junção relacionada também deverá ser do tipo de dados inteiro, mas poderá ser de um tamanho diferente. Entretanto, podem haver casos onde as conversões de tipos de dados implícitos poderão unir colunas aparentemente incompatíveis, que funcionarão.  
    >   
    > O [Designer de Consulta e Exibição](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) não verificará os tipos de dados das colunas que você usa para criar uma junção, mas, quando você executar a consulta, o banco de dados exibirá um erro se os tipos de dados não forem compatíveis.  
  
3.  Arraste o nome da segunda coluna de junção na janela da primeira tabela e solte sobre a coluna relacionada na janela da segunda tabela.  
  
4.  Repita a etapa 3 para cada par adicional de colunas de junção, nas duas tabelas.  
  
5.  Executa a consulta.  
  
## <a name="see-also"></a>Consulte Também  
[Consultar com junções &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
