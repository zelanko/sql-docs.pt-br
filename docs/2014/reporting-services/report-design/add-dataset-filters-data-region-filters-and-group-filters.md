---
title: Adicionar filtros de conjunto de dados, filtros de região de dados e filtros de grupo (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fcca7243-a702-4725-8e6f-cf118e988acf
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 7f133be198e7a141d13f0fded3ec17388308d44c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200806"
---
# <a name="add-dataset-filters-data-region-filters-and-group-filters-report-builder-and-ssrs"></a>Adicionar filtros de conjunto de dados, de região de dados e de grupo (Construtor de Relatórios e SSRS)
  Em um relatório, um filtro faz parte de um conjunto de dados, uma região de dados ou um grupo de regiões de dados criado por você para limitar os dados usados no relatório. Os filtros são uma forma de ajudar você a controlar os dados do relatório, caso você não possa alterar a consulta do conjunto de dados; por exemplo, se estiver usando um conjunto de dados compartilhado.  
  
 Os filtros ajudam a controlar os dados exibidos e processados em um relatório. É possível especificar filtros para um conjunto de dados, uma região de dados ou um grupo, em qualquer combinação.  
  
 Para obter mais informações, consulte [Adicionar um filtro a um conjunto de dados e SSRS&#40;Construtor de Relatórios e SSRS&#41;](../report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md) e [Exemplos de equações de filtro &#40;Construtor de Relatórios e SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="When"></a> Escolhendo quando definir um filtro  
 Especifique os filtros para itens de relatório quando você não puder filtrar dados na origem. Por exemplo, use os filtros de relatório quando a fonte de dados não oferecer suporte a parâmetros de consulta, quando você precisar executar procedimentos armazenados e não puder modificar a consulta ou quando um instantâneo de relatório com parâmetros exibir dados personalizados para usuários diferentes.  
  
 Você pode filtrar os dados do relatório antes ou depois de recuperá-los para gerar um conjunto de dados de relatório. Para filtrar os dados antes de eles serem recuperados, altere a consulta de cada conjunto de dados. Ao filtrar os dados da consulta, você filtra os dados na fonte de dados, reduzindo o volume de dados que precisa ser recuperado e processado em um relatório. Para filtrar os dados depois de recuperados, crie expressões de filtro no relatório. É possível definir expressões de filtro para um conjunto de dados, uma região de dados ou um grupo, incluindo grupos de detalhes. Você também pode incluir parâmetros nas expressões de filtro, sendo essa uma forma de filtrar os dados para valores ou usuários específicos, por exemplo, aplicando o filtro por um valor que identifica o usuário que está exibindo o relatório.  
  
##  <a name="Where"></a> Escolhendo onde definir um filtro  
 Determine onde você deseja definir um filtro pelo efeito que deseja obter em seu relatório. No tempo de execução, o processador de relatório aplica filtros na seguinte ordem: no conjunto de dados e na região de dados e nos grupos de cima para baixo em cada hierarquia de grupo. Em uma tabela, matriz e lista, os filtros para grupos de linha, grupos de coluna e grupos adjacentes são aplicados de forma independente. Em um gráfico, os filtros para grupos de categoria e grupos de série são aplicados de forma independente. Quando o processador de relatório aplica o filtro, todas as equações de filtros são aplicadas na ordem em que elas foram definidas na página **Filtro** da caixa de diálogo **Propriedades** para cada item de relatório, que é o equivalente a combiná-los com as operações boolianas AND.  
  
 A lista a seguir compara o efeito de definir filtros em itens de relatório diferentes:  
  
-   **No conjunto de dados** Defina o filtro no conjunto de dados quando desejar que uma ou mais regiões de dados associadas a um único conjunto de dados sejam filtradas da mesma maneira. Por exemplo, defina o filtro no conjunto de dados associado a uma tabela que exibe os dados de vendas e um gráfico que exibe os mesmos dados.  
  
-   **Na região de dados** Defina um filtro na região de dados quando quiser que uma ou mais regiões de dados associadas a um único conjunto de dados forneçam uma exibição diferente do conjunto de dados. Por exemplo, defina o filtro em uma região de dados Tabela para exibir as dez principais lojas para vendas e uma região de dados Tabela diferente para exibir as dez últimas lojas para vendas no mesmo relatório.  
  
-   **Nos grupos de colunas ou linhas em uma região de dados Tablix** Defina um filtro em um grupo quando quiser incluir ou excluir determinados valores para uma expressão de grupo controlar quais valores de grupo são exibidos na tabela, matriz ou lista.  
  
-   **No grupo de detalhes em uma região de dados Tablix** Defina um filtro no grupo de detalhes para uma região de dados quando tiver vários grupos de detalhes para uma região de dados e quiser que cada grupo de detalhes exiba um conjunto de dados diferente do conjunto de dados.  
  
-   **Nos grupos de categorias ou séries em uma região de dados Gráfico** Defina um valor em um grupo de séries ou categorias quando quiser incluir ou excluir determinados valores para uma expressão de grupo, a fim de controlar quais os valores exibidos no gráfico.  
  
##  <a name="FilterEquations"></a> Entendendo uma equação de filtro  
 Em tempo de execução, o processador de relatório converte o valor para o tipo de dados especificado e usa o operador especificado para comparar a expressão e o valor. A lista a seguir descreve cada parte da equação de filtro:  
  
-   **Expressão** Define o que você está filtrando. Geralmente, isso é um campo de conjunto de dados.  
  
-   **Tipo de Dados** Especifica o tipo de dados a ser usado quando a equação de filtro é avaliada em tempo de execução pelo processador de relatórios. O tipo de dados selecionado deve ser um dos tipos de dados com suporte do esquema de definição de relatórios.  
  
-   **Operador** Define como comparar as duas partes da equação do filtro.  
  
-   `Value` Define a expressão a ser usada na comparação.  
  
 As seções a seguir descrevem cada parte da equação de filtro.  
  
### <a name="expression"></a>Expression  
 Quando a equação de filtro é avaliada pelo processador de relatórios em tempo de execução, os tipos de dados da expressão e o valor devem ser iguais. O tipo de dados do campo selecionado para **Expressão** é determinado pela extensão de processamento de dados ou pelo provedor de dados usado para recuperar dados da fonte de dados. O tipo de dados da expressão digitado para `Value` é determinado pelo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] padrões. As opções do tipo de dados são determinadas pelos tipos de dados suportados para uma definição de relatório. Os valores do banco de dados podem ser convertidos pelo provedor de dados em um tipo CLR.  
  
### <a name="data-type"></a>Tipo de Dados  
 Para o processador de relatórios comparar os dois valores, os tipos de dados devem ser iguais. A tabela a seguir lista o mapeamento entre os tipos de dados CLR e os tipos de dados de definição de relatórios. Os dados recuperados de uma fonte de dados podem ser convertidos em um tipo de dados diferente até o momento em que os dados são relatados.  
  
|**Tipo de dados de esquema de definição de relatórios**|**Tipo(s) CLR**|  
|--------------------------------------------|-----------------------|  
|`Boolean`|`Boolean`|  
|`DateTime`|`DateTime`, `DateTimeOffset`|  
|`Integer`|`Int16`, `Int32`, `UInt16`, `Byte`, `SByte`|  
|`Float`|`Single`, `Double`, `Decimal`|  
|`Text`|`String`, `Char`, `GUID`, `Timespan`|  
  
 Em casos em que você deve especificar um tipo de dados, você pode especificar sua própria conversão na parte da expressão Valor.  
  
### <a name="operator"></a>Operador  
 A tabela a seguir lista os operadores que podem ser usados em uma equação de filtro e o que o processador de relatórios usa para avaliar a equação de filtro.  
  
|Operador|Ação|  
|--------------|------------|  
|**Equal, Like, NotEqual, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual**|Compara a expressão a um valor.|  
|**TopN, BottomN**|Compara a expressão a um valor `Integer`.|  
|**TopPercent, BottomPercent**|Compara a expressão com um `Integer` ou `Float` valor.|  
|**Entre**|Testa se a expressão está entre dois valores, inclusive.|  
|**Entrada**|Testa se a expressão está contida em um conjunto de valores.|  
  
### <a name="value"></a>Valor  
 A expressão Valor especifica a parte final da equação do filtro. O processador de relatórios converte a expressão avaliada para o tipo de dados especificado e avalia a equação de filtro inteira para determinar se os dados especificados na Expressão são transmitidos pelo filtro.  
  
 Para converter para um tipo de dados que não seja um tipo de dados CLR, você deve modificar a expressão para converter explicitamente para um tipo de dados. Você pode usar as funções de conversão listadas na caixa de diálogo **Expressão** em **Funções Comuns**, **Conversão**. Por exemplo, para um campo `ListPrice` que representa os dados armazenados como um tipo de dados **dinheiro** em uma fonte de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a extensão de processamento de dados retornará o valor de campo como um tipo de dados <xref:System.Decimal> . Para definir um valor para usar somente valores maiores de **US$ 50.000,00** na moeda do relatório, converta o valor para Decimal usando a expressão `=CDec(50000.00)`.  
  
 Esse valor também pode incluir uma referência de parâmetro para permitir que um usuário selecione um valor interativamente.  
  
## <a name="see-also"></a>Consulte também  
 [Usos de expressões em relatórios &#40;relatórios e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](report-parameters-report-builder-and-report-designer.md)  
  
  
