---
title: "Serviços de aprendizado de máquina do SQL Server | Microsoft Docs"
ms.date: 12/04/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: "38"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: 99f42ddd8d906799c02b05d856597db7c44a8eb6
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="sql-server-machine-learning-services"></a>Serviços de SQL Server Machine Learning

Serviços do aprendizado de máquina 2017 SQL Server (anteriormente SQL Server 2016 R Services) fornece uma plataforma para desenvolvimento e implantação de aplicativos inteligentes que descobrem novas informações. Como o aprendizado de máquina está integrado com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode manter a análise próxima aos dados e eliminar os custos e os riscos de segurança associados à movimentação de dados.
  
+ No SQL Server 2016, você pode facilmente desenvolver e implantar soluções baseadas na linguagem R popular para ciência de dados. 

    Os recursos incluem o [Microsoft R](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) bibliotecas, que fornecem novas escalabilidade e desempenho para soluções de R e algoritmos de última geração no [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package).
+ No SQL Server de 2017, você pode usar para desenvolver e operacionalizar soluções de ciência de dados R e Python. 

    O [revoscalepy](../python/what-is-revoscalepy.md) biblioteca para Python fornece contextos de computação remota e escalabilidade comparável às RevoScaleR.

Melhor desempenho, segurança e capacidade de gerenciamento de suporte do SQL Server para cargas de trabalho de aprendizado de máquina por meio de um conjunto abrangente de ferramentas e tecnologias. Você pode implantar o R ou soluções usando conveniente Python, metodologia SQL familiar e ferramentas. Usar apenas o [!INCLUDE[tsql](../../includes/tsql-md.md)] para chamar os tempos de execução de R ou Python de seus aplicativos de produção, para criar modelos ou recuperar os elementos visuais. Se você já treinar um modelo, você pode gerar previsões dele usando somente T-SQL, por meio de [pontuação nativo](../sql-native-scoring.md).

## <a name="machine-learning-in-sql-server-2017"></a>No SQL Server 2017 de aprendizado de máquina

+ Instalar **serviços de aprendizado de máquina (no banco de dados)** durante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação para habilitar a execução segura de scripts de R ou Python no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador.
  
    Quando você seleciona esse recurso, as extensões são instaladas no mecanismo de banco de dados para permitir a execução de código escrito em R ou Python. Um novo serviço é criado, o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], para gerenciar as comunicações entre os tempos de execução externas e a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.
  
+ Instalar **aprendizado de máquina do Microsoft Server (autônomo)** em um computador separado, se você não precisa usar o SQL Server como o contexto de computação. Servidor de aprendizado de máquina inclui os mesmos componentes de aprendizado de máquina, além da capacidade de executar tarefas de aprendizado de máquina escalonável e distribuído como um serviço web.
  
+ Instalar [Microsoft R cliente](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) em computadores remotos para desenvolver soluções que podem ser implantados para o SQL Server ou ao servidor de aprendizado de máquina no Windows, Linux ou Hadoop.

## <a name="machine-learning-in-sql-server-2016"></a>No SQL Server 2016 de aprendizado de máquina

+ Instalar **R Services (no banco de dados)** durante a instalação do SQL Server 2016 para permitir a execução segura de scripts de R no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador.
  
    Quando você seleciona esse recurso, você recebe a capacidade de executar script R usando o SQL Server como o contexto de computação, ou para executar o script de R em um procedimento armazenado.
  
+ Instalar **Microsoft R Server (autônomo)** da instalação do SQL Server 2016, para instalar os componentes de R em um computador separado que você pode usar para desenvolver ou implantar soluções de R.

## <a name="how-to-get-started"></a>Como começar

Instalação do SQL Server fornece duas opções:

+ Instalação de recursos de análise no banco de dados que é integrado com o SQL Server, ou
+ Instale a versão autônoma do servidor de aprendizado de máquina (ou Microsoft R Server) que dá suporte ao aprendizado de máquina em escala sem uma instância do SQL Server.

Se você precisa executar seu código R [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], usando procedimentos armazenados ou usando a instância do SQL Server como o contexto de computação, você deve instalar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] conforme descrito no [guia de instalação](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md). Essa opção fornece segurança máxima de dados e a integração com ferramentas do SQL Server.

Aprendizado de máquina do Microsoft Server (autônomo) é uma opção separada projetada para usar o [Microsoft R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) e [relacionados bibliotecas Python](../python/what-is-revoscalepy.md) em um computador com Windows que não esteja executando o SQL Server. Essa opção requer uma licença do Enterprise Edition do SQL Server.
    
É recomendável que você instala o servidor de aprendizado de máquina (autônomo) em um laptop ou outro computador remoto usado para desenvolvimento e use esse computador para criar e testar soluções de aprendizado de máquina que podem ser implantadas facilmente a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é executando serviços de aprendizado de máquina \(no banco de dados\) ou outro contexto de computação tem suporte.
  
Você também pode usar o **mrsdeploy** pacote instalado com o servidor de aprendizado de máquina para publicar e distribuir os trabalhos de R e Python como um serviço web.

## <a name="additional-resources"></a>Recursos adicionais

+ [Guia de Introdução com serviços de aprendizado de máquina do SQL Server](../../advanced-analytics/r/getting-started-with-sql-server-r-services.md)
 
    Descreve os cenários comuns de usos do R com o SQL Server

+ [Configurar serviços de aprendizado de máquina do SQL Server ou R Services no banco de dados](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

    Instalar componentes de banco de dados associado e R como parte da instalação do SQL Server
  
+ [Tutoriais do SQL Server e do R](../../advanced-analytics/tutorials/sql-server-r-tutorials.md)

    Saiba como criar fontes de dados do SQL Server no seu código R e como usar contextos de computação remota. Outros tutoriais destinados a desenvolvedores SQL demonstram como treinar e implantar um modelo de R no SQL Server.
