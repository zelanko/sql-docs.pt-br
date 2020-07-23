---
title: 'Etapa 3: Modificar o valor de configuração da propriedade Directory | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5a609b6c5edc5518904432cc199e5e624fb114ad
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916842"
---
# <a name="lesson-5-3-modify-the-directory-property-configuration-value"></a>Lição 5-3: Modificar o valor de configuração da propriedade Directory

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



Nesta tarefa, você modificará a definição de configuração, armazenada no arquivo **SSISTutorial.dtsConfig** para definir a propriedade **Value** da variável no nível de pacote `User::varFolderName`. A variável atualiza a propriedade **Directory** do contêiner Loop Foreach. O valor modificado aponta para a pasta **Novos Dados de Exemplo** criada na tarefa anterior. Depois de modificar a definição de configuração e executar o pacote, a propriedade **Directory** é atualizada usando a variável no arquivo de configuração. Anteriormente, o valor da propriedade **Directory** fazia parte do pacote.  
  
## <a name="modify-the-configuration-setting-of-the-directory-property"></a>Modificar a definição de configuração da propriedade Directory  
  
1.  No Bloco de notas ou em qualquer outro editor de texto, localize e abra o arquivo de configuração **SSISTutorial.dtsConfig** criado usando o Assistente para Configuração de Pacote na tarefa anterior.  
  
2.  Altere o valor do elemento **ConfiguredValue** para corresponder ao caminho da pasta **Novos Dados de Exemplo** criada na tarefa anterior. Não coloque o caminho entre aspas. Se a pasta **Novos Dados de Exemplo** estiver no nível raiz da unidade (por exemplo, **C:\\** ), o XML atualizado deverá ser semelhante à seguinte amostra:  
  
    ```
    <?xml version="1.0"?>
    <DTSConfiguration>
      <DTSConfigurationHeading>
        <DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFEE1D3FA}" GeneratedDate="6/10/2018 8:16:50 AM"/>
      </DTSConfigurationHeading>
      <Configuration ConfiguredType="Property" 
          Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String">
        <ConfiguredValue>C:\New Sample Data</ConfiguredValue>
      </Configuration>
    </DTSConfiguration>  
    ```

    Evidentemente, as informações do cabeçalho, **GeneratedBy**, **GeneratedFromPackageID** e **GeneratedDate** são diferentes em seu arquivo. O elemento a ser anotado é o elemento **Configuration** . A propriedade **Value** da variável, `User::varFolderName`, agora contém **C:\New Sample Data**.  
  
3.  Salve a alteração e feche o editor de textos.  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa  
[Etapa 4: Testar o pacote da Lição 5](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
  
