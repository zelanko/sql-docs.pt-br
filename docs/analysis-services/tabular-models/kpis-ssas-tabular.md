---
title: KPIs | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b5ca210a69127a6fc1a0e66c23b7f35e9fa35791
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="kpis"></a>KPIs
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Um *KPI* (indicador chave de desempenho), em um modelo de tabela, é usado para medir o desempenho de um valor, definido por uma medida *Base* , em relação a um valor de *Destino* , também definido por uma medida ou por um valor absoluto. Este artigo fornece a autores de modelo de tabela uma compreensão básica de KPIs em um modelo de tabela.  
  
##  <a name="bkmk_benefits"></a> Benefícios  
 Na terminologia empresarial, um KPI (indicador chave de desempenho) é uma medida quantificável para medir os objetivos empresariais. Um KPI é avaliado, frequentemente, ao longo do tempo. Por exemplo, o departamento de vendas de uma organização pode usar um KPI para medir lucro bruto mensal em relação ao lucro bruto projetado. O departamento de contabilidade pode medir as despesas mensais em relação à receita para avaliar custos, e um departamento de recursos humanos pode medir a rotatividade de funcionários trimestral. Cada um é um exemplo de KPI. Os executivos frequentemente usam KPIs agrupados em um scorecard empresarial para obter um resumo histórico rápido e preciso do sucesso da empresa ou para identificar tendências.  
  
 Um KPI em um modelo de tabela inclui:  
  
 **Valor base**  
 Um valor base é definido por uma medida que resolve em um valor. Por exemplo, este valor pode ser uma agregação das Vendas reais ou uma medida calculada como Lucro para um determinado período.  
  
 **Valor de destino**  
 Um valor de destino é definido por uma medida que resolve em um valor ou por um valor absoluto. Por exemplo, um valor de destino pode ser o valor pelo qual os gerentes de negócios de uma organização desejam aumentar vendas ou ganhos.  
  
 **Limites de status**  
 Um limite de Status é definido pelo intervalo entre um limite baixo e alto ou por um valor fixo. O limite de status é exibido com um gráfico para ajudar usuários a determinarem facilmente o status do Valor base comparado com o Valor de destino.  
  
##  <a name="bkmk_example"></a> Exemplo  
 A gerente de vendas da Adventure Works quer criar uma Tabela Dinâmica que possa ser usada para exibir rapidamente se os funcionários de vendas estão atingindo suas cotas de vendas para um determinado período (ano). Para cada funcionário de vendas, ela deseja que a Tabela Dinâmica exiba o valor de vendas real em dólares, o valor da cota de vendas em dólares e uma exibição gráfica simples mostrando o status de cada funcionário de vendas, se está abaixo, acima ou na cota. Ela deseja poder segmentar os dados por ano.  
  
 Para fazer isto, o gerente de vendas pede a ajuda do desenvolvedor de solução de BI da organização para adicionar um KPI de Vendas ao Modelo Tabular do AdventureWorks. O gerente de vendas, em seguida, usará o Excel para se conectar ao modelo Tabular do Adventure Works como uma fonte de dados e criar uma tabela dinâmica com os campos (medidas e KPI) e segmentações de dados para analisar se a equipe de vendas está atingindo as cotas.  
  
 No modelo, é criada uma medida na coluna SalesAmount na tabela FactResellerSales, que dá o valor de vendas real em dólares para cada funcionário de vendas. Esta medida definirá o Valor base do KPI.  
  
 A medida Sales é criada com a seguinte fórmula:  
  
```  
Sales:=Sum(FactResellerSales[SalesAmount])  
```  
  
 A coluna SalesAmountQuota na tabela FactSalesQuota tem uma cota do valor de vendas definida para cada funcionário. Os valores nesta coluna servirão como a medida de destino (valor) no KPI.  
  
 A medida SalesAmountQuota é criada com a seguinte fórmula:  
  
```  
Target SalesAmountQuota:=Sum(FactSalesQuota[SalesAmountQuota])  
```  
  
> [!NOTE]  
>  Há uma relação entre a coluna de EmployeeKey na tabela FactSalesQuota e a EmployeeKey na tabela DimEmployees. Esta relação é necessária para que cada funcionário de vendas na tabela DimEmployee seja representado na tabela FactSalesQuota.  
  
 Agora que as medidas foram criadas para servir como o Valor base e o Valor de destino do KPI, a medida Sales é estendida para um novo KPI de vendas. No KPI de vendas, a medida de destino SalesAmountQuota é definida como o Valor de destino. O Limite de status é definido como um intervalo por percentual, o destino do qual é 100%, que significa as vendas reais definidas pela medida Sales que atingiu a quantidade de cota definida na medida de destino SalesAmountQuota. Os percentuais Baixo e Alto são definidos na barra de status e um tipo de gráfico é selecionado.  
  
 A gerente de vendas agora pode criar uma Tabela Dinâmica adicionando o Valor base do KPI, o Valor de destino e o Status ao campo Valores. A coluna Employees é adicionada ao campo RowLabel e a coluna CalendarYear é adicionada como uma segmentação de dados.  
  
 A gerente de vendas agora pode fatiar por ano o valor de vendas real, o valor da cota de vendas e o status para cada funcionário de vendas. Ela pode analisar tendências de vendas ao longo de anos para determinar se precisa ajustar a cota para um funcionário de vendas.  
  
##  <a name="bkmk_create"></a> Create and edit KPIs  
 Para criar KPIs, no designer de modelo, você usará a caixa de diálogo Indicador chave de desempenho. Como KPIs devem ser associados a uma medida, você cria um KPI estendendo uma medida que é avaliada como um valor Base e, em seguida, criando uma medida que é avaliada como um valor de Destino ou inserindo um valor absoluto. Depois que a medida Base (valor) e o valor de Destino forem definidos, você pode definir os parâmetros de limite de status entre os valores Base e Destino. O status é exibido em um formato gráfico usando ícones selecionáveis, barras, gráficos ou cores. Os valores Base e de Destino, assim como o Status, podem ser adicionados a um relatório ou Tabela Dinâmica como valores que podem ser fatiados em relação a outros campos de dados.  
  
 Para exibir a caixa de diálogo Indicador chave de desempenho, na grade de medida para uma tabela, clique com o botão direito em uma medida que servirá como valor Base e clique em **Criar KPI**. Depois que uma medida foi estendida para um KPI como um valor Base, um ícone será exibido ao lado do nome da medida na grade de medida identificando a medida como associada a um KPI.  
  
##  <a name="bkmk_related_tasks"></a> Tarefas relacionadas  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Criar e gerenciar KPIs](../../analysis-services/tabular-models/create-and-manage-kpis-ssas-tabular.md)|Descreve como criar um KPI com uma medida Base, uma medida de Destino e limites de status.|  
  
## <a name="see-also"></a>Consulte também  
 [Medidas](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [Perspectivas](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)  
  
  
