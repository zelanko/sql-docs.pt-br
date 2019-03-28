---
title: Desempenho do SQL Server R Services ajuste - serviços de aprendizado de máquina do SQL Server
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e547e2cd3c50e020d1164dc2b8aaffb31f4e3cb8
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510103"
---
# <a name="performance-tuning-for-r-in-sql-server"></a>Ajuste de desempenho para R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo é o primeiro de uma série de quatro artigos que descrevem a otimização de desempenho para R Services, com base em dois estudos de caso:

- Testes de desempenho conduzidos pela equipe de desenvolvimento de produto para validar o perfil de desempenho das soluções de R

- Otimização de desempenho pela equipe de ciência de dados da Microsoft para um cenário de aprendizado de máquina específica frequentemente solicitado pelos clientes.

O objetivo desta série é fornecer orientações sobre os tipos de técnicas que são mais úteis para a execução de trabalhos do R no SQL Server de ajuste de desempenho.

+ Este tópico (primeiro) fornece uma visão geral da arquitetura e alguns problemas comuns ao otimizar para tarefas de ciência de dados.
+ O segundo artigo aborda as otimizações do SQL Server e o hardware específico.
+ O terceiro artigo aborda as otimizações no código R e recursos para operacionalização.
+ O quarto artigo descreve os métodos de teste em detalhes e as descobertas de relatórios e conclusões.

**Aplica-se a:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services

## <a name="performance-goals-and-targeted-scenarios"></a>Metas de desempenho e cenários de destino

O recurso R Services foi introduzido no SQL Server 2016 para dar suporte à execução de scripts R pelo SQL Server. Quando você usa esse recurso, o tempo de execução de R opera em um processo separado do mecanismo de banco de dados, mas troca dados com segurança com o mecanismo de banco de dados, usando recursos de servidor e serviços que interagem com o SQL Server, como o Launchpad confiável.

No SQL Server 2017, o suporte foi anunciado para a execução de scripts de Python usando a mesma arquitetura, com um idioma adicional a seguir no futuro.

À medida que cresce o número de versões com suporte e de idioma, é importante que o administrador de banco de dados e o arquiteto do banco de dados estão cientes do potencial de contenção de recursos devido a trabalhos de aprendizado de máquina e que eles sejam capazes de configurar o servidor para dar suporte novas cargas de trabalho. Embora mantendo a análise próxima aos dados elimina as movimentações de dados inseguro, ele também move cargas de trabalho analíticas desativar o laptop do cientista de dados e volta para o servidor que hospeda os dados.

Otimização de desempenho para o machine learning não é claramente uma proposta única. As seguintes tarefas comuns podem ter perfis de desempenho muito diferentes:

- Tarefas de treinamento: criar e treinar um modelo de regressão versus treinar uma rede neural
- Engenharia de recursos usando o R versus a extração de recursos usando o T-SQL
- Pontuação em pequenos lotes, versus em massa usando entradas de tabela de pontuação ou de linhas simples
- Executar pontuação em R vs. implantação de modelos para produção no SQL Server em procedimentos armazenados
- Modificando o código R para minimizar a transferência de dados ou remover transformações de dados caros
- Habilitar testes automatizados e retreinamento de modelos

Como a escolha das técnicas de otimização depende de qual tarefa é essencial para seu aplicativo ou caso de uso, os estudos de caso abrangem dicas gerais de desempenho e diretrizes sobre como otimizar um cenário específico, a otimização para pontuação do lote.

+ **Opções de otimização individual no SQL Server**

    O primeiro estudo de caso de desempenho, vários testes foram executados em um único conjunto de dados usando um único tipo de modelo. O algoritmo rxLinMod RevoscaleR foi usado para criar um modelo e criar pontuações dele, mas o código, bem como as tabelas de dados subjacentes foram alteradas sistematicamente para testar o impacto de cada alteração.

    Por exemplo, uma execução de teste, o código R foi alterado para que uma comparação poderia ser feita entre a engenharia de recursos usando uma função de transformação versus previamente os recursos de computação e, em seguida, carregando recursos de uma tabela. Em outra execução de teste, o desempenho de treinamento do modelo foi comparado entre o uso de uma tabela indexada padrão versus dados em uma tabela com vários tipos de compactação ou novos tipos de índice.

