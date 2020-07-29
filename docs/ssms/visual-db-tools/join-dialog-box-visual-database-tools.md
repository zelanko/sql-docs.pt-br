---
title: Caixa de diálogo Junção
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.ppg.joinline
- vdtsql.chm:69638
ms.assetid: 0d9516bb-4ad3-4fcf-bb77-93474dea698f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: d049e23db7020ca84c4cec1e4ddc1ba5bbe84b4d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011711"
---
# <a name="join-dialog-box-visual-database-tools"></a>Caixa de diálogo Unir (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Use essa caixa de diálogo para especificar opções para unir tabelas. Para acessá-la, no painel **Design** , selecione uma linha de junção. Na janela **Propriedades**, clique em **Condição e Tipo de Junção** e clique nas reticências **(...)** exibidas à direita da propriedade.  
  
Por padrão, tabelas relacionadas são unidas usando uma junção interna que cria um conjunto de resultados baseado em linhas que contêm informações correspondentes nas colunas de junção. Ao definir opções na caixa de diálogo **Junção** , você pode especificar uma junção baseada em um operador diferente e pode especificar uma junção externa.  
  
Para obter mais informações sobre como unir tabelas, veja [Consultar com junções &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md).  
  
## <a name="options"></a>Opções  
  
|**Termo**|**Definição**|  
|------------|------------------|  
|**Table**|Nomes das tabelas ou objetos com valor de tabela envolvidos na junção. Você não pode alterar os nomes das tabelas aqui – essas informações são exibidas apenas com fins informativos.|  
|**Coluna**|Nomes das colunas usadas para unir as tabelas. O operador na lista de operadores especifica a relação entre os dados nas colunas. Você não pode alterar os nomes das colunas aqui – essas informações são exibidas apenas com fins informativos.|  
|**Operador**|Especifique o operador usado para relacionar as colunas de junção. Para especificar um operador diferente de igual (=), selecione-o na lista. Quando você fechar a página de propriedades, o operador que você selecionou será exibido no gráfico de losangos da linha de junção, como a seguir:<br /><br />![Ícone de Ferramentas de Banco de Dados Visual](../../ssms/visual-db-tools/media/dv3wbii.gif "Ícone de Ferramentas de Banco de Dados Visual")|  
|**Todas as linhas de <table1>**|Especifique que todas as linhas da tabela esquerda apareçam na saída, mesmo que não haja correspondências na tabela direita. Colunas sem dados correspondentes na tabela direita são exibidas como nulas. Escolher essa opção equivale a especificar LEFT OUTER JOIN na instrução SQL.|  
|**Todas as linhas de <table2>**|Especifique que todas as linhas da tabela direita sejam exibidas na saída, mesmo que não haja correspondências na tabela esquerda. Colunas sem dados correspondentes na tabela esquerda são exibidas como nulas. Escolher essa opção equivale a especificar RIGHT OUTER JOIN na instrução SQL.|  
  
Selecionar tanto Todas **as linhas de <table1>** como **Todas as linhas de <table2>** equivale a especificar FULL OUTER JOIN na instrução SQL.  
  
Quando você seleciona uma opção para criar uma junção externa, o gráfico de losangos na linha de junção é alterado para indicar que a junção é externa esquerda, externa direita ou externa completa.  
  
> [!NOTE]  
> As palavras "esquerda" e "direita" não necessariamente correspondem à posição de tabelas no painel Diagrama. "Esquerda" refere-se à tabela cujo nome é exibido à esquerda da palavra-chave JOIN na instrução SQL e "direita" refere-se à tabela cujo nome é exibido à direita da palavra-chave JOIN. Se você mover as tabelas no painel **Diagrama** , a tabela considerada esquerda ou direita não será alterada.  
  
## <a name="see-also"></a>Consulte Também  
[Consultar com junções &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
