---
title: Cálculos | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c71a931814e28a28ccfffd810deff15d7f126f6f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="calculations"></a>Cálculos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Um cálculo é uma expressão MDX (Multidimensional Expressions) ou um script que é usado para definir um membro calculado, um conjunto nomeado ou uma tarefa no escopo em um cubo no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Os cálculos permitem a adição de objetos que são definidos não pelos dados do cubo, mas pelas expressões que fazem referência a outras partes do cubo, a outros cubos, ou mesmo a informações fora do banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Os cálculos permitem a extensão das capacidades de um cubo, adicionando flexibilidade e poder a aplicativos de inteligência comercial. Para obter mais informações sobre cálculos de script, consulte [Introduction to MDX Scripting in Microsoft SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81892). Para obter mais informações sobre problemas de desempenho relacionadas a cálculos e consultas MDX, consulte o [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621).  
  
## <a name="calculated-members"></a>Membros calculados  
 Um membro calculado é um membro cujo valor é calculado no tempo de execução usando uma linguagem MDX que você especificou ao definir o membro calculado. Um membro calculado está disponível para aplicativos de inteligência comercial assim como qualquer outro membro. Membros calculados não aumentam o tamanho do cubo porque somente as definições são armazenadas no cubo; os valores são calculados na memória conforme necessário para responder a uma consulta.  
  
 Os membros calculados podem ser definidos para qualquer dimensão, inclusive a dimensão de medidas. Os membros calculados criados na dimensão de medidas são chamados medidas calculadas.  
  
 Embora membros calculados estejam geralmente baseados em dados já existentes no cubo, você pode criar expressões complexas combinando dados com operadores, números e funções aritméticas. Você também pode usar funções MDX, como LookupCube, para acessar dados em outros cubos no banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] inclui as bibliotecas de funções padronizadas do Visual Studio, e usar procedimentos armazenados para recuperar dados de fontes diferentes do banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] atual. Para obter mais informações sobre procedimentos armazenados, consulte [definindo procedimentos armazenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md).  
  
 Por exemplo, suponha que os executivos em uma empresa transportadora queiram determinar quais tipos de carga são mais lucrativos, com base no lucro por unidade de volume. Eles usam um cubo Shipments que contém as dimensões Cargo, Fleet e Time e as medidas Price_to_Ship, Cost_to_Ship e Volume_in_Cubic_Meters; contudo, o cubo não contém uma medida para rentabilidade. Você pode criar um membro calculado como uma medida chamada Profit_per_Cubic_Meter no cubo combinando as medidas existentes na seguinte expressão:  
  
```  
([Measures].[Price_to_Ship] - [Measures].[Cost_to_Ship]) /  
[Measures].[Volume_in_Cubic_Meters]  
```  
  
 Depois de criar o membro calculado, o Profit_per_Cubic_Meter aparecerá juntamente com as outras medidas na próxima vez que o cubo Shipments for acessado.  
  
 Para criar membros calculados, use o **cálculo**guia no Designer de cubo. Para obter mais informações, consulte [criar membros calculados](../../analysis-services/multidimensional-models/create-calculated-members.md)  
  
## <a name="named-sets"></a>Conjuntos nomeados  
 Um conjunto nomeado é uma expressão de instrução CREAT SET MDX que retorna um conjunto. A expressão MDX é salva como parte da definição de um cubo em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Um conjunto nomeado é criado para reutilização nas consultas MDX. Um conjunto nomeado permite que os usuários empresariais simplifiquem consultas e utilizem um nome de conjunto em vez de uma expressão de conjunto para expressões de conjunto complexas usadas com mais frequência. **Tópico relacionado:** [criar conjuntos nomeados](../../analysis-services/multidimensional-models/create-named-sets.md)  
  
## <a name="script-commands"></a>Comandos de script  
 Um comando de script é um script MDX, incluído como parte da definição do cubo. Os comandos de script permitem a execução de praticamente qualquer ação com suporte suporte pelo MDX em um cubo, como incluir no escopo um cálculo a ser aplicado a apenas parte do cubo. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], scripts MDX podem aplicar ao cubo inteiro ou às seções específicas do cubo, em pontos específicos durante a execução do script. O comando de script padrão, que é a instrução CALCULATE, popula as células no cubo com dados agregados com base no escopo padrão.  
  
 O escopo padrão é o cubo inteiro, mas você pode definir um escopo mais limitado, conhecido como subcubo, e então aplicar um script MDX a apenas aquele espaço específico do cubo. A instrução SCOPE define o escopo de todas as expressões MDX subsequentes e instruções no script de cálculo até que o escopo seja finalizado ou redefinido. A instrução THIS é então usada para aplicar uma expressão MDX ao escopo atual. Você pode usar a instrução BACK_COLOR para especificar uma cor de fundo para as células no escopo atual, para ajudá-lo durante a depuração.  
  
 Por exemplo, você pode usar um comando de script para alocar cotas de vendas a funcionários ao longo do tempo e a território de vendas com base nos valores ponderados de um período de tempo anterior.  
  
## <a name="see-also"></a>Consulte também  
 [Cálculos em modelos multidimensionais](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
