---
title: "Introdução ao Microsoft R Server (autônomo) | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: "21"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 5ff9e6bc9b6cebb4602683180737aa78e7deb6e3
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="getting-started-with-machine-learning-server-standalone"></a>Guia de Introdução ao servidor de aprendizado de máquina (autônomo)
 
No SQL Server 2016, Microsoft R Server (autônomo) ajudou a trazer a linguagem R de software livre popular para a empresa, para habilitar a integração com outros aplicativos de negócios e soluções de análise de alto desempenho.  

No SQL Server de 2017, o nome foi alterado para o servidor de aprendizado de máquina (autônomo) para refletir a adição de suporte para a linguagem Python. Ambas as versões estão disponíveis gratuitamente para os usuários do Enterprise Edition ou do Software Assurance.

Este artigo fornece uma visão geral de como você pode usar o servidor de aprendizado de máquina (ou R Server) e como começar com exemplos e instalação.

## <a name="why-use-a-standalone-server-for-machine-learning"></a>Por que usar um servidor autônomo para aprendizado de máquina

Se você não precisa integrar seu soluções com dados do SQL Server de aprendizado de máquina, o servidor de aprendizado de máquina oferece o mesmo suporte distribuído e dimensionável para R e Python e Além disso oferece suporte à implantação de soluções para o Hadoop, Spark ou Linux.

Servidor de aprendizado de máquina também inclui modelos previamente treinados para análise de imagem e análise de sentimento, você poderá usar imediatamente em aplicativos.

Os recursos de operacionalização do servidor de aprendizado de máquina dão suporte a implantar e distribuir as soluções de R e Python usando serviços web, com a execução remota, topologias em cluster Spark e Hadoop MapReduce e suportam para Windows ou Linux.

**SQL Server 2016**

+ Instale o Microsoft R Server (autônomo) de instalação do SQL Server 2016.

    Esta opção cria um servidor autônomo que é totalmente independente do R Services (no banco de dados). Esta versão dá suporte a R somente. Instalação de um servidor autônomo é incluída em sua política de suporte do SQL Server Enterprise Edition. Para obter mais informações, consulte [Criar um R Server autônomo](../../advanced-analytics/r/create-a-standalone-r-server.md).

+ Instale o R Server usando o Windows installer separado.

    O instalador cria uma nova instância do Microsoft R Server que usa a política de suporte da Microsoft modernos ciclo de vida de Software. Você também pode instalar o R Server para Linux, Cloudera, Teradata e Hadoop.
    
    Para obter mais informações, consulte [instalar o R Server 9.1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

**SQL Server 2017**

+ Instale servidor de aprendizado de máquina (autônomo) de instalação do SQL Server 2017. 

    Esta opção cria um servidor autônomo para dar suporte a operacionalização da máquina de aprendizado em R, Python ou ambos. Instalação de um servidor autônomo é incluída em sua política de suporte do SQL Server Enterprise Edition. Para obter mais informações, consulte [Criar um R Server autônomo](../../advanced-analytics/r/create-a-standalone-r-server.md).  

+ Use o novo instalador do Windows autônoma.

    Esse método de instalação cria uma nova instância do servidor de aprendizado de máquina que usa a política de suporte da Microsoft modernos ciclo de vida de Software. Você também pode instalar o servidor de aprendizado de máquina no Linux, Hadoop ou no Spark sem custo adicional.
    
    Para obter mais informações, consulte [instalar Machine Learning Server para Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

**Atualizar um servidor existente**

+ Se você tiver um servidor existente ou a instância que você deseja atualizar, baixe e execute o instalador baseado no Windows para obter as atualizações. 

    Para obter mais informações, consulte [usando SqlBindR para atualizar uma instância](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="start-using-machine-learning-server"></a>Começar a usar o servidor de aprendizado de máquina

 Depois de configurar os componentes de servidor e configurado o IDE para usar os binários do servidor de aprendizado de máquina, você pode começar a desenvolver sua solução usando as novas APIs, como o RevoScaleR e revoscalepy, MicrosoftML e olapR.
    
Para começar, consulte estas guias:

+ [Modelos de solução](https://docs.microsoft.com/machine-learning-server/r/sample-solutions)

    Exemplos dessas políticas são soluções que demonstram como aplicar o aprendizado de máquina em setores específicos. São cenários atuais no varejo, financeiros, saúde e marketing.

+ [Explorar o R e ScaleR em 25 funções](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): explorar este conjunto de funções analíticas distribuíveis que fornecem alto desempenho e escalabilidade para soluções de R. Inclui versões paralelizáveis de muitos dos pacotes mais populares de modelagem do R, como clustering k-means, árvores de decisão e florestas de decisão, bem como as ferramentas para a manipulação de dados.

- [MicrosoftML](https://msdn.microsoft.com/library/mt790482.aspx)

    O pacote de MicrosoftML é um conjunto de novos algoritmos e as transformações desenvolvidas na Microsoft rápido e escalonável de aprendizado de máquina. Você pode usá-lo em R ou Python. Para obter mais informações, consulte [MicrosoftML para Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) e [MicrosoftML para R](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package).

## <a name="see-also"></a>Consulte também

[Introdução aos serviços de aprendizado de máquina do SQL Server](../../advanced-analytics/r/getting-started-with-sql-server-r-services.md)