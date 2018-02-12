---
title: Criando fluxos de trabalho de BI com R | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 04/18/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 34c3b1c2-97db-4cea-b287-c7f4fe4ecc1b
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: dcfd7571f5dd555e6654eb65c4bbb7852f82feff
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
---
# <a name="creating-bi-workflows-with-r"></a>Criando fluxos de trabalho de BI com R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Um banco de dados relacional é uma tecnologia altamente otimizada para fornecer soluções escalonáveis para processamento, armazenamento e consulta de dados de transações.

Por outro lado, tradicionalmente soluções R têm geralmente baseava-se à importação de dados de várias fontes, geralmente no formato CSV, para executar modelagem e exploração de dados adicional. Essas práticas não são apenas ineficientes, mas inseguras.

Este tópico descreve os cenários de integração de R com o SQL Server que evitar armadilhas comuns e a riscos de segurança que pode ocorrer se as soluções de aprendizado de máquina são desenvolvidas fora do banco de dados.

Ele também descreve exemplos de como os aplicativos de business intelligence, especialmente Integration Services e serviços Reportng, podem interagir com código de R e consumir dados ou gráficos gerados por R.

Aplica-se a: SQL Server 2016 R Services, SQL Server 2017 serviços de aprendizado de máquina

## <a name="bring-compute-power-to-the-data"></a>Colocar a capacidade de computação para os dados

Uma meta de design principais da integração do aprendizado de máquina com o SQL Server foi traga análise próxima aos dados. Isso oferece várias vantagens:

+ Segurança de dados. Trazer R mais próximo para a fonte de dados evita a movimentação de dados de uso ou não.

+ Velocidade. Os bancos de dados são otimizados para operações baseadas em conjunto. As recentes inovações em bancos de dados como tabelas na memória tornam resumos e agregações muito mais e são um complemento perfeito para ciência de dados.

+ Facilidade de implantação e integração. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]é o ponto central de operações para muitas outras tarefas de gerenciamento de dados e aplicativos. Usando dados que residem no banco de dados ou warehouse de relatórios, você garantir que os dados usados por soluções de aprendizado de máquina são consistente e atualizado. 

+ Eficiência em nuvem e local. Em vez de processar dados no R, é possível contar com pipelines de dados corporativos incluindo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e o Azure Data Factory. Comunicar resultados ou análises é fácil com o Power BI ou o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

Usando a combinação certa de SQL e R para processamento de dados e tarefas analíticas diferentes, desenvolvedores e cientistas de dados podem ser mais produtivos.

## <a name="use-integration-services-for-data-transformation-and-automation"></a>Usar os serviços de integração de dados transformação e automação

Fluxos de trabalho de ciência de dados são altamente iterativos e envolvem muita transformação de dados, incluindo dimensionamento, agregações, cálculo de probabilidades, renomeação e mesclagem de atributos. Os cientistas de dados estão acostumados a fazer muitas dessas tarefas em R, Python ou outra linguagem; contudo, a execução desses fluxos de trabalho em dados empresariais requer integração perfeita com processos e ferramentas de ETL.

Como o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] permite que você execute operações complexas em R por meio do Transact-SQL e de procedimentos armazenados, é possível integrar tarefas específicas de R a processos de ETL existentes sem o mínimo trabalho de novo desenvolvimento. Em vez de executar uma cadeia de tarefas de uso intensivo de memória em R, a preparação de dados pode ser otimizada usando as ferramentas mais eficientes, incluindo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e [!INCLUDE[tsql](../../includes/tsql-md.md)]. 

Aqui estão alguns ideass de como você pode automatizar seus dados de processamento de um dmodeling pipelines usando [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ Use [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tarefas para criar recursos de dados necessários no banco de dados SQL
+ Usar ramificação condicional para alternar o contexto de computação para trabalhos em R
+ Executar trabalhos em R que geram seus próprios dados no banco de dados e compartilhar dados com aplicativos
+ Ao usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], carregar o script R salvo em uma variável de texto e executá-lo no SQL Server

### <a name="examples"></a>Exemplos

[Operacionalizar seu projeto de aprendizado de máquina usando o SQL Server 2016 SSIS e o R Services](https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/)  

Esta postagem de blog demonstra técnicas básicas de manipulação de código R usando [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]: 

+ Chamar o R usando a tarefa Executar SQL, para gerar dados e salvá-lo em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

+ Usar um procedimento armazenado para treinar um modelo R e armazená-lo no banco de dados

+ Executar a pontuação no modelo usando a tarefa Script e a tarefa Executar SQL

##  <a name="bkmk_ssrs"></a>Usar o Reporting Services para visualização

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
> Para este exemplo, o código que oferece suporte ao dispositivo de gráficos de R para o Reporting Services deve ser instalado no servidor do Reporting Services, bem como no Visual Studio. Também são necessárias a compilação e a configuração manuais.
