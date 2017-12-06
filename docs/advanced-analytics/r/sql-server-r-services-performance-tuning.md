---
title: Ajuste de desempenho do SQL Server R Services | Microsoft Docs
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf6f3b7d-f9f9-4e45-b0d1-07850b53e0c5
caps.latest.revision: "20"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a1f3db839e51a85151141149d7a2778ce8cd423b
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="performance-tuning-for-r-in-sql-server"></a>Ajuste de desempenho de R no SQL Server

Este artigo é o primeiro em uma série de quatro artigos que descrevem a otimização de desempenho para serviços de R, com base em dois estudos de caso:

- Testes de desempenho realizados pela equipe de desenvolvimento do produto para validar o perfil de desempenho de soluções de R

- Otimização de desempenho, a equipe de ciência de dados da Microsoft para um cenário de aprendizado de máquina específico geralmente solicitado pelos clientes.

O objetivo desta série é fornecer orientação sobre os tipos de técnicas que são mais úteis para executar trabalhos de R no SQL Server de ajuste de desempenho.

+ Este tópico (primeiro) fornece uma visão geral da arquitetura do e alguns problemas comuns ao otimizar para tarefas de ciência de dados.
+ O segundo artigo abrange otimizações do SQL Server e o hardware específico.
+ O terceiro artigo abrange as otimizações no código de R e recursos para operacionalização.
+ O quarto artigo descreve os métodos de teste em detalhes e os resultados de relatórios e conclusões.

**Aplica-se a:** R Services do SQL Server 2016, SQL Server 2017 serviços de aprendizado de máquina

## <a name="performance-goals-and-targeted-scenarios"></a>Metas de desempenho e cenários de destino

O recurso Serviços de R foi introduzido no SQL Server 2016 para permitir a execução de scripts de R pelo SQL Server. Quando você usar esse recurso, o tempo de execução de R opera em um processo separado do mecanismo de banco de dados, mas troca dados de forma segura com o mecanismo de banco de dados, usando os recursos do servidor e serviços que interagem com o SQL Server, como a barra inicial confiável.

No SQL Server de 2017, o suporte foi anunciado para executar scripts Python usando a mesma arquitetura, com um idioma adicional a seguir no futuro.

À medida que aumenta o número de versões com suporte e de idioma, é importante que o administrador de banco de dados e o arquiteto de banco de dados estão cientes do potencial para contenção de recursos devido a trabalhos de aprendizado de máquina e que eles sejam capazes de configurar o servidor para dar suporte novas cargas de trabalho. Embora manter análise próxima aos dados elimina movimentos de dados insegura, ele também move cargas de trabalho analíticas desativar o laptop do cientista de dados e volta para o servidor que hospeda os dados.

Otimização de desempenho para o aprendizado de máquina claramente não é uma proposta única. As seguintes tarefas comuns podem ter perfis de desempenho muito diferentes:

- Tarefas de treinamento: Criando e treinar um modelo de regressão versus treinar uma rede neural
- Engenharia de recurso usando o R e extração de um recurso usando o T-SQL
- Pontuação em linhas únicas ou lotes pequenos, versus em massa usando entradas de tabela de pontuação
- Executando a pontuação em R e implantar modelos em produção no servidor SQL em procedimentos armazenados
- Modificar o código de R para minimizar a transferência de dados ou remover transformações de dados cara
- Habilitar automatizada de teste e treinamento de modelos

Como a escolha de técnicas de otimização depende de qual tarefa é essencial para seu aplicativo ou caso de uso, os estudos de caso abrangem dicas de desempenho geral e a orientação sobre como otimizar para um cenário específico, a otimização para a pontuação do lote.

+ **Opções de otimização individuais no SQL Server**

    O primeiro estudo de caso de desempenho, vários testes foram executados em um único conjunto de dados usando um único tipo de modelo. O algoritmo rxLinMod RevoscaleR foi usado para criar um modelo e criar pontuações dele, mas o código, bem como as tabelas de dados subjacentes sistematicamente foram alteradas para testar o impacto de cada alteração.

    Por exemplo, em uma execução de teste, o código R foi alterado para que uma comparação foi feita entre usando uma função de transformação versus previamente os recursos de computação e, em seguida, carregar recursos de uma tabela de engenharia de recurso. Em outra execução de teste, desempenho de treinamento de modelo foi comparado entre usando uma tabela indexada padrão versus dados em uma tabela com vários tipos de compactação ou novos tipos de índice.

