---
title: "Etapa 9: Testando o pacote de tutorial da Li&#231;&#227;o 1 | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Etapa 9: Testando o pacote de tutorial da Li&#231;&#227;o 1
Nesta lição, você executou as seguintes tarefas:  
  
-   Criou um novo projeto do [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
-   Configurou os gerenciadores de conexões que o pacote precisa para estabelecer conexão com os dados de origem e de destino.  
  
-   Adicionou um fluxo de dados que usa os dados de uma origem de arquivo simples, desenvolve as transformações Pesquisa necessárias sobre os dados e configura os dados para o destino.  
  
Seu pacote está completo agora! Está na hora de testá-lo.  
  
## Verificando o layout do pacote  
Antes de testar o pacote, é recomendável verificar se os fluxos de controle e de dados do pacote da Lição 1 contêm os objetos mostrados nos diagramas a seguir.  
  
**Fluxo de Controle**  
  
![Control flow in package](../integration-services/media/task9lesson1control.gif "Control flow in package")  
  
**Fluxo de Dados**  
  
![Data flow in package](../integration-services/media/task9lesson1data.gif "Data flow in package")  
  
### Para executar o pacote de tutorial da Lição 1  
  
1.  No menu **Depurar** , clique em **Iniciar Depuração**.  
  
    O pacote será executado, resultando em 1097 linhas adicionadas à tabela de fatos **FactCurrency** no **AdventureWorksDW2012**.  
  
2.  Terminada a execução do pacote, no menu **Depurar** , clique em **Parar Depuração**.  
  
## Próxima lição  
[Lição 2: Adicionando um loop com o SSIS](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## Consulte também  
[Execução de projetos e pacotes](../Topic/Execution%20of%20Projects%20and%20Packages.md)  
  
  
  
