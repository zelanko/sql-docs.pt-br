---
title: Caixa de diálogo Unir (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.ppg.joinline
- vdtsql.chm:69638
ms.assetid: 0d9516bb-4ad3-4fcf-bb77-93474dea698f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e266d398debd65a8a03f73d7f8726899c97b7e13
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62711127"
---
# <a name="join-dialog-box-visual-database-tools"></a>Caixa de diálogo Unir (Visual Database Tools)
  Use essa caixa de diálogo para especificar opções para unir tabelas. Para acessá-la, no painel **Design** , selecione uma linha de junção. Na janela **Propriedades**, clique em **Condição e Tipo de Junção** e clique nas reticências **(...)** exibidas à direita da propriedade.  
  
 Por padrão, tabelas relacionadas são unidas usando uma junção interna que cria um conjunto de resultados baseado em linhas que contêm informações correspondentes nas colunas de junção. Ao definir opções na caixa de diálogo **Junção** , você pode especificar uma junção baseada em um operador diferente e pode especificar uma junção externa.  
  
 Para obter mais informações sobre como unir tabelas, veja [Consultar com junções &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
## <a name="options"></a>Opções  
  
|**Termo**|**Definição**|  
|--------------|--------------------|  
|**Table**|Nomes das tabelas ou objetos com valor de tabela envolvidos na junção. Você não pode alterar os nomes das tabelas aqui – essas informações são exibidas apenas com fins informativos.|  
|**Coluna**|Nomes das colunas usadas para unir as tabelas. O operador na lista de operadores especifica a relação entre os dados nas colunas. Você não pode alterar os nomes das colunas aqui – essas informações são exibidas apenas com fins informativos.|  
|**Operador**|Especifique o operador usado para relacionar as colunas de junção. Para especificar um operador diferente de igual (=), selecione-o na lista. Quando você fechar a página de propriedades, o operador que você selecionou será exibido no gráfico de losangos da linha de junção, como a seguir:<br /><br /> ![Ícone de Ferramentas de Banco de Dados Visual](../../database-engine/media//dv3wbii.gif "Ícone de Ferramentas de Banco de Dados Visual")|  
|**Todas as linhas \<de Table1>**|Especifique que todas as linhas da tabela esquerda apareçam na saída, mesmo que não haja correspondências na tabela direita. Colunas sem dados correspondentes na tabela direita são exibidas como nulas. Escolher essa opção equivale a especificar LEFT OUTER JOIN na instrução SQL.|  
|**Todas as linhas \<de Table2>**|Especifique que todas as linhas da tabela direita sejam exibidas na saída, mesmo que não haja correspondências na tabela esquerda. Colunas sem dados correspondentes na tabela esquerda são exibidas como nulas. Escolher essa opção equivale a especificar RIGHT OUTER JOIN na instrução SQL.|  
  
 Selecionar todas as **linhas de \<Table1>** e **todas as linhas \<de TABLE2>** é equivalente a especificar a junção externa completa na instrução SQL.  
  
 Quando você seleciona uma opção para criar uma junção externa, o gráfico de losangos na linha de junção é alterado para indicar que a junção é externa esquerda, externa direita ou externa completa.  
  
> [!NOTE]  
>  As palavras "esquerda" e "direita" não necessariamente correspondem à posição de tabelas no painel Diagrama. "Esquerda" refere-se à tabela cujo nome é exibido à esquerda da palavra-chave JOIN na instrução SQL e "direita" refere-se à tabela cujo nome é exibido à direita da palavra-chave JOIN. Se você mover as tabelas no painel **Diagrama** , a tabela considerada esquerda ou direita não será alterada.  
  
## <a name="see-also"></a>Consulte Também  
 [Consultar com junções &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