+ **Otimização para um cenário específico de pontuação de alto volume**

    A tarefa de aprendizado de máquina no segundo estudo de caso envolve muitas currículos enviados para várias posições e Localizando mais adequados para cada cargo de trabalho de processamento. O próprio modelo de aprendizado de máquina é formulado como um problema de classificação binária: ele tem uma descrição do trabalho e retomar como entrada e gera a probabilidade para cada par de resume-job. Como o objetivo é encontrar a melhor correspondência, um limite de probabilidade definidas pelo usuário é usado para filtrar ainda mais e obter apenas as correspondências BOM.

    Para esta solução, o principal objetivo era obter baixa latência durante a pontuação. No entanto, essa tarefa é dispendiosa, mesmo durante o processo de pontuação, porque cada novo trabalho deve ser comparado com milhões de retomada em um período razoável. Além disso, a etapa de engenharia de recurso produz mais de 2.000 recursos por continuar ou trabalho e é um gargalo de desempenho significativa.

Sugerimos que você examine todos os resultados da primeira estudo de caso para determinar quais técnicas são aplicáveis à sua solução e avaliar o impacto deles.

Em seguida, examine os resultados de pontuação estudo de caso de otimização para ver como o autor aplicadas técnicas diferentes e o servidor para dar suporte a uma determinada carga de trabalho otimizado.

## <a name="performance-optimization-process"></a>Processo de otimização do desempenho

Configuração e ajuste de desempenho requer a criação de uma base sólida, no qual as otimizações de camada projetadas para cargas de trabalho específicas:

- Escolha um servidor apropriado para análise do host. Normalmente, um relatório secundário, data warehouse ou outro servidor que já é usado para outros relatórios ou a análise é preferencial. No entanto, em uma solução de processamento transacional analíticos (HTAP), os dados operacionais podem ser usados como entrada para R para pontuação rápida.

- Configurar a instância do SQL Server para operações de mecanismo de banco de dados de saldo e R ou execução em níveis apropriados do script de Python. Isso pode incluir a alteração de padrões do SQL Server para memória e uso de CPU, NUMA e as configurações de afinidade do processador e criação de grupos de recursos.

- Otimize o computador do servidor para dar suporte a uso eficiente de scripts externos. Isso pode incluir a aumentar o número de contas usadas para a execução do script externo, permitindo o gerenciamento de pacote, e atribuir usuários relacionados a funções de segurança.

- Aplicando otimizações específicas para o armazenamento de dados e transferência no SQL Server, incluindo a indexação e estratégias de estatísticas, design de consulta e otimização de consulta e o design de tabelas que são usados para aprendizado de máquina. Você também pode analisar as fontes de dados e dados de métodos de transporte ou modificar os processos ETL para otimizar a extração do recurso.

- Ajuste o modelo analítico para evitar ineficiências. O escopo das otimizações de possíveis dependem da complexidade do seu código R e os pacotes e os dados que você está usando. As principais tarefas incluem eliminar transformações de dados cara ou descarregar dados preparação ou recurso engenharia tarefas de R ou Python para processos de ETL ou SQL. Você também pode refatorar scripts, eliminar instalações de pacote na linha, divida o código R em procedimentos separados para treinamento, pontuação e avaliação ou simplificar o código para trabalhar com mais eficiência um procedimento armazenado.

## <a name="articles-in-this-series"></a>Esta série de artigos

+ [Ajuste de desempenho de R no SQL Server - hardware](..\r\sql-server-configuration-r-services.md)

    Fornece orientação para configurar o hardware que [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] está instalado e para configurar a instância do SQL Server para oferecer melhor suporte a scripts externos. Isso é especialmente útil para **os administradores de banco de dados**.

+ [Ajuste de desempenho de R no SQL Server - código e dados de otimização](..\r\r-and-data-optimization-r-services.md)

    Fornece dicas específicas sobre como otimizar o script externo para evitar problemas conhecidos. É mais útil **cientistas de dados**.

    [!NOTE]
    > Embora muitas das informações nesta seção se aplica a R em geral, algumas informações são específicas para as funções de análise RevoScaleR. Diretrizes de desempenho detalhada não estão disponível para **revoscalepy** e outras bibliotecas de Python de suporte.

+ [Ajuste de desempenho de R no SQL Server - métodos e resultados](..\r\performance-case-study-r-services.md)

    Resume os dados que foram usado dois estudos de caso, como o desempenho foi testado e como as otimizações afetados resultados.
