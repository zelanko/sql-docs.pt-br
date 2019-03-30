---
title: Aprendizado de máquina do ciclo de vida e o processo de equipe - serviços de aprendizado de máquina do SQL Server
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c06155a433718a068bc914b071f0f738cd236613
ms.sourcegitcommit: c60784d1099875a865fd37af2fb9b0414a8c9550
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58645428"
---
# <a name="machine-learning-lifecycle-and-personas"></a>Personalidades e ciclo de vida de aprendizado de máquina
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Projetos de aprendizado de máquina podem ser complexos, pois exigem as habilidades e a colaboração de um conjunto diferente de profissionais. Este artigo descreve as principais tarefas no ciclo de vida de aprendizado de máquina, o tipo de profissionais de dados que estão envolvidas em aprendizado de máquina e como o SQL Server dá suporte a necessidades.

> [!TIP]
> 
> Antes de você começar a usar em um projeto de aprendizado de máquina, é recomendável que você examine as ferramentas e práticas recomendadas fornecidas pelo [processo de ciência de dados de equipe do Microsoft](https://docs.microsoft.com/azure/machine-learning/team-data-science-process/overview), ou TDSP. Esse processo foi criado por consultores da Microsoft para consolidar as práticas recomendadas sobre planejamento e iterando em projetos de aprendizado de máquina de aprendizado de máquina. O TDSP tem suas raízes em padrões do setor como CRISP-DM, mas incorpora práticas recentes, como o DevOps e visualização.

## <a name="machine-learning-life-cycle"></a>Ciclo de vida de aprendizado de máquina

O Machine learning é um processo complexo que abrange todos os aspectos dos dados da empresa, e muitos projetos de aprendizado de máquina acabam levando mais tempo e que está sendo mais complexas do que o previsto. Aqui estão algumas das maneiras que o aprendizado de máquina requer o suporte de profissionais de dados da empresa:

+ Aprendizado de máquina começa com a identificação de metas e as regras de negócio.
+ Os profissionais de aprendizado de máquina devem estar cientes das políticas para armazenamento, extrair e dados de auditoria.
+ Coleta de dados potencialmente aplicáveis vem a seguir.  Fontes de dados devem ser identificadas e os dados apropriados são extraídos de sensores e aplicativos de negócios. 
+ A qualidade dos esforços de aprendizado de máquina é altamente dependente não apenas o tipo de dados que está disponíveis, mas muito processos usados para extrair, processamento e armazenamento de dados. 
+ Nenhum projeto de machine learning estaria completo sem uma estratégia para emissão de relatórios e análise e possivelmente o envolvimento do cliente e comentários.

SQL Server ajuda a acabar com muitas das lacunas entre os profissionais de dados corporativos e especialistas em aprendizado de máquina:

+ Dados podem ser armazenados localmente ou na nuvem
+ O SQL Server é integrado em cada estágio do processamento de dados empresariais, incluindo os relatórios e ETL
+ SQL Server dá suporte a segurança de dados, redundância de dados e auditoria
+ Fornece a governança de recursos

## <a name="data-scientists"></a>Cientistas de dados

Cientistas de dados usam uma variedade de ferramentas para análise de dados e aprendizado de máquina, variando de Excel ou plataformas de código-fonte aberto gratuitas, a pacotes de estatísticas que exigem conhecimento técnico avançado. No entanto, usando o R ou Python com o SQL Server fornece alguns benefícios exclusivos em comparação com essas ferramentas tradicionais:

+ Você pode desenvolver e testar uma solução usando o ambiente de desenvolvimento de sua escolha e implantar seu código R ou Python como parte de código T-SQL.
+ Mova computações complexas desativar laptop do cientista de dados e para o servidor, evitando a movimentação de dados para estar em conformidade com políticas de segurança da empresa.
+ Desempenho e escala são aprimorados por meio de pacotes de R especiais e APIs. Você não é restritos pela arquitetura de thread único, associado à memória de R e pode trabalhar com grandes conjuntos de dados e cálculos multithread, com vários núcleos e vários processos.
+ Portabilidade do código: Soluções podem ser executadas no SQL Server ou no Hadoop ou no Linux, usando [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server). O código uma vez, implante em qualquer lugar.

## <a name="application-and-database-developers"></a>Desenvolvedores de aplicativo e o banco de dados

Os desenvolvedores de banco de dados são responsáveis por integrar várias tecnologias e reunir os resultados para que possam ser compartilhados por toda a empresa. O desenvolvedor de banco de dados funciona com os desenvolvedores de aplicativos, os desenvolvedores SQL e os cientistas de dados para criar soluções, recomendar métodos de gerenciamento de dados e arquitetar ou implantar soluções.

Integração com o SQL Server fornece muitos benefícios aos desenvolvedores de dados:

+ O cientista de dados pode trabalhar no RStudio, enquanto o desenvolvedor de dados implanta a solução usando o SQL Server Management Studio. Não há mais recodificação de soluções de R ou Python.
+ Otimize suas soluções usando o melhor de T-SQL, R e Python. Operações complexas em grandes conjuntos de dados podem ser executadas muito mais eficiência usando o SQL Server que no R. Aproveite o conhecimento de seus profissionais de banco de dados para melhorar o desempenho das soluções de aprendizado de máquina, por meio de índices de columnstore na memória, e agregações usando operações do SQL com base em conjunto. 
+ Automatize com facilidade tarefas que devem ser executado repetidamente em grandes quantidades de dados, como geração de pontuações de previsão nos dados de produção. 
+ Acesso com parâmetros de script R ou Python em qualquer aplicativo que usa [!INCLUDE[tsql](../../includes/tsql-md.md)]. Basta chame um procedimento armazenado para treinar um modelo, gerar um gráfico ou previsões de saída.
+ APIs podem transmitir grandes conjuntos de dados e se beneficiar de cálculos no banco de dados de vários segmentos, com vários núcleos e vários processos.

Para obter informações sobre tarefas relacionadas, consulte:
+ [Operacionalização do código R](../../advanced-analytics/r/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>Administradores de banco de dados

Os administradores de banco de dados devem integrar projetos e prioridades concorrentes em um único ponto de contato: o servidor de banco de dados. Eles devem fornecer acesso a dados não apenas aos cientistas de dados, mas a vários desenvolvedores de relatório, analistas de negócios e consumidores de dados corporativos, mantendo a integridade dos armazenamentos de dados operacionais e de relatório. Na empresa, o DBA é uma parte fundamental da criação e implantação de uma infraestrutura eficiente para a ciência de dados. 

SQL Server fornece recursos exclusivos para o administrador de banco de dados que deve dar suporte à função de ciência de dados:

+ Segurança pelo SQL Server: A arquitetura do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] protege seus bancos de dados e isola a execução das sessões de script externo da operação da instância do banco de dados. Você pode especificar quem tem permissão para executar scripts de aprendizado de máquina e, em seguida, usar funções de banco de dados para gerenciar pacotes.

+ Sessões de R e Python são executadas em um processo separado para garantir que o servidor continue a executar como de costume, mesmo que o script externo encontre problemas.

+ Governança de recursos usando o SQL Server permite que você controle a memória e os processos alocados para tempos de execução externos, para evitar que cálculos imensos prejudiquem o desempenho geral do servidor.

Para obter informações sobre tarefas relacionadas, consulte:
+ [Gerenciando e monitorando soluções de aprendizado de máquina](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

## <a name="architects-and-data-engineers"></a>Engenheiros de dados e arquitetos

Arquitetos de projetar fluxos de trabalho integrados que abrangem todos os aspectos do ciclo de vida de aprendizado de máquina. Engenheiros de dados de design e criar soluções ETL e determinam como otimizar tarefas de engenharia de recurso para o aprendizado de máquina. A plataforma de dados geral deve ser projetada para equilibrar as necessidades de negócios concorrentes.

Já que o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] é profundamente integrado a outras ferramentas da Microsoft como as ferramentas de business intelligence e pilha de data warehouse, as ferramentas de mobilidade e nuvem empresarial e o Hadoop, ele fornece vários benefícios ao engenheiro de dados ou ao arquiteto de sistema que deseja promover análises avançadas.

+ Chame qualquer script do Python ou R, usando procedimentos armazenados do sistema, para preencher conjuntos de dados, gerar gráficos ou obter previsões. Sem mais projetar fluxos de trabalho paralelos em ferramentas de ETL e ciência de dados. Suporte para o Azure Data Factory e Azure SQL Database torna mais fácil de usar fontes de dados de nuvem em fluxos de trabalho de aprendizado de máquina.

+ Para agendamento e gerenciamento de tarefas de aprendizado de máquina, use fluxos de trabalho de automação padrão no SQL Server, com base no Integration Services, SQL Agent ou do Azure Data Factory. Ou, use o [recursos de operacionalização](https://docs.microsoft.com/machine-learning-server/operationalize/how-to-deploy-web-service-publish-manage-in-r) no Machine Learning Server.

Para obter informações sobre tarefas relacionadas, consulte:

+ [Criando fluxos de trabalho de aprendizado de máquina no SQL Server](../../advanced-analytics/r/creating-workflows-that-use-r-in-sql-server.md)

