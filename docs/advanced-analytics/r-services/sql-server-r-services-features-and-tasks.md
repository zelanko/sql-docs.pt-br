---
title: "Recursos e tarefas do SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 52ad3f10-6d24-477a-aeb6-110456b2ed1c
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 13
---
# Recursos e tarefas do SQL Server R Services
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] combina o poder e a flexibilidade da linguagem de R de código-fonte aberto com ferramentas de nível empresarial para armazenamento de dados e gerenciamento, desenvolvimento de fluxo de trabalho e relatórios e visualização. Ele oferece suporte às necessidades dos profissionais de quatro dados diferentes e cenários.  
  
## Cientistas de dados: analise, modele e pontue usando R e SQL Server  
 Os cientistas de dados têm acesso a várias ferramentas de análise de dados e aprendizado de máquina, desde o conhecido Excel e plataformas de software livre, até pacotes de estatísticas que exigem conhecimento técnico avançado. Entre eles, o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] oferece benefícios exclusivos, pois permite que o cientista de dados envie cálculos ao banco de dados, evitando a movimentação de dados e atendendo às políticas de segurança corporativas. Além disso, o código R criado pelo cientista de dados pode facilmente ser implantado no ambiente de produção e solicitado por soluções e ferramentas corporativas conhecidas: aplicativos baseados em bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ferramentas de relatórios de BI e painéis. Com o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], o cientista de dados pode implantar e atualizar uma solução de análise enquanto atende aos requisitos padrão de gerenciamento de dados corporativos, incluindo segurança, facilidade de implantação, gerenciamento e monitoramento e auditoria de acesso.  
  
-   **Interface do usuário conhecida.**  Desenvolva e teste suas soluções usando o ambiente de desenvolvimento R de sua escolha.  
  
-   **Processamento no banco de dados.**  Execute o código R e realize os cálculos no computador que hospeda a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Isso elimina a necessidade de movimentação dos dados.  
  
-   **Desempenho e escalabilidade.**  Inclui escalonável pacotes R e APIs, para que você não está restrito pela arquitetura de thread único, o limite de memória de R. Você pode trabalhar com grandes conjuntos de dados e cálculos multithread, com vários núcleos, vários processos.  
    
-   **Portabilidade do código.**  O mesmo código de R executadas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados podem ser facilmente reutilizados em relação a outras fontes de dados, como Hadoop.  
  
 Para obter informações detalhadas sobre conceitos e tarefas relacionadas, consulte [exploração de dados e modelagem de previsão com R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md).  
  
## Desenvolvedores de aplicativos e de banco de dados: implantar soluções de R  
 Os desenvolvedores de banco de dados são responsáveis por integrar várias tecnologias e reunir os resultados para que possam ser compartilhados por toda a empresa. O desenvolvedor de banco de dados trabalha com os desenvolvedores de aplicativos, os desenvolvedores de SQL e os cientistas de dados para criar soluções, recomendar métodos de gerenciamento de dados e projetar e implantar soluções. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] fornece muitos benefícios aos desenvolvedores que trabalham com os cientistas de dados:  
  
-   **Interagir com scripts de R usando [!INCLUDE[tsql](../../includes/tsql-md.md)].**  Seus desenvolvedores e analistas de relatório, e desenvolvedores de banco de dados, podem invocar scripts R chamando procedimentos armazenados do sistema. Se sua solução usa agregações complexas ou envolve grandes conjuntos de dados, você pode ter computações executadas no banco de dados ou usar uma combinação de R e [!INCLUDE[tsql](../../includes/tsql-md.md)], dependendo do que fornece o melhor desempenho. A integração tranquilo com o  [!INCLUDE[tsql](../../includes/tsql-md.md)] é especialmente bem-vinda quando você precisa executar tarefas repetidamente em grandes quantidades de dados, como na geração de pontuações de previsão sobre os dados de produção.  
  
     A integração com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também significa que você pode executar scripts R em qualquer aplicativo que use o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Por exemplo, você pode chamar um procedimento armazenado de facilmente um [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] relatório para invocar o script R e gerar um gráfico juntamente com as previsões no relatório.  
  
