---
title: "Introdução ao SQL Server de aprendizado de máquina | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 12/07/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 5b28a663-effe-41f6-9bda-eda95f0c6943
caps.latest.revision: "34"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c114d320e71a93ffc6614ae6cfb1b535af2510e1
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="getting-started-with-sql-server-machine-learning"></a>Introdução ao SQL Server de aprendizado de máquina

Serviços de aprendizado de máquina no SQL Server foi projetado para oferecer suporte a tarefas de ciência de dados sem expor seus dados a riscos de segurança ou unnecesarily movimentação de dados.

+ No SQL Server 2016, você pode trabalhar com suas ferramentas favoritas de R, mas dimensionar sua análise bilhões de registros ao mesmo tempo, aumentando o desempenho. Integrando o aprendizado de máquina do SQL Server também significa que você pode colocar o código R em produção sem a necessidade de código novamente.

+ SQL Server 2017 adiciona suporte para o código Python, usando a mesma estrutura de extensibilidade.

Este tópico descreve os cenários principais para usar o R ou Python no banco de dados e fornece recursos para ajudá-lo a se familiarizar com suas próprias soluções.

Aplica-se a: SQL Server 2016 R Services, SQL Server 2017 Services (no banco de dados) de aprendizado de máquina

> [!NOTE]
> SQL Server 2016 inclui suporte somente para a linguagem R. Suporte para linguagem Python requer o SQL Server de 2017 CTP 2.0.

## <a name="step-1-set-up-sql-server-machine-learning-services"></a>Etapa 1. Configurar serviços de aprendizado de máquina do SQL Server

1. Execute a instalação do SQL Server e instale pelo menos uma instância do mecanismo de banco de dados do SQL Server.
2. Adicione o recurso que dá suporte à execução dos tempos de execução externos.
3. No SQL Server 2016, R é adicionado por padrão. No SQL Server de 2017, você deve selecionar um idioma a ser adicionado. Você pode selecionar R ou Python ou permitir.
4. Quando a instalação é feita, executar algumas etapas adicionais para habilitar a execução do script externo e reinicie o servidor.

**Recursos**

