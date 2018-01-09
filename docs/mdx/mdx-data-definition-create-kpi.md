---
title: "Instrução CREATE KPI (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE KPI
- KPI
- CREATE_KPI
- CREATE
helpviewer_keywords:
- CREATE KPI statement
- key performance indicators [MDX]
ms.assetid: 87618fef-95e5-4dd0-a650-aeb60ccbddcb
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6a97fbc894a0b88511ab551aa231fcfb3746d52c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-data-definition---create-kpi"></a>Definição de dados MDX - criar KPI
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Cria um KPI (indicador chave de desempenho). Um KPI é uma coleção de cálculos associada a um grupo de medidas em um cubo e é usado para avaliar sucesso nos negócios ou sucesso de cenário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE KPI CURRENTCUBE | <Cube Name>.KPI_Name AS KPI_Value  
   [,Property_Name = Property_Value, ...n]  
```  
  
## <a name="arguments"></a>Argumentos  
 *KPI_Name*  
 Uma cadeia de caracteres válida que fornece um nome KPI.  
  
 *KPI_Value*  
 Uma linguagem MDX válida que retorna um valor numérico.  
  
 *Property_Name*  
 Uma cadeia de caracteres válida que fornece o nome de uma propriedade KPI.  
  
 *Property_Value*  
 Uma expressão escalar válida que define o valor de propriedade KPI.  
  
## <a name="remarks"></a>Remarks  
 A especificação de um cubo diferente daquele conectado no momento causa um erro. Portanto, deve-se usar CURRENTCUBE no lugar de um nome de cubo para indicar o cubo atual.  
  
## <a name="kpi-properties"></a>Propriedades KPI  
 A tabela a seguir relaciona todas as propriedades KPI. Nenhuma dessas propriedades tem um valor padrão. Portanto, até que um valor específico seja atribuído a uma propriedade KPI, consultas relativas àquelas propriedades retornarão um valor nulo.  
  
|Identificador de propriedade|Significado|  
|-------------------------|-------------|  
|GOAL|Uma expressão MDX válida que retorna um valor numérico.|  
|STATUS|Uma expressão MDX válida que retorna um valor numérico.|  
|STATUS_GRAPHIC|Uma cadeia de caracteres que define um conjunto de imagens gráficas que será usado pelo aplicativo cliente.|  
|TREND|Uma expressão MDX válida que retorna um valor numérico.|  
|TREND_GRAPHIC|Uma cadeia de caracteres que define um conjunto de imagens gráficas que será usado pelo aplicativo cliente.|  
|WEIGHT|Uma expressão MDX válida que retorna um valor numérico.|  
|CURRENT_TIME_MEMBER|Uma linguagem MDX válida que retorna um membro na dimensão temporal. CURRENT_TIME_MEMBER define o ponto de referência para todas as funções de hora relativas|  
|PARENT_KPI|Uma cadeia de caracteres válida que especifica o nome do KPI pai.|  
|CAPTION|Uma cadeia de caracteres que o aplicativo cliente usa como legenda para o KPI.|  
|DISPLAY_FOLDER|Uma cadeia de caracteres que especifica o caminho da pasta de exibição onde o KPI será mostrado pelo aplicativo cliente. O separador de nível de pasta é definido pelo aplicativo cliente. Para ferramentas e clientes fornecidos pelo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], a barra invertida (\\) é o separador de nível. Para várias pastas de exibição de um membro definido, use ponto-e-vírgula (;) para separar as pastas.|  
|ASSOCIATED_MEASURE_GROUP|Uma cadeia de caracteres que especifica o nome do grupo de medidas ao qual todos os cálculos de MDX deveriam recorrer.|  
  
 Os valores para as propriedades GOAL, STATUS e TREND são expressões MDX que deveriam ser avaliadas entre -1 a 1. No entanto, é o aplicativo cliente que define o intervalo real de valores para essas propriedades. Quando você usa as ferramentas e clientes fornecidos pelo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para procurar KPIs, valores menores do que -1 são tratados como -1, e valores maiores do que 1 são tratados como 1.  
  
 STATUS_GRAPHIC e TREND_GRAPHIC são valores de cadeia de caracteres que o aplicativo cliente usa para identificar o conjunto correto de imagens a serem exibidas. Essas cadeias de caracteres também definem o comportamento da função de exibição. Esse comportamento inclui o número de estados a serem exibidos (normalmente, esse é um número ímpar) e quais imagens serão usadas para cada um dos estados.  
  
### <a name="kpi-graphics-in-sql-server-data-tools"></a>Elementos gráficos de KPI nas Ferramentas de Dados do SQL Server  
 No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], os elementos gráficos de KPI podem ter três ou cinco estados. A tabela a seguir define os valores para cada um desses estados.  
  
|Número de estados para elementos gráficos de KPI|Valor desses estados|  
|--------------------------------------|---------------------------|  
|3|Ruim = -1 a -0,5<br /><br /> OK = -0,4999 a 0,4999<br /><br /> Bom = 0,50 a 1|  
|5|Inválido = -1 a -0,75<br /><br /> Risco = -0,7499 a -0,25<br /><br /> OK = -0,2499 a 0,2499<br /><br /> Subindo = 0,25 a 0,7499<br /><br /> Bom = 0,75 a 1|  
  
> [!NOTE]  
>  Para alguns gráficos, como o medidor invertido ou a seta de status invertida, o intervalo é invertido. Ou seja, -1 é bom e 1 é ruim.  
  
 No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], o nome do elemento gráfico de KPI determina se o gráfico tem três ou cinco estados. A tabela a seguir lista o uso, nome e número de estados que [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] associa a seus elementos gráficos de KPI.  
  
|Uso de gráfico|Nome de gráfico de KPI|Número de estados|  
|--------------------|-------------------------|----------------------|  
|Status|Formas|3|  
|Status|Sinal de trânsito|3|  
|Status|Placas de trânsito|3|  
|Status|Medidor|3|  
|Status|Medidor invertido|5|  
|Status|Termômetro|3|  
|Status|Cilindro|3|  
|Status|Faces|3|  
|Status|Seta de variação|3|  
|Tendência|Seta padrão|3|  
|Tendência|Seta de status|3|  
|Tendência|Seta de status invertida|5|  
|Tendência|Faces|3|  
  
## <a name="see-also"></a>Consulte Também  
 [Instrução DROP KPI retorna &#40; MDX &#41;](../mdx/mdx-data-definition-drop-kpi.md)   
 [Instruções de definição de dados MDX &#40; MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
