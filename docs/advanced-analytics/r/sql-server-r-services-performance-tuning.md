---
title: Ajuste de desempenho para R
description: Este artigo descreve a otimização de desempenho para o R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4d7b6b91ac3aeaa45c5e6c3e05c12176f5f60b28
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727353"
---
# <a name="performance-tuning-for-r-in-sql-server"></a>Ajuste de desempenho de R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este é o primeiro de quatro artigos que descrevem a otimização de desempenho para R Services com base em dois estudos de caso:

- Testes de desempenho conduzidos pela equipe de desenvolvimento de produto para validar o perfil de desempenho de soluções de R

- Otimização de desempenho pela equipe de ciência de dados da Microsoft para um cenário de aprendizado de máquina específico, frequentemente solicitado pelos clientes.

O objetivo desta série é fornecer diretrizes sobre os tipos de técnicas de ajuste de desempenho que são mais úteis para executar trabalhos de R no SQL Server.

+ Este (primeiro) tópico fornece uma visão geral da arquitetura e alguns problemas comuns ao otimizar tarefas de ciência de dados.
+ O segundo artigo aborda as otimizações específicas de hardware e do SQL Server.
+ O terceiro artigo aborda otimizações nos recursos e no código R para operacionalização.
+ O quarto artigo descreve os métodos de teste em detalhes e relata descobertas e conclusões.

**Aplica-se a:** SQL Server 2016 R Services, Serviços de Machine Learning do SQL Server

## <a name="performance-goals-and-targeted-scenarios"></a>Metas de desempenho e cenários de destino

O recurso R Services foi introduzido no SQL Server 2016 para dar suporte à execução de scripts de R pelo SQL Server. Quando você usa esse recurso, o runtime de R opera em um processo separado do mecanismo de banco de dados, mas troca dados com segurança com o mecanismo de banco de dados usando recursos e serviços do servidor que interagem com o SQL Server, como o Trusted Launchpad.

No SQL Server 2017, foi anunciado o suporte para executar scripts de Python usando a mesma arquitetura, com linguagens adicionais a serem disponibilizadas no futuro.

À medida que aumenta o número de versões e linguagens com suporte, é importante que o administrador e o arquiteto do banco de dados estejam cientes do potencial de contenção de recursos devido a trabalhos de aprendizado de máquina e que possam configurar o servidor para dar suporte às novas cargas de trabalho. Embora manter a análise próxima dos dados elimine movimentações de dados inseguras, isso também tira as cargas de trabalho analíticas do laptop do cientista de dados e as coloca de volta no servidor que hospeda os dados.

Claramente, a otimização de desempenho para aprendizado de máquina não é uma solução unificada. Estas tarefas comuns podem ter perfis de desempenho muito diferentes:

- Tarefas de treinamento: criar e treinar um modelo de regressão versus treinar uma rede neural
- Engenharia de recursos usando R versus extração de recursos usando T-SQL
- Pontuação em linhas simples ou pequenos lotes versus pontuação em massa usando entradas de tabela
- Execução de pontuação em R versus implantação de modelos para produção no SQL Server em procedimentos armazenados
- Modificar o código R para minimizar a transferência de dados ou remover transformações de dados dispendiosas
- Habilitar testes automatizados e novos treinamentos de modelos

Como a escolha das técnicas de otimização depende de qual tarefa é essencial para seu aplicativo ou caso de uso, os estudos de caso abordam dicas de desempenho gerais e diretrizes sobre como otimizar para um cenário específico, a otimização para pontuação em lote.

+ **Opções de otimização individuais no SQL Server**

    No primeiro estudo de caso de desempenho, vários testes foram executados em um único conjunto de dados usando um único tipo de modelo. O algoritmo rxLinMod no RevoscaleR foi usado para criar um modelo e criar pontuações com base nele, mas o código, bem como as tabelas de dados subjacentes, foram alterados sistematicamente para testar o impacto de cada alteração.

    Por exemplo, em uma execução de teste, o código R foi alterado para que pudesse ser feita uma comparação entre a engenharia de recursos usando uma função de transformação versus pré-calculando os recursos e os carregando de uma tabela. Em outra execução de teste, o desempenho de treinamento do modelo foi comparado entre usar uma tabela indexada padrão versus dados em uma tabela com vários tipos de compactação ou novos tipos de índice.

