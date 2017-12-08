---
title: Calculado colunas (SSAS Tabular) | Microsoft Docs
ms.custom: 
ms.date: 10/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e1011278-556d-4984-b01d-a37f8a33b304
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: c7fe8e5ad97a1955160bf2f8f953c85971f66b09
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="calculated-columns"></a>Colunas calculadas
  Colunas calculadas, em modelos tabulares, permitem que você adicionar novos dados a seu modelo. Em vez de colar ou importar valores para a coluna, você cria uma fórmula DAX que define os valores do nível de linha da coluna. A coluna calculada pode então ser usada em um relatório, Tabela Dinâmica ou Gráfico Dinâmico como você faria com qualquer outra coluna.  
 
  
  
##  <a name="bkmk_understanding"></a> Benefícios  
 As fórmulas nas colunas calculadas são bem semelhantes às fórmulas do Excel. No entanto, diferentemente do Excel, não é possível criar fórmulas diferentes para linhas distintas em uma tabela; em vez disso, a fórmula DAX é aplicada automaticamente a toda a coluna.  
  
 Quando uma coluna contém uma fórmula, o valor é computado para cada linha. Os resultados são calculados para a coluna quando você insere uma fórmula válida. Em seguida, os valores de coluna são recalculados conforme necessário, como quando os dados subjacentes são atualizados.  
  
 É possível criar medidas ou colunas calculadas baseadas em medidas e em outras colunas calculadas. Por exemplo, talvez você crie uma coluna calculada para extrair um número de uma cadeia de caracteres de texto e, em seguida, usar esse número em outra coluna calculada.  
  
 Uma coluna calculada se baseia nos dados que você já tem em uma tabela existente, ou criou usando uma fórmula DAX. Por exemplo, você pode querer concatenar valores, realizar adição, extrair subcadeias de caracteres ou comparar os valores em outros campos. Para adicionar uma coluna calculada, você deve ter pelo menos uma tabela em seu modelo.  
  
 Este exemplo demonstra uma fórmula simples em uma coluna calculada:  
  
```  
=EOMONTH([StartDate],0])  
  
```  
  
 Esta fórmula extrai o mês da coluna StartDate. Em seguida, ela calcula o final do valor de mês para cada linha da tabela. O segundo parâmetro especifica o número de meses antes ou depois do mês em StartDate; neste caso, 0 significa o mesmo mês. Por exemplo, se o valor na coluna StartDate for 01/06/2001, o valor na coluna calculada será 30/06/2001.  
  
##  <a name="bkmk_naming"></a> Naming a calculated column  
 Por padrão, novas colunas calculadas são adicionadas à direita de outras colunas em uma tabela, e a coluna recebe automaticamente o nome padrão **CalculatedColumn1**, **CalculatedColumn2**e assim por diante. Você também pode clicar com o botão direito em uma coluna e clicar em Inserir Coluna para criar uma nova coluna entre duas colunas existentes. Você pode reorganizar as colunas dentro da mesma tabela clicando e arrastando, e pode renomear as colunas depois que elas forem criadas; porém, você deve estar atento às seguintes restrições sobre alterações para colunas calculadas:  
  
-   Cada nome de coluna deve ser exclusivo dentro de uma tabela.  
  
-   Evite nomes que já foram usados para medidas dentro do mesmo modelo. Embora seja possível que uma medida e uma coluna calculada tenham o mesmo nome, se os nomes não forem exclusivos você poderá obter erros de cálculo. Para evitar invocar uma medida acidentalmente, ao fazer referência a uma coluna use sempre uma referência de coluna totalmente qualificada.  
  
-   Quando você renomeia uma coluna calculada, todas as fórmulas que se baseiam na coluna devem ser atualizadas manualmente. A menos que você esteja no modo de atualização manual, a atualização dos resultados das fórmulas acontece automaticamente. No entanto, essa operação pode demorar um pouco.  
  
-   Há alguns caracteres que não podem ser usados nos nomes de colunas. Para obter mais informações, consulte "Requisitos de nomenclatura" na [Referência da Sintaxe DAX](http://msdn.microsoft.com/en-us/098630f4-7d1d-467e-976c-99b2279430d5).  
  
##  <a name="bkmk_perf"></a> Performance of calculated columns  
 A fórmula de uma coluna calculada pode consumir mais recursos do que a fórmula usada para uma medida. Um motivo é que o resultado para uma coluna calculada sempre é calculado para cada linha de uma tabela, enquanto uma medida é calculada apenas para as células definidas pelo filtro usado em um relatório, Tabela Dinâmica ou Gráfico Dinâmico. Por exemplo, uma tabela com um milhão de linhas sempre terá uma coluna calculada com um milhão de resultados, e um efeito correspondente em desempenho. No entanto, uma Tabela Dinâmica normalmente filtra os dados, aplicando títulos de linha e coluna; por isso, uma medida só é calculada para o subconjunto de dados em cada célula da Tabela Dinâmica.  
  
 Uma fórmula tem dependências nos objetos referenciados na fórmula, como outras colunas ou expressões que avaliam valores. Por exemplo, uma coluna calculada baseada em outra coluna, ou um cálculo que contenha uma expressão com uma referência de coluna, não pode ser avaliada até que a outra coluna seja avaliada. Por padrão, a atualização automática permanece habilitada em pastas de trabalho; por isso, todas essas dependências podem afetar o desempenho enquanto os valores são atualizados e as fórmulas, atualizadas.  
  
 Para evitar problemas de desempenho ao criar colunas calculadas, siga estas diretrizes:  
  
-   Em vez de criar uma única fórmula que contém muitas dependências complexas, crie as fórmulas em etapas, salvando os resultados em colunas, de forma que possa validar os resultados e avaliar o desempenho.  
  
-   A modificação de dados muitas vezes exigirá que colunas calculadas sejam recalculadas. É possível impedir isso, definindo-se o modo de recálculo como manual; no entanto, se algum valor na coluna calculada estiver incorreto, a coluna permanecerá esmaecida até você atualizar e recalcular os dados.  
  
-   Se você alterar ou excluir relações entre tabelas, as fórmulas que usam colunas nessas tabelas se tornarão inválidas.  
  
-   Se você criar uma fórmula contendo uma dependência circular ou autorreferenciada, ocorrerá um erro.  
  
##  <a name="bkmk_rel_tasks"></a> Related tasks  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Criar uma coluna calculada](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md)|As tarefas neste tópico descrevem como adicionar uma nova coluna calculada a uma tabela.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e colunas](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [Medidas](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [Cálculos](../../analysis-services/tabular-models/calculations-ssas-tabular.md)  
  
  
