---
title: "Ferramentas e aplicativos usados no Analysis Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 0ddb3b7a-7464-4d04-8659-11cb2e4cf3c3
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 17
---
# Ferramentas e aplicativos usados no Analysis Services
  Encontre as ferramentas e os aplicativos que você precisa criar modelos do Analysis Services e gerenciar os bancos de dados associados em uma instância do Analysis Services.  
  
## Designers de modelos do Analysis Services  
 Modelos multidimensionais e de tabela são criados por meio de modelos de projeto em uma solução criada no shell do Visual Studio. O modelo de projeto possibilita aos designers criar tabelas, relacionamentos, cubos, dimensões e funções que compõem uma solução do Analysis Services. O shell fornece o espaço de trabalho visual, as páginas de propriedade e a estrutura de comando na qual o projeto é criado. O designer do modelo que fornece o shell e os modelos é um download gratuito na Web.  
  
 Os modelos têm uma configuração de nível de compatibilidade que determina a disponibilidade do recursos e em qual versão do Analysis Services executar o modelo.  A especificação de determinado nível de compatibilidade é determinado em parte pelo designer do modelo.  
  
 Modelos de tabela usando a funcionalidade mais recente no SQL Server 2016, como arquivos BIM no formato JSON tabular e filtragem cruzada bidirecional, devem ser criados no nível de compatibilidade 1200, na versão do SQL Server Data Tools para Visual Studio 2015 que é entregue simultaneamente com o SQL Server 2016 (consulte abaixo para o link de download).  
  
 Se você precisar de um nível de compatibilidade mais baixo, talvez porque você deseja implantar um modelo em uma versão anterior do Analysis Services, ainda pode usar o designer de modelo SSDT para Visual Studio 2015. Versões mais recentes da ferramenta de oferecem suporte à criação de qualquer tipo de modelo (em tabela ou multidimensional) em qualquer nível de compatibilidade necessário. Não é necessário manter ferramentas anteriores para criar ou editar um modelo mais antigo.  
  
### Baixe o designer do modelo  
 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], antes conhecido como SSDT-BI (SQL Server Data Tools para Business Intelligence) e, antes disso, como BIDS (Business Intelligence Development Studio) é usado para criar modelos do Analysis Services.  
  
||  
|-|  
|**[Baixar o SSDT para Visual Studio 2015](https://msdn.microsoft.com/mt429383)**|  
  
 O uso do SQL Server Data Tools para Visual Studio 2015 tem prioridade sobre as versões anteriores do designer. Ele contém modelos de projeto para todos os tipos de conteúdo do SQL Server, incluindo banco de dados relacional, modelos do Analysis Services, relatórios do Reporting Services e pacotes do Integration Services.  
  
 O SSDT é executado no shell do Visual Studio 2015. Se você já tiver o Visual Studio 2015, a instalação do SSDT adiciona apenas os modelos do projeto. Se você não tiver o Visual Studio 2015, o shell e modelos serão instalados.  
  
 Se você tiver uma versão anterior do SSDT-BI ou BIDS instalado no computador, a versão mais recente será instalada lado a lado da versão anterior.  
  
 Depois de instalar o SSDT, você deve ver os modelos de Business Intelligence na caixa de diálogo Novo Projeto.  
  
 ![Novos modelos de projeto no SSDT](../analysis-services/media/ssdt-biprojects.png "Novos modelos de projeto no SSDT")  
  
## Ferramentas administrativas  
  
### Baixar o SQL Server Management Studio  
 O Management Studio é a principal ferramenta de administração para todos os recursos do SQL Server, incluindo o Analysis Services. Agora é um download separado.  
  
||  
|-|  
|**[Baixar o SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)**|  
  
 No SQL Server 2016, o Management Studio inclui eventos estendidos (xEvents) para o Analysis Services, fornecendo uma alternativa leve para rastreamentos do SQL Server Profiler usado para monitorar atividades e diagnosticar problemas do servidor. Consulte [Monitorar o Analysis Services com Eventos Estendidos do SQL Server](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md).  
  
### SQL Server Profiler  
 Embora oficialmente preterido em favor do xEvents, o SQL Server Profiler fornece uma abordagem familiar para conexões de monitoramento, execução da consulta MDX, e outras operações do servidor. O SQL Server Profiler é instalado por padrão. Você pode encontrá-lo entre os aplicativos do SQL Server nos aplicativos do Windows Server 2012.  
  
### PowerShell  
 Você pode usar os comandos do PowerShell para realizar muitas tarefas administrativas. Consulte [Scripts do PowerShell no Analysis Services](../analysis-services/instances/powershell-scripting-in-analysis-services.md) para obter mais informações.  
  
### Ferramentas da comunidade e de terceiros  
 Verifique a [página de codeplex do Analysis Services](http://sqlsrvanalysissrvcs.codeplex.com/) para ver exemplos de código da comunidade. Os [fóruns](http://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices) podem ser úteis ao buscar recomendações de ferramentas de terceiros com suporte para o Analysis Services.  
  
## Consulte também  
 [Nível de compatibilidade de um banco de dados multidimensional &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Nível de compatibilidade para modelos de tabela no Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  