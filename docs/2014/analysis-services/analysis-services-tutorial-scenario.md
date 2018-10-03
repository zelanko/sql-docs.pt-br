---
title: Cenário do Tutorial do Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 2f5b1a42-b814-4d7d-b603-5383d9ac66b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7dddb6aec8d55a2a0495900b87661a431f8de9d0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106739"
---
# <a name="analysis-services-tutorial-scenario"></a>Cenário do tutorial de Analysis Services
  Este tutorial baseia-se na [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)], uma empresa fictícia. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] é uma grande empresa multinacional que produz e distribui bicicletas de metal e compostos para mercados comerciais da América do Norte, Europa e Ásia. A sede da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] é em Bothell, Washington, onde a empresa emprega 500 trabalhadores. Além disso, a [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] emprega várias equipes de vendas regionais por toda a sua base de mercado.  
  
 Nos últimos anos, a [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] adquiriu uma fábrica pequena, a Importadores Neptuno, situada no México. A Importadores Neptuno fabrica vários subcomponentes importantes para a linha de produtos da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] . Esses subcomponentes são transportados para as instalações de Bothell para o assembly de produto final. Em 2005, a Importadores Neptuno se tornou o fabricante e o distribuidor exclusivo do grupo de produtos de bicicleta de passeio.  
  
 Depois de um ano fiscal próspero, a [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] deseja ampliar sua participação no mercado, direcionando suas vendas para seus melhores clientes, estendendo a disponibilidade dos produtos através de um site externo e diminuindo o custo de vendas reduzindo os custos de produção.  
  
## <a name="current-analysis-environment"></a>Ambiente de análise atual  
 Para dar suporte às necessidades de análise de dados das equipes de vendas e marketing e do gerenciamento sênior, atualmente, a empresa usa dados transacionais do banco de dados [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] e informações não transacionais, como cotas de vendas de planilhas, e consolida essas informações no data warehouse relacional **AdventureWorksDW2012** . No entanto, o data warehouse relacional apresenta os seguintes desafios:  
  
-   Os relatórios são estáticos. Os usuários não têm como explorar os dados de maneira interativa para obter informações mais detalhadas, como eles fariam com uma tabela dinâmica do [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel. Embora o conjunto existente de relatórios predefinidos seja suficiente para muitos usuários, os usuários mais avançados precisam do acesso de consulta direta ao banco de dados para consultas interativas e relatórios especializados. Entretanto, devido à complexidade do banco de dados **AdventureWorksDW2012** , é preciso muito tempo para que esses usuários possam criar consultas eficientes.  
  
-   O desempenho da consulta é amplamente variável. Por exemplo, algumas consultas retornam resultados muito rapidamente, em apenas alguns segundos, enquanto outras precisam de muitos minutos.  
  
-   Tabelas de agregação são difíceis de gerenciar. Na tentativa de aprimorar o tempo de resposta da consulta, a equipe do data warehouse no [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] criou várias tabelas de agregação no banco de dados **AdventureWorksDW2012** . Por exemplo, foi criada uma tabela que resume as vendas por mês. Entretanto, enquanto essas tabelas de agregação melhoram amplamente o desempenho da consulta, a infraestrutura criada para manter as tabelas ao longo do tempo é frágil e suscetível a erros.  
  
-   A lógica de cálculo complexa foi descartada nas definições de relatório e o compartilhamento entre relatórios torna-se difícil. Como esta lógica corporativa é gerada separadamente para cada relatório, às vezes as informações de resumo são diferentes entre os relatórios. Portanto, o gerenciamento apresenta confiança limitada aos relatórios do data warehouse.  
  
-   Os usuários de diferentes unidades empresariais estão interessados em diferentes exibições de dados. Cada grupo é distraído e confundido por elementos de dados irrelevantes.  
  
-   A lógica de cálculo é particularmente desafiadora para usuários que precisam de relatórios especializados. Como esses usuários devem definir a lógica de cálculo separadamente para cada relatório, não há controle centralizado sobre como a lógica de cálculo é definida. Por exemplo, alguns usuários sabem que eles devem usar técnicas básicas de estatística, como as médias de movimentação, mas eles não sabem como construir esses cálculos e, portanto, deixam de usar as técnicas.  
  
-   É difícil combinar conjuntos relacionados de informações. Consultas especializadas que combinam dois conjuntos de informações relacionadas, como vendas e cotas de vendas, é um processo difícil para os usuários criarem. Como as consultas sobrecarregam o banco de dados, a empresa requer que os usuários solicitem os conjuntos de dados a partir da área de estudo da equipe do data warehouse. Como resultado, foram definidos apenas alguns dos relatórios predefinidos que combinam dados de várias áreas de estudo. Além disso, os usuários estão relutando em tentar modificar esses relatórios devido à complexidade.  
  
-   Nos estados Unidos, o foco dos relatórios está voltado principalmente para as informações empresariais. Os usuários de outras subsidiárias que não estão nos EUA demonstram uma certa insatisfação com esse foco, pois desejam visualizar os relatórios com dados de diferentes moedas e idiomas.  
  
-   É difícil examinar as informações. O departamento financeiro atual usa o banco de dados **AdventureWorksDW2012** apenas como uma fonte de dados para consultas em massa. O departamento baixa os dados em planilhas individuais e seus membros passam horas preparando dados e trabalhando com as planilhas. A empresa tem dificuldades em preparar, examinar e gerenciar os relatórios financeiros corporativos.  
  
## <a name="the-solution"></a>A solução  
 A equipe do data warehouse realizou recentemente uma revisão do design do sistema de análise atual. A revisão incluiu a análise de lacunas nos assuntos atuais e futuras demandas. A equipe do data warehouse determinou que o banco de dados **AdventureWorksDW2012** é um banco de dados dimensional bem projetado com dimensões compatíveis e chaves alternativas. As dimensões adequadas permitem que a dimensão seja usada em vários data marts, como a dimensão de tempo ou de produto. As chaves substitutas são chaves artificiais que vinculam a dimensão e as tabelas de fatos, e são usadas para garantir a singularidade e para melhorar o desempenho. Além disso, a equipe do data warehouse determinou que não há problemas significativos com o carregamento e o gerenciamento das tabelas base no banco de dados **AdventureWorksDW2012** . A equipe decidiu usar o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para:  
  
-   Fornecer acesso de dados unificado por uma camada de metadados comum para análise analítica e geração de relatórios.  
  
-   Simplificar a exibição de dados dos usuários direcionando o desenvolvimento de consultas e relatórios tanto interativas quanto predefinidas.  
  
-   Criar corretamente consultas que combinem dados de várias áreas de estudo.  
  
-   Gerenciar agregações.  
  
-   Armazenar e reutilizar cálculos complexos.  
  
-   Apresentar uma chance de trabalho a usuários empresariais que estejam fora dos Estados Unidos.  
  
 As lições no tutorial do Analysis Services fornecem orientação sobre como criar um banco de dados de cubo que atende a todas estas metas. Para começar, continue na primeira lição: [Lesson 1: Create a New Tabular Model Project](lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="see-also"></a>Consulte também  
 [Modelagem multidimensional &#40;Tutorial da Adventure Works&#41;](multidimensional-modeling-adventure-works-tutorial.md)  
  
  
