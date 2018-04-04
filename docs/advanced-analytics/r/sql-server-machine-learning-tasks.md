---
title: O processo de equipe e ciclo de vida de aprendizado de máquina | Microsoft Docs
ms.date: 11/03/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: b651085859d41125ea4e3d34e25292f245b4a99f
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2018
---
# <a name="machine-learning-lifecycle-and-personas"></a>Personas e ciclo de vida de aprendizado de máquina
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Projetos de aprendizado de máquina podem ser complexos, porque eles exigem as habilidades e a colaboração de um conjunto diferentes de profissionais. Este artigo descreve as principais tarefas no ciclo de vida de aprendizado de máquina, o tipo de profissionais de dados que estão envolvidos no aprendizado de máquina, e como o SQL Server oferece suporte às necessidades.

> [!TIP]
> 
> Antes de começar em um projeto de aprendizado de máquina, é recomendável que você examine as ferramentas e práticas recomendadas fornecidas pelo [processo de ciência de dados do Microsoft Team](https://blogs.technet.microsoft.com/machinelearning/2017/10/09/the-microsoft-team-data-science-process-tdsp-recent-updates/), ou TDSP. Esse processo foi criado por consultores da Microsoft para consolidar as práticas recomendadas para o planejamento e a iteração em projetos de aprendizado de máquina de aprendizado de máquina. O TDSP tem suas raízes em padrões do setor como CRISP-DM, mas incorpora práticas recentes como DevOps e visualização.

## <a name="machine-learning-life-cycle"></a>Ciclo de vida de aprendizado de máquina

Aprendizado de máquina é um processo complexo que abrange todos os aspectos dos dados da empresa e muitos projetos de aprendizado de máquina acabam demorando mais e sendo mais complexas do que o previsto. Aqui estão algumas das maneiras de aprendizado de máquina requer o suporte de profissionais de dados da empresa:

+ Aprendizado de máquina começa com a identificação de metas e regras de negócio.
+ Profissionais de aprendizado de máquina devem estar cientes das políticas de armazenamento, da extração e dados de auditoria.
+ Coleta de dados potencialmente aplicáveis é próxima.  Fontes de dados devem ser identificadas e os dados apropriados extraídos de sensores e aplicativos de negócios. 
+ A qualidade dos esforços de aprendizado de máquina é altamente dependente não apenas o tipo de dados que estão disponíveis, mas os processos muito usados para extrair, processamento e armazenamento de dados. 
+ Nenhum projeto de aprendizado de máquina estaria completo sem uma estratégia para emissão de relatórios e análise e possivelmente envolvimento de clientes e comentários.

SQL Server ajuda a ponte muitas das lacunas entre os profissionais de dados da empresa e especialistas de aprendizado de máquina:

+ Os dados podem ser armazenados no local ou na nuvem
+ O SQL Server é integrado em todos os estágios do processamento de dados corporativos, incluindo relatórios e ETL
+ SQL Server dá suporte à segurança de dados, a redundância de dados e auditoria
+ Fornece controle de recursos

## <a name="data-scientists"></a>Cientistas de dados

Cientistas de dados usam uma variedade de ferramentas de análise de dados e aprendizado de máquina, variando de Excel ou plataformas livres do código-fonte aberto, a pacotes de estatísticas que exigem conhecimento técnico avançado. No entanto, usar o R ou Python com o SQL Server oferece alguns benefícios exclusivos, em comparação com essas ferramentas tradicionais:

+ Você pode desenvolver e testar uma solução usando o ambiente de desenvolvimento de sua escolha e implantar seu código R ou Python como parte do código do T-SQL.
+ Mova cálculos complexos desativar laptop do cientista de dados e para o servidor, evitando a movimentação de dados de acordo com as políticas de segurança corporativas.
+ Desempenho e escalabilidade são aprimorados por meio de APIs e pacotes de R especiais. Você não é restritas por arquitetura de thread único, o limite de memória de R e pode trabalhar com grandes conjuntos de dados e cálculos multithread, com vários núcleos e vários processos.
+ Portabilidade do código: soluções podem ser executadas no SQL Server ou no Hadoop ou Linux, usando [Server de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server). O código de uma vez, implante em qualquer lugar.

## <a name="application-and-database-developers"></a>Desenvolvedores de aplicativo e banco de dados

Os desenvolvedores de banco de dados são responsáveis por integrar várias tecnologias e reunir os resultados para que possam ser compartilhados por toda a empresa. O desenvolvedor de banco de dados funciona com os desenvolvedores de aplicativos, os desenvolvedores do SQL e os cientistas de dados para criar soluções, recomendar métodos de gerenciamento de dados e a arquitetura ou implantar soluções.

Integração com o SQL Server fornece muitos benefícios aos desenvolvedores de dados:

+ O cientista de dados pode trabalhar em RStudio, enquanto o desenvolvedor de dados implanta a solução usando o SQL Server Management Studio. Não há mais recodificar das soluções de R ou Python.
+ Otimize suas soluções usando o melhor de T-SQL, R e Python. Operações complexas em grandes conjuntos de dados podem ser executadas com mais eficiência usando o SQL Server que em R. Aproveite o conhecimento de seu profissionais de banco de dados para melhorar o desempenho das soluções de aprendizado de máquina, usando índices columnstore na memória, e agregações usando operações do SQL com base em conjunto. 
+ Facilmente automatize tarefas que devem ser executado repetidamente em grandes quantidades de dados, como gerar pontuações de previsão nos dados de produção. 
+ Acesso com parâmetros de script R ou Python de qualquer aplicativo que usa [!INCLUDE[tsql](../../includes/tsql-md.md)]. Basta chame um procedimento armazenado para treinar um modelo, gerar um gráfico ou previsões de saída.
+ APIs podem transmitir grandes conjuntos de dados e se beneficiar de cálculos no banco de dados de vários segmentos, com vários núcleos e vários processos.

Para obter informações sobre tarefas relacionadas, consulte:
+ [Operacionalização do código R](../../advanced-analytics/r/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>Administradores de banco de dados

Os administradores de banco de dados devem integrar projetos e prioridades concorrentes em um único ponto de contato: o servidor de banco de dados. Eles devem fornecer acesso a dados não apenas aos cientistas de dados, mas a vários desenvolvedores de relatório, analistas de negócios e consumidores de dados corporativos, mantendo a integridade dos armazenamentos de dados operacionais e de relatório. Na empresa, o DBA é uma parte fundamental da criação e implantação de uma infraestrutura eficiente para a ciência de dados. 

SQL Server fornece recursos exclusivos para o administrador de banco de dados que deve oferecer suporte à função de ciência de dados:

+ Segurança pelo SQL Server: arquitetura de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] protege seus bancos de dados e isola a execução de sessões de script externo da operação da instância do banco de dados. Você pode especificar quem tem permissão para executar scripts de aprendizado de máquina e usar funções de banco de dados para gerenciar pacotes.

+ Sessões de R e Python são executadas em um processo separado para garantir que o servidor continue a executar como de costume, mesmo que o script externo encontre problemas.

+ Governança de recursos usando o SQL Server permite que você controle a memória e os processos alocados para tempos de execução externos, para evitar que cálculos imensos prejudiquem o desempenho geral do servidor.

Para obter informações sobre tarefas relacionadas, consulte:
+ [Gerenciando e monitorando soluções de aprendizado de máquina](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

## <a name="architects-and-data-engineers"></a>Engenheiros de arquitetos e dados

Os arquitetos projetam fluxos de trabalho integrados que abrangem todos os aspectos do ciclo de vida de aprendizado de máquina. Engenheiros de dados projetarem e desenvolver soluções ETL e determinam como otimizar as tarefas de engenharia de recurso para o aprendizado de máquina. A plataforma de dados geral deve ser criada para equilibrar as necessidades de negócios concorrentes.

Já que o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] é profundamente integrado a outras ferramentas da Microsoft como as ferramentas de business intelligence e pilha de data warehouse, as ferramentas de mobilidade e nuvem empresarial e o Hadoop, ele fornece vários benefícios ao engenheiro de dados ou ao arquiteto de sistema que deseja promover análises avançadas.

+ Chame qualquer script Python ou R usando procedimentos armazenados do sistema, para preencher conjuntos de dados, gerar gráficos ou obter previsões. Não mais criando fluxos de trabalho paralelos em ciência de dados e ferramentas de ETL. Suporte do Azure Data Factory e banco de dados do SQL Azure torna mais fácil de usar fontes de dados de nuvem em fluxos de trabalho do aprendizado de máquina.

+ Para agendamento e gerenciamento de tarefas de aprendizado de máquina, use fluxos de trabalho de automação standard no SQL Server, com base no Integration Services, SQL Agent ou do Azure Data Factory. Ou, use o [recursos operacionalização](https://docs.microsoft.com/machine-learning-server/operationalize/how-to-deploy-web-service-publish-manage-in-r) no servidor de aprendizado de máquina.

Para obter informações sobre tarefas relacionadas, consulte:

+ [Criando fluxos de trabalho de aprendizado de máquina no SQL Server](../../advanced-analytics/r/creating-workflows-that-use-r-in-sql-server.md)

