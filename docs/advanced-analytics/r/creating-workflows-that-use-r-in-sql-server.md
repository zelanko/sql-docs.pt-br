---
title: Criar inteligência de negócios (BI) de fluxos de trabalho com R - serviços do SQL Server Machine Learning
description: Suportam a cenários de integração de combinação de business intelligence (BI) e a linguagem R no SQL Server e SQL Server Integration Services (SSIS).
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 32dfb3317cb790c19289ab02362bf8ee765e5259
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432729"
---
# <a name="creating-bi-workflows-with-r"></a>Criando fluxos de trabalho de BI com o R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Um banco de dados relacional é uma tecnologia altamente otimizada para fornecer soluções escalonáveis para processamento, armazenamento e consulta de dados de transações.

Em contraste, tradicionalmente soluções de R geralmente dependem de importação de dados de várias fontes, geralmente no formato CSV, para executar modelagem e exploração de dados adicional. Essas práticas não são apenas ineficientes, mas inseguras.

Este artigo descreve os cenários de integração para o R com o SQL Server que evitar armadilhas comuns e a riscos de segurança que pode ocorrer se as soluções de aprendizado de máquina desenvolvidas fora do banco de dados.

Ele também descreve exemplos de como os aplicativos de business intelligence, especialmente do Integration Services e Reporting Services, podem interagir com o código de R e consumir dados ou elementos gráficos gerados por R.

Aplica-se a: SQL Server 2016 R Services, serviços de aprendizado de máquina do SQL Server 2017

## <a name="bring-compute-power-to-the-data"></a>Traga o poder de computação para os dados

Uma meta de design de chave de integração de aprendizado de máquina com o SQL Server foi colocar a análise próxima aos dados. Isso oferece várias vantagens:

+ Segurança de dados. Trazendo o mais próximo do R para a fonte de dados evita a movimentação de dados desperdiçadora ou insegura.

+ Velocidade. Os bancos de dados são otimizados para operações baseadas em conjunto. As recentes inovações em bancos de dados como tabelas na memória tornam resumos e agregações muito mais e são um complemento perfeito para ciência de dados.

+ Facilidade de integração e implantação. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é o ponto central de operações para muitas outras tarefas de gerenciamento de dados e aplicativos. Usando dados que residem no banco de dados ou no warehouse de relatórios, verifique se que os dados usados por soluções de aprendizado de máquina são consistente e atualizado. 

+ Eficiência na nuvem e locais. Em vez de processar dados no R, é possível contar com pipelines de dados corporativos incluindo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e o Azure Data Factory. Comunicar resultados ou análises é fácil com o Power BI ou o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

Usando a combinação certa de SQL e R para processamento de dados e tarefas analíticas diferentes, desenvolvedores e cientistas de dados podem ser mais produtivos.

## <a name="use-integration-services-for-data-transformation-and-automation"></a>Usar o Integration Services para dados de transformação e automação

Fluxos de trabalho de ciência de dados são altamente iterativos e envolvem muita transformação de dados, incluindo dimensionamento, agregações, cálculo de probabilidades, renomeação e mesclagem de atributos. Os cientistas de dados estão acostumados a fazer muitas dessas tarefas em R, Python ou outra linguagem; contudo, a execução desses fluxos de trabalho em dados empresariais requer integração perfeita com processos e ferramentas de ETL.

Como o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] permite que você execute operações complexas em R por meio do Transact-SQL e de procedimentos armazenados, é possível integrar tarefas específicas de R a processos de ETL existentes sem o mínimo trabalho de novo desenvolvimento. Em vez disso, executar uma cadeia de tarefas intensivo de memória em R, preparação de dados pode ser otimizada usando as ferramentas mais eficientes, incluindo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e [!INCLUDE[tsql](../../includes/tsql-md.md)]. 

Aqui estão algumas ideias de como você pode automatizar o processamento de dados e pipelines de modelagem usando [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ Use [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tarefas para criar recursos de dados necessários no banco de dados SQL
+ Usar ramificação condicional para alternar o contexto de computação para trabalhos em R
+ Executar trabalhos do R que geram seus próprios dados no banco de dados e compartilhar dados com aplicativos
+ Ao usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], carregar o script R salvo em uma variável de texto e executá-lo no SQL Server

### <a name="examples"></a>Exemplos

[Operacionalizar seu projeto de aprendizado de máquina usando o SQL Server 2016 SSIS e o R Services](https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/)  

Esta postagem de blog demonstra as técnicas básicas para manipular o código R usando [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]: 

+ Chamar o R usando a tarefa Executar SQL, para gerar dados e salvá-los em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

+ Usar um procedimento armazenado para treinar um modelo R e armazená-lo no banco de dados

+ Executar a pontuação no modelo usando a tarefa Script e a tarefa Executar SQL

##  <a name="bkmk_ssrs"></a> Usar o Reporting Services para visualização

Embora R possa criar gráficos e efeitos visuais interessantes, não é bem integrado com fontes de dados externas, significando que cada de gráfico tem de ser produzido individualmente. O compartilhamento também pode ser difícil.

Usando o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], é possível executar operações complexas em R por meio de procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)], que podem ser facilmente consumidos por uma variedade de ferramentas de relatório empresariais, incluindo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o Power BI.

+ Visualizar objetos gráficos retornados de um script de R usando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]
+ Usar a tabela no Power BI

### <a name="examples"></a>Exemplos

[R Graphics Device para Microsoft Reporting Services (SSRS)](https://rgraphicsdevice.codeplex.com/)

Este projeto CodePlex fornece o código para ajudar você a criar um item de relatório personalizado que renderiza a saída de gráficos de R como uma imagem que pode ser usada nos relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  Usando o item de relatório personalizado, é possível:

+ Publicar gráficos e plotagens criados usando o R Graphics Device para painéis do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]

+ Passar parâmetros [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para gráficos de R

> [!NOTE]
> Para este exemplo, o código que dá suporte ao R Graphics Device para Reporting Services deve ser instalado no servidor do Reporting Services, bem como no Visual Studio. Também são necessárias a compilação e a configuração manuais.
