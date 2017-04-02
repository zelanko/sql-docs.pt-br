---
title: "Etapa 4: Testando o pacote de tutorial da Li&#231;&#227;o 5 | Microsoft Docs"
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
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Etapa 4: Testando o pacote de tutorial da Li&#231;&#227;o 5
Em tempo de execução, o pacote irá obter o valor da propriedade **Directory** de uma variável atualizada em tempo de execução, ao invés de utilizar o nome original de diretório que foi especificado quando você criou o pacote. O valor da variável é populado pelo arquivo SSISTutorial.dtsConfig.  
  
Para verificar se, em tempo de execução, o pacote atualizou corretamente o Diretório com o novo valor, simplesmente execute o pacote. Devido a serem copiados apenas três arquivos de dados de exemplo para o novo diretório, o fluxo de dados irá executar apenas três vezes ao invés de interagir com 14 arquivos da pasta original.  
  
## Verificando o layout do pacote  
Antes de testar o pacote, deve-se verificar se os fluxos de controle e de dados do pacote da Lição 5 contêm os objetos mostrados nos diagramas a seguir. O fluxo de controle deve ser idêntico ao fluxo de controle da Lição 4. O fluxo de dados deve ser idêntico ao fluxo de dados da lição 4.  
  
**Fluxo de Controle**  
  
![Control flow in package](../integration-services/media/task4lesson2control.gif "Control flow in package")  
  
**Fluxo de Dados**  
  
![Data flow in package](../integration-services/media/task9lesson1data.gif "Data flow in package")  
  
### Para testar o pacote de tutorial da Lição 5  
  
1.  No menu **Depurar** , clique em **Iniciar Depuração**.  
  
2.  Terminada a execução do pacote, no menu **Depurar** , clique em **Parar Depuração**.  
  
## Próxima lição  
[Lição 6: Usando parâmetros com o modelo de implantação de projetos no SSIS](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
  