+ **Otimização para um cenário específico de pontuação de alto volume**

    A tarefa de aprendizado de máquina no segundo estudo de caso envolve muitos currículos enviados para várias posições e localizar o melhor candidato para cada posição de trabalho de processamento. O próprio modelo de aprendizado de máquina é formulado como um problema de classificação binária: ela usa uma descrição do trabalho e retomada como entrada e gera a probabilidade para cada par de resume-job. Como o objetivo é encontrar a melhor correspondência, um limite de probabilidade definidas pelo usuário é usado para filtrar ainda mais e obter apenas as correspondências de BOM.

    Para esta solução, o principal objetivo era obter baixa latência durante a pontuação. No entanto, essa tarefa é computacionalmente cara, mesmo durante o processo de pontuação, pois cada novo trabalho deve ser comparado com milhões de resumos em um período razoável. Além disso, a etapa de engenharia de recurso produz recursos mais de 2.000 por retomar ou trabalho e é um gargalo de desempenho significativa.

Sugerimos que você examine todos os resultados do primeiro estudo de caso para determinar quais técnicas são aplicáveis à sua solução e avaliar seu impacto em potencial.

Em seguida, examine os resultados da pontuação estudo de caso de otimização para ver como o autor aplicado técnicas diferentes e o servidor para dar suporte a uma determinada carga de trabalho otimizado.

## <a name="performance-optimization-process"></a>Processo de otimização do desempenho

Configuração e ajuste de desempenho requer a criação de uma base sólida, na qual as otimizações de camada projetadas para cargas de trabalho específicas:

- Escolha um servidor apropriado para análise de host. Normalmente, um relatório secundário, data warehouse ou outro servidor que já é usado para outros relatórios ou análises é preferencial. No entanto, em uma solução de processamento transacional analíticos (HTAP) híbrido, dados operacionais podem ser usados como entrada para o R para pontuação rápida.

- Configurar a instância do SQL Server para operações de mecanismo de banco de dados de saldo e R ou execução em níveis apropriados de script do Python. Isso pode incluir a alteração de padrões do SQL Server para a memória e uso da CPU, NUMA e configurações de afinidade de processador e criação de grupos de recursos.

- Otimize o computador do servidor para dar suporte a um uso eficiente de scripts externos. Isso pode incluir o aumento do número de contas usadas para a execução do script externo, permitindo o gerenciamento de pacote, e atribuindo usuários relacionadas a funções de segurança.

- Aplicando otimizações específicas ao armazenamento de dados e transferência no SQL Server, incluindo a indexação e estratégias de estatísticas, design de consulta e otimização da consulta e o design de tabelas que são usados para aprendizado de máquina. Você também pode analisar as fontes de dados e dados de métodos de transporte ou modificar os processos de ETL para otimizar a extração de recursos.

- Ajuste o modelo analítico para evitar ineficiências. O escopo das otimizações possíveis dependem a complexidade do seu código R e os pacotes e os dados que você está usando. As tarefas principais incluem eliminar as transformações de dados caros ou descarregamento de dados de preparação ou recurso de engenharia tarefas do R ou Python para processos de ETL ou SQL. Você também pode refatorar scripts, eliminar instalações de pacote na linha, divida o código R em procedimentos separados de treinamento, pontuação e avaliação ou simplificar o código para trabalhar com mais eficiência como um procedimento armazenado.

## <a name="articles-in-this-series"></a>Artigos desta série

+ [Ajuste de desempenho para R no SQL Server - hardware](../r/sql-server-configuration-r-services.md)

    Fornece orientação para configurar o hardware que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] é instalado em e para configurar a instância do SQL Server para oferecer melhor suporte a scripts externos. É particularmente útil para **os administradores de banco de dados**.

+ [Ajuste de desempenho para R no SQL Server - código e dados de otimização](../r/r-and-data-optimization-r-services.md)

    Fornece dicas específicas sobre como otimizar o script externo para evitar problemas conhecidos. É mais útil **cientistas de dados**.

    > [!NOTE]
    > Embora muitas das informações nesta seção se aplica a R em geral, algumas informações são específicas para funções analíticas RevoScaleR. Diretrizes de desempenho detalhados não estão disponível para **revoscalepy** e outras bibliotecas de Python com suporte.
    >

+ [Ajuste de desempenho para R no SQL Server - métodos e os resultados](../r/performance-case-study-r-services.md)

    Resume os dados que foram usado dois estudos de caso, como o desempenho foi testado e como as otimizações afetado resultados.
