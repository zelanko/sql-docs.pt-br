---
title: Ajuste de desempenho do SQL Server R Services
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: dd12e38e0d1f01cd142cc4c11efe43346dd1f8ce
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715626"
---
# <a name="performance-tuning-for-r-in-sql-server"></a>Ajuste de desempenho para R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo é o primeiro de uma série de quatro artigos que descrevem a otimização de desempenho para o R Services, com base em dois estudos de caso:

- Testes de desempenho conduzidos pela equipe de desenvolvimento do produto para validar o perfil de desempenho de soluções de R

- Otimização de desempenho pela equipe de ciência de dados da Microsoft para um cenário de aprendizado de máquina específico, geralmente solicitado pelos clientes.

O objetivo desta série é fornecer orientações sobre os tipos de técnicas de ajuste de desempenho que são mais úteis para executar trabalhos de R em SQL Server.

+ Este tópico (primeiro) fornece uma visão geral da arquitetura e alguns problemas comuns ao otimizar tarefas de ciência de dados.
+ O segundo artigo aborda as otimizações específicas de hardware e SQL Server.
+ O terceiro artigo aborda otimizações em código R e recursos para operacionalização.
+ O quarto artigo descreve os métodos de teste em detalhes e relata conclusões e conclusões.

**Aplica-se a:** SQL Server serviços de 2016, SQL Server Serviços de Machine Learning

## <a name="performance-goals-and-targeted-scenarios"></a>Metas de desempenho e cenários de destino

O recurso R Services foi introduzido no SQL Server 2016 para dar suporte à execução de scripts R por SQL Server. Quando você usa esse recurso, o tempo de execução de R opera em um processo separado do mecanismo de banco de dados, mas troca dados com segurança com o mecanismo de banco de dados, usando recursos de servidor e serviços que interagem com SQL Server, como o Launchpad confiável.

No SQL Server 2017, o suporte foi anunciado para executar scripts Python usando a mesma arquitetura, com idioma adicional a ser seguido no futuro.

À medida que aumenta o número de versões e idiomas com suporte, é importante que o administrador de banco de dados e o arquiteto de banco de dados estejam cientes do potencial de contenção de recursos devido a trabalhos de aprendizado de máquina e que eles possam configurar o servidor para dar suporte ao as novas cargas de trabalho. Embora manter a análise perto dos dados elimine os movimentos de dados inseguros, ele também move as cargas de trabalho analíticas do laptop do cientista de dados e de volta para o servidor que hospeda os dados.

A otimização de desempenho para o aprendizado de máquina não é claramente uma proposta de tamanho único. As seguintes tarefas comuns podem ter perfis de desempenho muito diferentes:

- Tarefas de treinamento: Criando e treinando um modelo de regressão versus treinando uma rede neural
- Engenharia de recursos usando R versus extração de recursos usando o T-SQL
- Pontuação em linhas simples ou pequenos lotes, versus a pontuação em massa usando entradas de tabela
- Execução de pontuação em R versus implantação de modelos para produção em SQL Server procedimentos armazenados
- Modificando o código R para minimizar a transferência de dados ou remover transformações de dados dispendiosas
- Habilitar teste automatizado e readaptação de modelos

Como a escolha das técnicas de otimização depende de qual tarefa é essencial para seu aplicativo ou caso de uso, os estudos de caso abordam as dicas de desempenho gerais e orientações sobre como otimizar para um cenário específico, otimização para Pontuação de lote.

+ **Opções de otimização individuais no SQL Server**

    No primeiro estudo de caso de desempenho, vários testes foram executados em um único conjunto de uma única vez usando um único tipo de modelo. O algoritmo rxLinMod em RevoscaleR foi usado para criar um modelo e criar pontuações a partir dele, mas o código, bem como as tabelas de dados subjacentes, foram sistematicamente alterados para testar o impacto de cada alteração.

    Por exemplo, em uma execução de teste, o código R foi alterado para que uma comparação possa ser feita entre a engenharia de recursos usando uma função de transformação vs. pré-computando os recursos e carregando recursos de uma tabela. Em outra execução de teste, o desempenho de treinamento do modelo foi comparado entre usar uma tabela indexada padrão versus dados em uma tabela com vários tipos de compactação ou novos tipos de índice.

