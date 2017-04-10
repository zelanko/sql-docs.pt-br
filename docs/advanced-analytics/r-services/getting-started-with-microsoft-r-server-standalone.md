---
title: "Introdu&#231;&#227;o ao servidor Microsoft R (aut&#244;nomo) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "r-server"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 16
---
# Introdu&#231;&#227;o ao servidor Microsoft R (aut&#244;nomo)
  O Microsoft R Server (autônomo) ajuda você a trazer a linguagem de software livre de R para a empresa, a fim de habilitar soluções analíticas de alto desempenho e integração com outros aplicativos de negócios.  
  
## O que é o Microsoft R Server?  
 O Microsoft R Server (autônomo) inclui os pacotes R avançados desenvolvidos pela Revolution Analytics e oferece suporte a conexões com diversas fonte de dados como Hadoop, Teradata e muito mais. Ao instalar o servidor autônomo, você pode criar um ambiente de servidor para executar trabalhos em R complexos e dimensionáveis.  
  
## Benefícios do uso do servidor Microsoft R (autônomo)  
 R é a linguagem de programação mais poderosa do mundo para computação estatística, aprendizado de máquina e gráficos e tem o suporte de uma vibrante comunidade global de usuários, desenvolvedores e colaboradores. Tradicionalmente, usar o R em uma configuração empresarial apresenta determinados desafios, especialmente à medida que aumenta o volume de dados ou quando você precisa implantar soluções em ambientes de produção. O Microsoft R Server resolve os problemas de implantação e operacionalização do código R.  
  
 Microsoft R Server pode ser instalado em qualquer computador com Windows e inclui todos os pacotes de R e ferramentas de conectividade para habilitar o contexto de computação remota e para oferecer suporte a soluções escalonáveis, paralelizáveis.  
  
 Microsoft R servidor (autônomo) oferece suporte a estes cenários:  
  
-   **Uso de um servidor central para operacionalizar soluções de R**  
  
     O servidor autônomo oferece a você desempenho em R aprimorado sem dependência do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cálculos complexos ou com uso intensivo de recursos podem ser executados no servidor em um computador laptop ou desenvolvimento que pode ter recursos limitados.  
  
     Você também pode centralizar os trabalhos, por exemplo, se você precisar pontuação em um modelo de previsão em produção, ou usar o servidor de R como um único ponto de contato para R plota e previsões usada no relatório. 
     
     Também recomendamos que você instale o servidor R (autônomo) no computador do SQL Server se você precisar executar R fora do contexto do SQL Server com frequência.
  
-   **Habilitando a exploração de dados mais eficiente e a modelagem com previsão**  
  
     O cientista de dados pode usar qualquer estação de trabalho cliente e qualquer ferramenta de desenvolvimento do R para criar soluções de R. Se a solução usar as APIs do pacote RevoScaleR, os cálculos poderão ser executados no servidor, que geralmente tem memória e potência de processamento muito maior. Assim, suas soluções podem trabalhar com conjuntos de dados muito maiores e aproveitar cálculos de vários segmentos, vários núcleos e vários processos.  
  
## Como posso obtê-lo?  
 Para obter instruções de instalação, consulte [Create a Standalone R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md). Todos os componentes podem ser instalados usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação.  
  
## Instalar ferramentas adicionais de R  
 Se você não tiver um ambiente de desenvolvimento preferido R, há muitas opções. Para obter detalhes, consulte [instalação ou configurar ferramentas R](../../advanced-analytics/r-services/setup-or-configure-r-tools.md). 
 
 Para conectar-se ao servidor do Microsoft R ou R serviços SQL Server em uma estação de trabalho de ciência de dados, recomendamos o livre [Microsoft R Client](http://aka.ms/rclient/download) (download).  
  
## Executar Script R no servidor Microsoft R (autônomo)  
 Depois de configurar os componentes de servidor e instalado IDE favorito R, você pode começar a desenvolver sua solução usando o pacote RevoScaleR. Essas APIs permitem que você envie comandos de R para um servidor remoto para execução.  
  
-   [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started): Iniciar explorando essa coleção de funções analíticas distribuíveis que fornecem alto desempenho e dimensionamento para soluções de R. Inclui versões paralelizáveis de muitos dos mais popular R pacotes, como clustering k-means, árvores de decisão e as florestas de decisão e ferramentas para manipulação de dados de modelagem. Você também pode usar o HPC para construir seu próprio algoritmo paralelo.  
    
-   [DeployR](https://msdn.microsoft.com/microsoft-r/deployr-about): essa estrutura opcional fornece as ferramentas para programadores de R usar o Java, JavaScript ou .net para integrar a análise de R de saída com um pacote de terceiros.  

Você pode trabalhar com dados em uma variedade de formatos, incluindo arquivos SAS, SPSS, Hadoop e texto. Você pode analisar dados no local ou mover seus dados com eficiência em seu ambiente de desenvolvimento local R usando o formato de arquivo .xdf.  
  
Para começar com o servidor de R, consulte este guia na biblioteca MSDN: [R Server - Introdução](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started)  
  
 Para obter informações sobre como usar os pacotes ScaleR, consulte [um Tutorial R em 25 funções](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#an-r-tutorial-in-25-functions-or-so)  
  
## Consulte também  
 [Introdução ao SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  