---
title: "Criar uma dimensão de tipo de data | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time dimensions [Analysis Services]
- dimensions [Analysis Services], time
- adding time intelligence
- server time dimensions [Analysis Services]
- calendars [Analysis Services]
- time intelligence [Analysis Services]
ms.assetid: 6d692856-4b01-4dca-a650-f97ac220c114
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 38a9c9d9a1fc035d652525b9ec0564977ac691bf
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="database-dimensions---create-a-date-type-dimension"></a>Dimensões de banco de dados - criar uma dimensão de tipo de data
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], uma dimensão de tempo é um tipo de dimensão cujos atributos representam períodos, como anos, semestres, trimestres, meses e dias. Os períodos em uma dimensão de tempo fornecem níveis de granularidade baseados em tempo para análises e geração de relatórios. Os atributos são organizados em hierarquias e a granularidade da dimensão de tempo é determinada em maior parte pelos requisitos de negócios e reporte de dados históricos. Por exemplo, a maioria dos dados financeiros e de vendas dos aplicativos de business intelligence usa uma granularidade mensal ou trimestral.  
  
 Normalmente, os cubos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incorporam uma dimensão de tempo de uma outra forma. Um cubo pode conter mais de uma dimensão de tempo ou várias hierarquias provenientes da mesma dimensão de tempo, dependendo da granularidade dos dados e dos requisitos de reporte. Contudo, nem todos os cubos requerem uma dimensão de tempo. Alguns aplicativos OLAP, como os de custos por atividade, não precisam de uma dimensão de tempo porque a geração de custos em uma dimensão baseada em atividades usa as atividades em vez do tempo.  
  
## <a name="dimension-structure"></a>Estrutura da Dimensão  
 A estrutura de uma dimensão de tempo depende de como a fonte de dados subjacente armazena as informações do período de tempo. Essa diferença no armazenamento produz dois tipos básicos de dimensões de tempo:  
  
 Dimensão de tempo  
 Dimensões de tempo são semelhantes a outras dimensões com relação ao fornecimento pela tabela de dimensões dos atributos para a dimensão. Cada coluna da tabela principal da dimensão define um atributo para um período específico.  
  
 Como outras dimensões, a tabela de fatos possui uma relação de chave estrangeira com a tabela de dimensões para a dimensão de tempo. O atributo principal de uma dimensão de tempo baseia-se em uma chave de número inteiro ou no nível mais baixo de detalhe, como a data, que aparece na tabela principal da dimensão.  
  
 Dimensão de tempo de servidor  
 Se não houver uma tabela de dimensões à qual associar atributos relacionados a tempo, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pode definir uma dimensão de tempo de servidor com base em períodos de tempo. Para definir as hierarquias, os níveis e os membros representados pela dimensão de tempo de servidor, selecione períodos de tempo padrão ao criar a dimensão.  
  
 Os atributos de uma dimensão de tempo de servidor possuem uma associação tempo-atributo especial. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza os tipos de atributo relacionados a datas, como Ano, Mês ou Dia, para definir os membros dos atributos de uma dimensão de tempo.  
  
 Depois de incluir a dimensão de tempo de servidor em um cubo, defina a relação entre o grupo de medidas e a dimensão de tempo de servidor especificando uma relação na página **Definir Uso da Dimensão** do Assistente para Cubos.  
  
### <a name="calendars"></a>Calendários  
 Em uma dimensão de tempo ou dimensão de tempo de servidor, os atributos são agrupados em hierarquias. Geralmente, essas hierarquias são denominadas calendários.  
  
 Os aplicativos de business intelligence frequentemente requerem várias definições de calendário. Por exemplo, o departamento de recursos humanos pode monitorar os funcionários usando um calendário *padrão* : um calendário gregoriano de doze meses, começando em 1º de janeiro e terminando em 31 de dezembro. No entanto, o mesmo departamento de recursos humanos pode monitorar despesas usando um calendário *fiscal* : um calendário de doze meses que estabelece o ano fiscal usado pela empresa.  
  
 Você pode construir manualmente esses calendários distintos no Designer de Dimensão. No entanto, o Assistente para Dimensões fornece vários modelos de hierarquia que podem ser usados para gerar automaticamente diversos tipos de calendários quando você criar uma dimensão de tempo ou uma dimensão de tempo de servidor. A tabela a seguir descreve os vários calendários que o Assistente para Dimensões pode gerar.  
  
