---
title: "Etapa 3: Modificando o valor de configura&#231;&#227;o da propriedade de diret&#243;rio | Microsoft Docs"
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
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Etapa 3: Modificando o valor de configura&#231;&#227;o da propriedade de diret&#243;rio
Nesta tarefa, você modificará a definição de configuração, armazenada no arquivo SSISTutorial.dtsConfig, da propriedade Value da variável no nível de pacote `User::varFolderName`. A variável atualiza a propriedade Directory do contêiner Loop Foreach. O valor modificado apontará para a pasta **Novos Dados de Exemplo** criada na tarefa anterior. Depois de modificar a definição de configuração e executar o pacote, a propriedade Directory será atualizada pela variável, usando o valor populado do arquivo de configuração, em vez do valor de diretório originalmente configurado no pacote.  
  
### Para modificar a definição de configuração da propriedade de diretório  
  
1.  No Bloco de notas ou em qualquer outro editor de texto, localize e abra o arquivo de configuração SSISTutorial.dts criado usando o Assistente para Configuração de Pacote na tarefa anterior.  
  
2.  Altere o valor do elemento **ConfiguredValue** para corresponder ao caminho da pasta **Novos Dados de Exemplo** criada na tarefa anterior. Não coloque o caminho entre aspas. Se a pasta **Novos Dados de Exemplo** estiver no nível raiz da unidade (por exemplo, C:\\), o XML atualizado deverá ser semelhante à seguinte amostra:  
  
    `<?xml version="1.0"?><DTSConfiguration><DTSConfigurationHeading><DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFA61D3FA}" GeneratedDate="6/10/2012 8:16:50 AM"/></DTSConfigurationHeading><Configuration ConfiguredType="Property" Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String"><ConfiguredValue></ConfiguredValue></Configuration></DTSConfiguration>`  
  
    Evidentemente, as informações do cabeçalho, **GeneratedBy**, **GeneratedFromPackageID** e **GeneratedDate** serão diferentes em seu arquivo. O elemento a ser anotado é o elemento **Configuration**. A propriedade **Value** da variável, `User::varFolderName`, agora contém C:\Novos Dados de Exemplo.  
  
3.  Salve a alteração e feche o editor de textos.  
  
## Próxima tarefa da lição  
[Etapa 4: Testando o pacote de tutorial da Lição 5](../integration-services/step-4-testing-the-lesson-5-tutorial-package.md)  
  
  
  