+ [Configurar o SQL Server com o aprendizado de máquina](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

> [!TIP]  
> Precisa criar um servidor para trabalhos em R, mas não precisa do SQL Server? Experimente o [Microsoft R Server](https://msdn.microsoft.com/library/mt674874.aspx).  

## <a name="step-2-develop-your-r-or-python-solutions"></a>Etapa 2. Desenvolver seu R ou soluções do Python

Os cientistas de dados geralmente usam R ou Python em seu próprios estação de trabalho do laptop ou de desenvolvimento, para explorar dados e criar e ajustar modelos de previsão, até que um bom modelo de previsão seja obtido. 

Com os serviços de aprendizado de máquina no SQL Server, não é necessário para alterar esse processo. Após a conclusão da instalação, você pode executar código R ou Python em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] localmente ou remotamente:

![rsql_keyscenario2](media/rsql-keyscenario2.png) 

+ **Usar o IDE preferir**. Os componentes do cliente do[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] fornece aos cientistas de dados todas as ferramentas necessárias para testes e para desenvolvimento. Essas ferramentas incluem o tempo de execução de R, a biblioteca de kernel de matemática da Intel para melhorar o desempenho de operações padrão de R e um conjunto avançados de pacotes de R que dão suporte à execução do código R no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

+ **Trabalhar remotamente ou localmente**. Os cientistas de dados podem se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e transferir os dados para o cliente para análise local, como de costume. No entanto, uma solução melhor é usar as APIs **ScaleR** para enviar por push os cálculos para o computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , evitando uma movimentação de dados cara e insegura.

+ **Inserir scripts R ou Python [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos armazenados**. Quando seu código é completamente otimizado, coloque-o em um procedimento armazenado para evitar a movimentação desnecessária de dados e otimizar as tarefas de processamento de dados.


**Recursos**

+ Instalar [ferramentas R para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation) ou RStudio.  

## <a name="step-3-optimize"></a>Etapa 3. Otimizar

Quando o modelo estiver pronto para dimensionar nos dados da empresa, o cientista de dados geralmente funcionará com o desenvolvedor do DBA ou SQL para otimizar os processos, como:

+ Engenharia de recursos
+ Ingestão de dados e transformação de dados
+ Pontuação

Tradicionalmente, os cientistas de dados usando R teve problemas com desempenho e escala, especialmente ao usar o conjunto de dados grande. Isso ocorre porque a implementação de tempo de execução comum é de thread único e pode acomodar apenas os conjuntos de dados que cabem na memória disponível no computador local. Integração com serviços de aprendizado de máquina do SQl Server fornece vários recursos para melhorar o desempenho, com mais dados:

+ **RevoScaleR**.: pacote R este contém implementações de algumas das funções R mais populares, remodeladas para oferecer paralelismo e escalabilidade. O pacote também inclui funções que aumentam ainda mais o desempenho e a escala enviando por push cálculos para o computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que geralmente tem muito mais memória e eficiência computacional.

+ **revoscalepy**. Essa biblioteca do Python, novo e está disponível apenas no SQL Server de 2017 CTP 2.0, implementa funções mais populares em RevoScaleR, como contextos de computação remota e processamento distribuído de muitos algoritmos que oferecem suporte.

+ Escolha a melhor linguagem para a tarefa.  R é melhor para cálculos estatísticos que são difíceis de implementar usando SQL. Para operações baseadas em conjunto de dados, aproveite a potência do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para alcançar desempenho máximo. Use o mecanismo de banco de dados na memória para cálculos muito rápidos sobre colunas.

**Recursos**

+ [Estudo de caso de desempenho](../../advanced-analytics/r/performance-case-study-r-services.md)
+ [R e otimização de dados](../../advanced-analytics/r/r-and-data-optimization-r-services.md)


## <a name="step-4-deploy-and-consume"></a>Etapa 4. Implantar e consumir

Depois que o script R ou o modelo estiver pronto para uso em produção, um desenvolvedor de banco de dados pode incorporar o código ou o modelo em um procedimento armazenado, para que o código de R ou Python salvo pode ser chamado de um aplicativo. Armazenar e executar código R do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] traz muitos benefícios: você pode usar a interface conveniente do [!INCLUDE[tsql](../../includes/tsql-md.md)] e todos os cálculos ocorrem no banco de dados, evitando movimentação desnecessária de dados.

![rsql_keyscenario1](media/rsql-keyscenario1.png)

+ **Seguro e extensível**. O[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa uma nova arquitetura de extensibilidade que mantém o mecanismo de banco de dados seguro e isola as sessões de R. Você também tem controle sobre os usuários que podem executar scripts R, e você pode especificar quais bancos de dados podem ser acessados pelo código R. Você pode controlar a quantidade de recursos alocados ao tempo de execução de R, para evitar que cálculos muito intensos prejudiquem o desempenho geral do servidor.

+ **Agendamento e auditoria**. Quando os trabalhos de script externo são executados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode controlar e auditoria de dados usado por cientistas de dados. Você também pode agendar trabalhos e criar fluxos de trabalho que contém scripts de R ou Python externos, exatamente como você pode agendar qualquer trabalho T-SQL ou procedimento armazenado.

Para aproveitar as vantagens dos recursos de segurança e gerenciamento de recursos no SQL Server, o processo de implantação pode incluir estas tarefas:

+ Convertendo seu código R em uma função que pode ser executados de forma ideal em um procedimento armazenado
+ Configurando a segurança e o bloqueio usados por uma tarefa específica de pacotes
+ Habilitar o controle de recursos

**Recursos**

+ [Governança de recursos para R](../../advanced-analytics/r/resource-governance-for-r-services.md)
+ [Gerenciamento de pacotes de R para o SQL Server](../../advanced-analytics/r/r-package-management-for-sql-server-r-services.md)

## <a name="quick-starts"></a>Início rápido

Leia este passo a passo para entender o fluxo de trabalho completo de exploração de dados para criar um modelo e implantá-la para o SQL Server.

+ [Passo a passo de ponta a ponta sobre a ciência de dados](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Saiba como usar o pacote RevoScaleR para análise escalonável e de alto desempenho.

+ [Aprofundamento da ciência de dados: usando os pacotes RevoScaleR](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)

Especialmente para o desenvolvedor de dados – todo o código de R fornecidas! Aprenda a incorporar R em procedimentos armazenados do SQL para criar ou treinar modelos e obter previsões de um modelo armazenado.

+ [Análise avançada no banco de dados para desenvolvedores do SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Aprenda a sintaxe para chamar R de um procedimento armazenado.

+ [Usando código do R no Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

## <a name="solutions"></a>Soluções

Para obter mais exemplos, incluindo setor = modelos de solução específica, consulte [tutoriais de aprendizado de máquina do SQL Server](../tutorials/machine-learning-services-tutorials.md).
