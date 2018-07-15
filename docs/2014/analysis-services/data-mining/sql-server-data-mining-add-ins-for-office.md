---
title: SQL Server Data Mining Add-Ins para o Office | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c9021a19-2c19-4f0a-a293-5f7e0ac2524c
caps.latest.revision: 8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d8897cdb41d1d72806bf93335b13bf8c683cc31
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37273892"
---
# <a name="sql-server-data-mining-add-ins-for-office"></a>Suplementos de Mineração de Dados do SQL Server para Office
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Suplementos de Mineração de Dados do para Office é um conjunto de ferramentas leve para análise preditiva que permite a você usar dados no Excel para criar modelos analíticos para previsão, recomendação ou exploração.  
  
 Os assistentes e as ferramentas de gerenciamento de dados nos suplementos fornecem instruções passo a passo para essas tarefas de mineração de dados comuns:  
  
-   **Organizar e limpar seus dados antes da modelagem.** Use dados armazenados no Excel ou em qualquer fonte de dados do Excel. Você pode criar e salvar conexões para reutilizar fontes de dados, repetir experimentos ou treinar modelos novamente.  
  
-   **Gere perfis, amostras e prepare.** Muitos mineradores de dados experientes indicam que 70 a 90% de um projeto de mineração de dados é gasto na preparação dos dados. Os suplementos podem tornar essa tarefa mais rápida, fornecendo visualizações no Excel e nos assistentes que ajudarão você com essas tarefas comuns:  
  
    -   Crie o perfil dos dados e entenda suas características e distribuição.  
  
    -   Crie conjuntos de treinamento e teste através da amostragem aleatória ou da sobreamostragem.  
  
    -   Encontre exceções, e remova-as ou substitua-as.  
  
    -   Rotule os dados novamente para melhorar a qualidade da análise.  
  
-   **Analise padrões por meio de aprendizado supervisionado ou não supervisionado.** Clique nos assistentes amigáveis para realizar algumas das tarefas de mineração de dados mais conhecidas, incluindo a análise de clustering, a análise de cesta de compras e previsão.  
  
     Entre os algoritmos de aprendizado de máquina conhecidos incluídos nos suplementos, estão o Naïve Bayes, a regressão logística, o clustering, a série temporal e as redes neurais.  
  
     Se você não tiver experiência em mineração de dados, obtenha ajuda para criar consultas de previsão no assistente de **Consulta** .  
  
     Usuários avançados podem criar consultas DMX personalizadas com o **Editor de Consulta Avançada**do tipo "arrastar e soltar", ou automatizar previsões usando o VBA do Excel.  
  
-   **Documente e gerencie.** Depois de criar um conjunto de dados e de criar alguns modelos, documente seu trabalho e suas ideias gerando um resumo estatísticos dos dados e dos parâmetros de modelo.  
  
-   **Explorar e visualizar.** A mineração de dados não é uma atividade que pode ser completamente automatizada. É necessário explorar e compreender seus resultados para tomar uma medida significativa. Os suplementos ajudam você na exploração, fornecendo visualizadores interativos no Excel, modelos do Visio que permitem personalizar os diagramas e a capacidade de exportar gráficos e tabelas para o Excel para filtragem ou modificação adicionais.  
  
-   **Implante e integre.** Quando você criar um modelo útil, coloque-o em produção, usando as ferramentas de gerenciamento para exportar o modelo do servidor de avaliação para outra instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     Você também pode deixar o modelo no servidor onde o criou, mas atualize os dados de treinamento e execute previsões usando o Integration Services ou scripts DMX.  
  
     Os usuários avançados apreciarão a funcionalidade de **rastreamento** , que permite exibir as instruções XMLA e DMX enviadas para o servidor.  
  
## <a name="getting-started"></a>Introdução  
 Consulte estes tópicos para obter informações sobre as ferramentas e se preparar:  
  
-   [Cliente de mineração de dados para Excel &#40;suplementos de mineração de dados do SQL Server&#41;](../data-mining-client-for-excel-sql-server-data-mining-add-ins.md)  
  
-   [Ferramentas de Análise de Tabela para Excel](../table-analysis-tools-for-excel.md)  
  
-   [Formas de mineração de dados para o Visio](../data-mining-shapes-for-visio.md)  
  
-   [Conectar a um servidor de mineração de dados](../connect-to-a-data-mining-server.md)  
  
## <a name="support-and-requirements"></a>Suporte e requisitos  
 Os Suplementos de Mineração de Dados do SQL Server para Office são downloads gratuitos. Você deve ter uma das versões do Office a seguir já instaladas para usar essas ferramentas:  
  
-   Office 2010, versões de 32 bits ou 64 bits  
  
-   Office 2013, versões de 32 bits ou 64 bits  
  
> [!WARNING]  
>  Baixe a versão dos suplementos que corresponda à sua versão do Excel.  
  
 Os Suplementos de Mineração de Dados requerem uma conexão com uma das seguintes edições do SQL Server Analysis Services:  
  
-   Enterprise  
  
-   Business Intelligence  
  
-   Standard  
  
 Dependendo da edição do SQL Server Analysis Services ao você se conectará, alguns algoritmos avançados possivelmente não estarão disponíveis. Para obter informações, consulte [Recursos com suporte nas edições do SQL Server 2014](https://msdn.microsoft.com/en-us/library/cc645993.aspx).  
  
 Para obter ajuda adicional com a instalação, consulte esta página no Centro de Download: [http://www.microsoft.com/download/details.aspx?id=29061](http://www.microsoft.com/download/details.aspx?id=29061)  
  
  