+ **Otimização para um cenário de pontuação de alto volume específico**

    A tarefa de aprendizado de máquina no segundo estudo de caso envolve processar muitos currículos enviados para diversas vagas e encontrar o melhor candidato para cada uma delas. O próprio modelo de machine learning é formulado como um problema de classificação binária: ele usa um currículo e uma descrição de vaga como entrada e gera a probabilidade de cada par currículo-vaga. Como o objetivo é encontrar a melhor correspondência, um limite de probabilidade definido pelo usuário é usado para filtrar ainda mais e obter apenas as boas correspondências.

    Para essa solução, o objetivo principal era ter baixa latência durante a pontuação. No entanto, essa tarefa é computacionalmente dispendiosa mesmo durante o processo de pontuação, pois cada nova vaga precisa ser comparada a milhões de currículos em um período razoável. Além disso, a etapa de engenharia de recursos produz mais de 2.000 recursos por currículo ou vaga e é um gargalo de desempenho significativo.

Sugerimos que você examine todos os resultados do primeiro estudo de caso para determinar quais técnicas são aplicáveis à sua solução e avalie seu impacto potencial.

Em seguida, examine os resultados do estudo de caso de otimização de pontuação para ver como o autor aplicou técnicas diferentes e otimizou o servidor para dar suporte a uma carga de trabalho específica.

## <a name="performance-optimization-process"></a>Processo de otimização de desempenho

A configuração e o ajuste do desempenho exigem a criação de uma base sólida, sobre a qual as otimizações são dispostas em camadas projetadas para cargas de trabalho específicas:

- Escolher um servidor apropriado para hospedar a análise. Normalmente, um servidor de relatórios secundário, um data warehouse ou outro servidor que já esteja sendo usado para outro relatório ou análise é preferencial. No entanto, em uma solução de HTAP (processamento analítico transacional híbrido), dados operacionais podem ser usados como entrada para R para pontuação rápida.

- Configure a instância do SQL Server para balancear as operações do mecanismo de banco de dados e a execução do script de R ou Python em níveis apropriados. Isso pode incluir a alteração dos padrões do SQL Server para uso de memória e CPU, configurações de afinidade de NUMA e do processador e a criação de grupos de recursos.

- Otimizar o computador do servidor para dar suporte ao uso eficiente de scripts externos. Isso pode incluir o aumento do número de contas usadas para a execução de scripts externos, a habilitação do gerenciamento de pacotes e a atribuição de usuários a funções de segurança relacionadas.

- Aplicação de otimizações específicas ao armazenamento e à transferência de dados no SQL Server, incluindo estratégias de indexação e estatísticas, otimização e design de consultas e design das tabelas usadas para aprendizado de máquina. Você também pode analisar fontes de dados e métodos de transporte de dados ou modificar processos de ETL para otimizar a extração de recursos.

- Ajustar o modelo analítico para evitar ineficiências. O escopo das otimizações que são possíveis depende da complexidade do código R e dos pacotes e dados que você está usando. As principais tarefas incluem a eliminação de transformações de dados dispendiosas ou o descarregamento de tarefas de preparação de dados ou engenharia de recursos do R ou do Python para processos de ETL ou para o SQL. Você também pode refatorar scripts, eliminar instalações de pacotes embutidas, dividir o código R em procedimentos separados para treinamento, pontuação e avaliação ou simplificar o código para trabalhar de forma mais eficiente como um procedimento armazenado.

## <a name="articles-in-this-series"></a>Artigos nesta série

+ [Ajuste de desempenho de R no SQL Server – hardware](../r/sql-server-configuration-r-services.md)

    Fornece orientações para configurar o hardware no qual o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] está instalado e para configurar a instância do SQL Server para dar melhor suporte a scripts externos. É particularmente útil para **administradores de banco de dados**.

+ [Ajuste de desempenho para R no SQL Server – otimização de dados e código do R](../r/r-and-data-optimization-r-services.md)

    Fornece dicas específicas sobre como otimizar o script externo para evitar problemas conhecidos. É mais útil para **cientistas de dados**.

    > [!NOTE]
    > Embora grande parte das informações desta seção se apliquem ao R em geral, algumas informações são específicas para funções analíticas do RevoScaleR. Orientações detalhadas sobre o desempenho não estão disponíveis para **revoscalepy** e para outras bibliotecas de Python com suporte.
    >

+ [Ajuste de desempenho de R no SQL Server – métodos e resultados](../r/performance-case-study-r-services.md)

    Resume quais dados foram usados nos dois estudos de caso, como o desempenho foi testado e como as otimizações afetaram os resultados.