+ **Otimização para um cenário de Pontuação de alto volume específico**

    A tarefa de aprendizado de máquina no segundo estudo de caso envolve o processamento de muitas retomadas enviadas para várias posições e a localização do melhor candidato para cada posição de trabalho. O próprio modelo de Machine Learning é formulado como um problema de classificação binária: ele usa uma retomada e uma descrição de trabalho como entrada e gera a probabilidade para cada par retomar trabalho. Como o objetivo é encontrar a melhor correspondência, um limite de probabilidade definido pelo usuário é usado para filtrar ainda mais e obter apenas as boas correspondências.

    Para essa solução, o objetivo principal era atingir baixa latência durante a pontuação. No entanto, essa tarefa é computacionalmente dispendiosa mesmo durante o processo de pontuação, pois cada novo trabalho deve ser correspondido em milhões de currículos em um período de tempo razoável. Além disso, a etapa de engenharia de recursos produz mais de 2000 recursos por currículo ou trabalho e é um afunilamento de desempenho significativo.

Sugerimos que você revise todos os resultados do primeiro estudo de caso para determinar quais técnicas são aplicáveis à sua solução e avalie seu impacto potencial.

Em seguida, examine os resultados do estudo de caso de otimização de Pontuação para ver como o autor aplicou técnicas diferentes e otimizou o servidor para dar suporte a uma carga de trabalho específica.

## <a name="performance-optimization-process"></a>Processo de otimização de desempenho

A configuração e o ajuste do desempenho exigem a criação de uma base sólida, na qual as otimizações de camada são projetadas para cargas de trabalho específicas:

- Escolha um servidor apropriado para hospedar a análise. Normalmente, um secundário de relatório, data warehouse ou outro servidor que já esteja sendo usado para outro relatório ou análise é preferencial. No entanto, em uma solução de HTAP (processamento analítico transacional) híbrido, os dados operacionais podem ser usados como entrada para R para Pontuação rápida.

- Configure a instância de SQL Server para balancear as operações do mecanismo de banco de dados e a execução do script R ou Python em níveis apropriados. Isso pode incluir a alteração SQL Server padrões de uso de memória e CPU, configurações de afinidade em NUMA e de processador e criação de grupos de recursos.

- Otimize o computador servidor para dar suporte ao uso eficiente de scripts externos. Isso pode incluir o aumento do número de contas usadas para a execução de script externo, a habilitação do gerenciamento de pacotes e a atribuição de usuários a funções de segurança relacionadas.

- Aplicação de otimizações específicas ao armazenamento de dados e transferência em SQL Server, incluindo estratégias de indexação e estatísticas, otimização de design e consulta de consulta e o design de tabelas usadas para aprendizado de máquina. Você também pode analisar fontes de dados e métodos de transporte de dados ou modificar processos de ETL para otimizar a extração de recursos.

- Ajuste o modelo analítico para evitar ineficiências. O escopo das otimizações que são possíveis depende da complexidade do código R e dos pacotes e dados que você está usando. As principais tarefas incluem a eliminação de transformações de dados dispendiosas ou a descarregamento de tarefas de preparação de dados ou de engenharia de recursos de R ou Python para processos de ETL ou SQL. Você também pode refatorar scripts, eliminar instalações de pacotes embutidas, dividir o código R em procedimentos separados para treinamento, pontuação e avaliação, ou simplificar o código para trabalhar de forma mais eficiente como um procedimento armazenado.

## <a name="articles-in-this-series"></a>Artigos desta série

+ [Ajuste de desempenho para R em SQL Server-hardware](../r/sql-server-configuration-r-services.md)

    Fornece orientação para configurar o hardware que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] está instalado no e para configurar a instância de SQL Server para oferecer melhor suporte a scripts externos. Ele é particularmente útil para **Administradores de banco de dados**.

+ [Ajuste de desempenho para R no código de SQL Server e otimização de dados](../r/r-and-data-optimization-r-services.md)

    Fornece dicas específicas sobre como otimizar o script externo para evitar problemas conhecidos. Ele é mais útil para **cientistas de dados**.

    > [!NOTE]
    > Embora grande parte das informações contidas nesta seção se aplique ao R em geral, algumas informações são específicas para as funções analíticas RevoScaleR. As diretrizes detalhadas de desempenho não estão disponíveis para **revoscalepy** e outras bibliotecas Python com suporte.
    >

+ [Ajuste de desempenho para R em SQL Server-métodos e resultados](../r/performance-case-study-r-services.md)

    Resume quais dados foram usados nos dois estudos de caso, como o desempenho foi testado e como as otimizações afetaram os resultados.
