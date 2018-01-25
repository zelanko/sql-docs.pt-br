---
title: Tutoriais do SQL Server R | Microsoft Docs
ms.custom: SQL2016_New_Updated
ms.date: 08/29/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: R
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 5cd3c997dbcda9df95b62eb1c0c75967c77a3f83
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="sql-server-r-tutorials"></a>Tutoriais do SQL Server R

Este artigo fornece uma lista de tutoriais e exemplos que demonstram o uso de R com o SQL Server 2016 ou 2017 do SQL Server. Por meio desses exemplos e demonstrações, você aprenderá:

+ Como executar R do T-SQL
+ Quais são os contextos de computação local e remoto e como você pode executar código R usando o computador do SQL Server
+ Como encapsular o código R em um procedimento armazenado
+ Otimizando o código R para um ambiente de produção do SQL
+ Cenários do mundo real para incorporar o aprendizado de máquina em aplicativos

Para obter informações sobre os requisitos e a instalação, consulte [pré-requisitos](#bkmk_Prerequisites).

## <a name="bkmk_sqltutorials"></a>Tutoriais de R

A menos que indicado de outra forma, os tutoriais foram desenvolvidos para o SQL Server 2016 R Services e devem trabalhar nos serviços de aprendizado de máquina do SQL Server de 2017 sem alterações significativas.

Todos os tutoriais fazem uso extensivo de recursos no pacote RevoScaleR para o SQL Server contextos de computação.

+ [Mergulho profundo de ciência de dados com R e SQL Server](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)

  Saiba como usar as funções dos pacotes de RevoScaleR. Mover dados entre R e o SQL Server e o comutador de computação contextos de acordo com uma determinada tarefa. Criar modelos e gráficos e movê-los entre o ambiente de desenvolvimento e o servidor de banco de dados.

  **Público-alvo:** para cientistas de dados ou desenvolvedores que já estão familiarizados com a linguagem R, e que desejam saber mais sobre os pacotes de R aprimorados e as funções no Microsoft R pela Revolution Analytics.

  **Requisitos:** conhecimentos básicos sobre R. Acesso a um servidor com o SQL Server R Services ou serviços de aprendizado de máquina com R. Para obter ajuda da instalação, consulte [pré-requisitos](#bkmk_Prerequisites).

+ [Análise de R no banco de dados para desenvolvedores em SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md)

  Criar e implantar uma solução completa de R, usando apenas o [!INCLUDE[tsql](../../includes/tsql-md.md)] ferramentas.

  Se concentra na movimentação de uma solução em produção. Você aprenderá a encapsular o código R em um procedimento armazenado, salvar um modelo do R em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fazer chamadas parametrizadas para o modelo do R para previsão.

  **Público-alvo:** para desenvolvedores do SQL, os desenvolvedores de aplicativos ou profissionais SQL que oferecem suporte a soluções de R e quiser saber como implantar modelos de R para o SQL Server.

  **Requisitos:** nenhum ambiente R é necessária. Todo o código R é fornecido e você pode criar a solução completa usando apenas o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e inteligência de negócios familiares e ferramentas de desenvolvimento do SQL. No entanto, alguns dados de Conhecimento básico de R é útil.

  Você deve ter acesso a um SQL Server com a linguagem R instalado e habilitado. Para obter ajuda da instalação, consulte [pré-requisitos](#bkmk_Prerequisites).

+ [Início rápido: Usando o R em T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

  Este guia de início rápido aborda a sintaxe básica para usar o R no [!INCLUDE[tsql](../../includes/tsql-md.md)].

  Saiba como chamar o tempo de execução de R de T-SQL, encapsular funções R no código SQL e executar um procedimento armazenado que salva a saída de R e modelos de R em uma tabela do SQL.

  **Público-alvo:** para as pessoas que são novos para o recurso e para aprender os conceitos básicos de chamar o R de um procedimento armazenado.

  **Requisitos:** nenhum conhecimento de R ou SQL é necessário. No entanto, é necessário que o SQL Server Management Studio ou outro cliente que possa se conectar a um banco de dados e executar o T-SQL. É recomendável livre [extensão MSSQL para o código do Visual Studio](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) se você estiver familiarizado com consultas T-SQL.

  Você também deve ter acesso a um servidor com o SQL Server R Services ou serviços de aprendizado de máquina com R já está habilitado. Para obter ajuda da instalação, consulte [pré-requisitos](#bkmk_Prerequisites).

+ [Passo a passo de ponta a ponta sobre a ciência de dados](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

  Demonstra o processo de ciência de dados do início ao fim, como obter dados e salvá-lo para o SQL Server, analisar os dados com R e criar gráficos.

  Você aprenderá a mover elementos gráficos entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e R e engenharia de recurso de comparação no T-SQL com funções de R. Por fim, você aprenderá como usar o modelo de previsão em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a pontuação do lote e pontuação de única linha.

  **Público-alvo:** para pessoas que estão familiarizadas com R e ferramentas de desenvolvedor, como SQL Server Management Studio.

  **Requisitos:** você deve ter acesso a um ambiente de desenvolvimento de R e saber como executar comandos de R. Uso do PowerShell é necessário para baixar o conjunto de dados de táxi cidade de Nova York. Você deve ter acesso a um servidor com o SQL Server R Services ou serviços de aprendizado de máquina com R já está habilitado. Para obter ajuda da instalação, consulte [pré-requisitos](#bkmk_Prerequisites).

## <a name ="bkmk_samples"></a>Exemplos de produtos

Esses exemplos e demonstrações são fornecidas pela equipe de desenvolvimento do SQL Server para realçar as várias maneiras que você pode usar a análise incorporada em aplicativos do mundo real.

+ [Criar um modelo de previsão usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction)

  Saiba como uma empresa de aluguel ski pode usar o aprendizado de máquina para prever locações futuras, que ajuda a equipe e plano de negócios para atender às demandas futuras.

+ [Executar o cliente clustering usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/)

  Use o aprendizado sem supervisão aos clientes de segmento, com base em dados de vendas.

## <a name="bkmk_Prerequisites"></a>Pré-requisitos

Para usar esses tutoriais e exemplos, você deve instalar um dos seguintes produtos de servidor:

+ SQL Server 2016 R Services (no banco de dados)
  
  Dá suporte a R. Certifique-se instalar a recursos de aprendizado de máquina e, em seguida, habilitar scripts externos.

+ Serviços de aprendizado de máquina do SQL Server de 2017 (no banco de dados)
  
  Dá suporte a R ou Python. Você deve selecionar a recurso e o idioma para instalação de aprendizado de máquina e, em seguida, habilitar scripts externos.

Depois de executar a instalação do SQL Server, não se esqueça destas etapas importantes:

+ Habilitar o recurso de execução do script externo, executando`sp_configure 'external scripts enabled', 1`
+ Reiniciar o servidor
+ Verifique se o serviço que chama o tempo de execução externo tem as permissões necessárias
+ Verifique se o logon do SQL ou a conta de usuário do Windows tem as permissões necessárias para se conectar ao servidor, a leitura de dados e para criar os objetos de banco de dados necessários para o exemplo

Se você tiver problemas, consulte este artigo para alguns problemas comuns: [Solucionando problemas de serviços de aprendizado de máquina](../machine-learning-troubleshooting-faq.md)