-   **Desempenho e escalabilidade.**  Embora a linguagem de código-fonte aberto R têm limitações, o pacote RevoScaleR APIs fornecidas pelo [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] pode operar em grandes conjuntos de dados e se beneficiar de vários segmentos, com vários núcleos, vários processos computações no banco de dados.  
  
-   **Ferramentas de desenvolvimento e gerenciamento padrão.**  Não há a necessidade de qualquer ferramenta adicional para administração ou implantação; todos os trabalhos de R podem ser chamados pela invocação de um procedimento armazenado. Além disso, o mesmo código R executado nos dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser facilmente usado em outras fontes de dados, como o Hadoop.  
  
 Para obter informações detalhadas sobre conceitos e tarefas relacionadas, consulte [operacionalização seu código R](../../advanced-analytics/r-services/operationalizing-your-r-code.md).  
  
## Administradores de banco de dados: gerenciar soluções de análise avançada  
 Os administradores de banco de dados devem integrar projetos e prioridades concorrentes em um único ponto de contato: o servidor de banco de dados. Eles devem fornecer acesso aos dados não apenas aos cientistas de dados, mas a vários desenvolvedores de relatório, analistas de negócios e consumidores de dados comerciais, mantendo a integridade dos repositórios de dados operacionais e de relatórios. Na empresa, o DBA é uma parte fundamental da criação e implantação de uma infraestrutura eficiente para ciência de dados. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] fornece muitos benefícios ao administrador de banco de dados que oferece suporte à função de ciência de dados:  
  
-   **Segurança.**  A arquitetura do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] protege seus bancos de dados e isola a execução de sessões de R da operação da instância do banco de dados.  
  
     Você pode especificar quem tem permissão para executar scripts R e certifique-se de que os dados usados em trabalhos em R são gerenciados usando as mesmas funções de segurança que são definidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Confiabilidade.**  Sessões de R são executadas em um processo separado a fim de garantir que o servidor continue a executar como de costume, mesmo que a sessão de R encontre problemas.  
  
-   **Administração do recursos.**  Você pode controlar a quantidade de recursos alocados ao tempo de execução de R, para evitar que cálculos muito intensos prejudiquem o desempenho geral do servidor.  
  
 Para obter informações detalhadas sobre conceitos e tarefas relacionadas, confira [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
  
## Arquitetos e Designers de ETL: criar fluxos de trabalho integrados que envolvam R e SQL Server  
 Os engenheiros de dados projetam e compilam soluções de ETL. Os arquitetos projetam plataformas de dados que atendam às necessidades de negócios concorrentes e complementares. Porque [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] está profundamente integrado com outras ferramentas da Microsoft, como o business intelligence e pilha de depósito de dados, nuvem empresarial e ferramentas de mobilidade e Hadoop, ele fornece uma variedade de benefícios para o arquiteto de engenharia ou sistema de dados que deseja promover análises avançadas.  
  
-   **Amplo conjunto de ferramentas de desenvolvimento conhecidas.**  Ao desenvolver soluções em R, use o [!INCLUDE[tsql](../../includes/tsql-md.md)] e os procedimentos armazenados do sistema para preencher conjuntos de dados, executar trabalhos em R ou obter previsões. Chega de fluxos de trabalho paralelos em ferramentas de ciência de dados; crie seus pipelines de dados no ambiente familiar do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
     Você precisa usar dados em nuvem? Suporte para Data Factory do Azure e banco de dados do SQL Azure facilita a transformação e gerenciar dados e usam fontes de dados de nuvem em fluxos de trabalho apenas, como aquelas para o local [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados.  
  
-   **Criar e gerenciar fluxos de trabalho.**  Agendar trabalhos e criar fluxos de trabalho que contém scripts de R, usando procedimentos armazenados do sistema.  
  
 Para obter informações detalhadas sobre conceitos e tarefas relacionadas, consulte [Criando fluxos de trabalho que Use R no SQL Server](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md).  
  
## Consulte também  
 [Introdução ao SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  