|Calendário|Description|  
|--------------|-----------------|  
|Calendário padrão|Um calendário gregoriano de doze meses, começando em 1º. de janeiro e terminando em 31 de dezembro.<br /><br /> Independentemente de você usar o Assistente para Dimensões para criar uma dimensão de tempo ou uma dimensão de tempo de servidor, o assistente gerará uma hierarquia para um calendário padrão depois que você definir os atributos que representam os períodos de tempo da dimensão. Se você usar o Assistente para Dimensões para criar uma dimensão de tempo de servidor, poderá ajustar a data inicial do calendário padrão para outro dia que não seja 1º. de janeiro.|  
|Calendário fiscal|Um calendário fiscal de doze meses. Ao selecionar esse calendário, especifique o dia e o mês iniciais para o ano fiscal usado pela empresa.<br /><br /> Observação: esse calendário estará disponível somente se você usar o Assistente para Dimensões para criar uma dimensão de tempo de servidor.|  
|Calendário de relatório (ou calendário comercial)|Um calendário de relatório de doze meses que inclui dois meses de quatro semanas e um mês de cinco semanas em um padrão repetitivo de três meses (trimestral). Ao selecionar esse calendário, especifique o dia e o mês iniciais e o padrão trimestral de 4–4–5, 4–5–4 ou 5–4–4 semanas, sendo que cada dígito representa o número de semanas do mês.<br /><br /> Observação: esse calendário estará disponível somente se você usar o Assistente para Dimensões para criar uma dimensão de tempo de servidor.|  
|Calendário de produção|Um calendário que usa 13 períodos de quatro semanas, dividido em três trimestres de três períodos e um trimestre de quatro períodos. Ao selecionar esse calendário, especifique a semana (entre 1 e 4) e o mês iniciais para o ano de produção usado pela empresa e também identifique qual trimestre conterá quatro períodos.<br /><br /> Observação: esse calendário estará disponível somente se você usar o Assistente para Dimensões para criar uma dimensão de tempo de servidor.|  
|Calendário ISO 8601|O calendário padrão de representação de datas e hora da Organização Internacional de Padronização (ISO) (8601). Esse calendário possui um número integrante de semanas de 7 dias. O ano novo pode começar vários dias antes ou depois do início do ano novo, com base no calendário gregoriano. A primeira semana desse calendário é determinada pela primeira semana do calendário gregoriano que contém uma quinta-feira. Portanto, o primeiro dia dessa semana, o domingo, pode cair de fato no ano anterior.<br /><br /> Observação: esse calendário estará disponível somente se você usar o Assistente para Dimensões para criar uma dimensão de tempo de servidor.|  
  
 Quando você criar uma dimensão de tempo de servidor e especificar os períodos de tempo e os calendários que serão usados nessa dimensão, o Assistente para Dimensões adicionará os atributos para os períodos de tempo que são apropriados para cada calendário especificado. Por exemplo, se você criar uma dimensão de tempo de servidor que usa anos como período de tempo e inclui os calendários fiscal e de relatório, o assistente adicionará à dimensão os atributos FiscalYear e ReportingYears, além do atributo padrão Years. Uma dimensão de tempo de servidor também terá atributos para combinações de períodos de tempo selecionados, como um atributo DayOfWeek para uma dimensão que contém Dias e Semanas. O Assistente para Dimensões criará uma hierarquia de calendário combinando atributos que pertencem a um único tipo de calendário. Por exemplo, a hierarquia de um calendário fiscal pode conter os seguintes níveis: Ano Fiscal, Semestre Fiscal, Trimestre Fiscal, Mês Fiscal e Dia Fiscal.  
  
## <a name="adding-time-intelligence-with-the-business-intelligence-wizard"></a>Adicionando inteligência de tempo com o Assistente de Business Intelligence  
 Depois de configurar a dimensão de tempo e adicioná-la a um cubo, você pode usar o Assistente de Business Intelligence para adicionar funcionalidades de inteligência de tempo, como medidas de período até esta data, de período a período e média de movimentação. Para obter mais informações, consulte [Definir cálculos de inteligência de tempo com o Assistente de Business Intelligence](../../analysis-services/multidimensional-models/define-time-intelligence-calculations-using-the-business-intelligence-wizard.md).  
  
> [!NOTE]  
>  Não é possível usar o Assistente de Business Intelligence para adicionar inteligência de tempo a dimensões de tempo de servidor. O Assistente de Business Intelligence adiciona uma hierarquia para oferecer suporte à inteligência de tempo e ela deve ser associada a uma coluna da tabela da dimensão de tempo. As dimensões de tempo de servidor não possuem uma tabela de dimensão de tempo correspondente e, portanto, não comportam essa hierarquia adicional.  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma dimensão de tempo ao gerar uma tabela de tempo](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)   
 [Ajuda de F1 do Assistente do Business Intelligence](http://msdn.microsoft.com/library/155ac80c-63ae-47aa-9e86-9396e3d920eb)   
 [Tipos de dimensão](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
