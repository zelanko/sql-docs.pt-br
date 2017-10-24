---
title: "Tarefas de aprendizado de máquina do SQL Server | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 04/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52ad3f10-6d24-477a-aeb6-110456b2ed1c
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 60272ce672c0a32738b0084ea86f8907ec7fc0a5
ms.openlocfilehash: c0e7a0929d5caa84df1a1fb02894db08313a36bd
ms.contentlocale: pt-br
ms.lasthandoff: 09/06/2017

---
# <a name="sql-server-machine-learning-tasks"></a>Tarefas de aprendizado de máquina do SQL Server

O[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] combina o poder e a flexibilidade da linguagem R de software livre com ferramentas de nível corporativo para armazenamento e gerenciamento de dados, desenvolvimento de fluxo de trabalho, geração de relatórios e visualização. Este tópico descreve a ciclo de vida e como o SQL Server oferece suporte às necessidades de quatro profissionais de dados diferentes que são enagged no aprendizado de máquina de aprendizado de máquina.

## <a name="machine-learning-life-cycle"></a>Ciclo de vida de aprendizado de máquina

Aprendizado de máquina não é uma tarefa de curto prazo, mas em vez disso, um processo de longo prazo que abrange todos os aspectos dos dados da empresa. Aprendizado de máquina começa com a identificação de metas de negócios e regras e coleta de dados de sensores e aplicativos de negócios. Aprendizado de máquina é altamente dependente de processos de extração, processamento e armazenamento de dados e é cada vez mais importante ao considerar as políticas para armazenamento, extrair e dados de auditoria. Finalmente, o aprendizado de máquina agora é uma importante opriedades das estratégias para emissão de relatórios e análise, bem como envolvimento de clientes e comentários.



SQL Server é ideal para aprendizado de máquina, pois ele liga muitas das lacunas na processo de aprendizado de máquina:

+ Funciona no local ou na nuvem
+ Integrado em todos os estágios do processamento de dados da empresa, incluindo o business intelligence
+ Oferece suporte à segurança de dados aprimorados
+ Fornece controle de recursos e auditoria

## <a name="data-professionals-and-how-they-use-machine-learning"></a>Dados profissionais e como eles aprendizado de máquina de uso

### <a name="data-scientists"></a>Cientistas de dados

Os cientistas de dados tem acesso a uma variedade de ferramentas para análise de dados e aprendizado de máquina, variando de Excel ou plataformas livres do código-fonte aberto, a pacotes de estatísticas que exigem conhecimento técnico avançado. No entanto, a integração com o SQL Server oferece benefícios exclusivos:

+ Desenvolva e teste suas soluções usando o ambiente de desenvolvimento R de sua escolha.
+ Enviar computações no banco de dados, evitando a movimentação de dados em conformidade com políticas de segurança corporativas.
+ Desempenho e escalabilidade são aprimorados por meio de APIs e pacotes de R especiais. Você não é restritas por arquitetura de thread único, o limite de memória de R e pode trabalhar com grandes conjuntos de dados e cálculos multithread, com vários núcleos e vários processos.
+ Código R pode ser facilmente implantado para produção e chamado pelo painéis, aplicativos, outros bancos de dados e ferramentas empresariais.
+ Os cientistas de dados podem implantar e atualizar uma solução de análise enquanto atende aos requisitos padrão de gerenciamento de dados corporativos, incluindo segurança e auditoria de acesso
+ Portabilidade do código: facilmente usar novamente o seu código R em relação a outras fontes de dados, como o Hadoop

### <a name="application-and-database-developers"></a>Desenvolvedores de aplicativos e banco de dados

Os desenvolvedores de banco de dados são responsáveis por integrar várias tecnologias e reunir os resultados para que possam ser compartilhados por toda a empresa. O desenvolvedor de banco de dados trabalha com os desenvolvedores de aplicativos, os desenvolvedores de SQL e os cientistas de dados para criar soluções, recomendar métodos de gerenciamento de dados e projetar e implantar soluções. 

Integração com o SQL Server oferece estes benefícios aos desenvolvedores de dados que trabalham com o aprendizado de máquina:

+ Use as ferramentas familiares para interagir com scripts R. Permitir que o cientista de dados trabalhem em RStudio enquanto o desenvolvedor de dados implanta a solução usando o SQL Server Management Studio. Não há mais recodificar das soluções de R ou Python.
+ Otimize pela combinação de SQL e R, ou SQL e Python. Muitas vezes, operações complexas em grandes conjuntos de dados podem ser executadas com mais eficiência usando os recursos do SQL Server, como columnstoreindexes na memória ou agregações muito rápidas em T-SQL. Usar uma idioma de aprendizado de máquina em que faz sentido e usar o SQL para mover e processar dados.
+ Facilmente automatize tarefas que devem ser executado repetidamente em grandes quantidades de dados, como gerar pontuações de previsão nos dados de produção.
+ Executar script R ou Python em qualquer aplicativo que usa [!INCLUDE[tsql](../../includes/tsql-md.md)]. Basta chame um procedimento armazenado para criar um modelo com parâmetros, gere um gráfico complexo ou previsões de saída.
+ O **RevoScaleR** e **revoscalepy** APIs podem operar em grandes conjuntos de dados e se beneficiar de cálculos no banco de dados de vários segmentos, com vários núcleos e vários processos.

Para obter informações sobre tarefas relacionadas, consulte:
+ [Operationalizing Your R Code](../../advanced-analytics/r-services/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>Administradores de banco de dados

Os administradores de banco de dados devem integrar projetos e prioridades concorrentes em um único ponto de contato: o servidor de banco de dados. Eles devem fornecer acesso a dados não apenas aos cientistas de dados, mas a vários desenvolvedores de relatório, analistas de negócios e consumidores de dados corporativos, mantendo a integridade dos armazenamentos de dados operacionais e de relatório. Na empresa, o DBA é uma parte fundamental da criação e implantação de uma infraestrutura eficiente para a ciência de dados. 

SQL Server fornece recursos exclusivos para o administrador de banco de dados que deve oferecer suporte à função de ciência de dados:

+ Segurança pelo SQL Server: arquitetura de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] protege seus bancos de dados e isola a execução de sessões de script externo da operação da instância do banco de dados. Você pode especificar quem tem permissão para executar scripts de aprendizado de máquina e quem pode instalar novos pacotes de R, usando as funções de banco de dados.

+ Sessões de R e Python são executadas em um processo separado para garantir que o servidor continue a executar como de costume, mesmo que o script externo encontre problemas.

+ Governança de recursos usando o SQL Server permite que você controle a memória e os processos alocados para tempos de execução externos, para evitar que cálculos imensos prejudiquem o desempenho geral do servidor.

Para obter informações sobre tarefas relacionadas, consulte:
+ [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)

### <a name="architects-and-etl-designers"></a>Arquitetos e Designers de ETL

Os arquitetos projetam fluxos de trabalho integrados que abrangem todos os aspectos do ciclo de vida de aprendizado de máquina. Engenheiros de dados projetar e desenvolver soluções ETL e determinar como otimizar engenharia de recurso tarefas que fazem parte da processo de aprendizado de máquina. Geralmente, a plataforma de dados geral deve ser criada para equilibrar as necessidades de negócios concorrentes e complementares.

Já que o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] é profundamente integrado a outras ferramentas da Microsoft como as ferramentas de business intelligence e pilha de data warehouse, as ferramentas de mobilidade e nuvem empresarial e o Hadoop, ele fornece vários benefícios ao engenheiro de dados ou ao arquiteto de sistema que deseja promover análises avançadas.

+ Ferramentas de desenvolvimento familiar para desenvolver soluções de R e Python. Você pode chamar qualquer script Python ou R usando procedimentos armazenados do sistema, para preencher conjuntos de dados, gerar gráficos ou obter previsões. Não mais criando fluxos de trabalho paralelos em ciência de dados e ferramentas de ETL. Suporte do Azure Data Factory e banco de dados do SQL Azure facilita a transformação e gerenciar dados e usar fontes de dados de nuvem em fluxos de trabalho do aprendizado de máquina.

+ Agendamento e gerenciamento de recursos de operacionalização no Microsoft R Server.

Para obter informações sobre tarefas relacionadas, consulte:

+ [Criando fluxos de trabalho que usam R no SQL Server](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md)


