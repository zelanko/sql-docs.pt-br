---
title: 'Etapa 3: modificar o valor de configuração da propriedade de diretório | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cb83ac5bb1b811c23b782b01167c437e9b989518
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62767358"
---
# <a name="step-3-modifying-the-directory-property-configuration-value"></a>Etapa 3: Modificar o valor de configuração da propriedade de diretório
  Nesta tarefa, você modificará a definição de configuração, armazenada no arquivo SSISTutorial.dtsConfig, da propriedade Value da variável no nível de pacote `User::varFolderName`. A variável atualiza a propriedade Directory do contêiner Loop Foreach. O valor modificado apontará para a `New Sample Data` pasta que você criou na tarefa anterior. Depois de modificar a definição de configuração e executar o pacote, a propriedade Directory será atualizada pela variável, usando o valor populado do arquivo de configuração, em vez do valor de diretório originalmente configurado no pacote.  
  
### <a name="to-modify-the-configuration-setting-of-the-directory-property"></a>Para modificar a definição de configuração da propriedade de diretório  
  
1.  No Bloco de notas ou em qualquer outro editor de texto, localize e abra o arquivo de configuração SSISTutorial.dts criado usando o Assistente para Configuração de Pacote na tarefa anterior.  
  
2.  Altere o valor do elemento **configurable** para corresponder ao caminho da `New Sample Data` pasta que você criou na tarefa anterior. Não coloque o caminho entre aspas. Se a `New Sample Data` pasta estiver no nível raiz da unidade (por exemplo, C:\\), o XML atualizado deverá ser semelhante ao seguinte exemplo:  
  
     `<?xml version="1.0"?><DTSConfiguration><DTSConfigurationHeading><DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFA61D3FA}" GeneratedDate="6/10/2012 8:16:50 AM"/></DTSConfigurationHeading><Configuration ConfiguredType="Property" Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String"><ConfiguredValue></ConfiguredValue></Configuration></DTSConfiguration>`  
  
     As informações de cabeçalho `GeneratedBy`, `GeneratedFromPackageID`, e **GeneratedDate** serão diferentes em seu arquivo, é claro. O elemento a ser anotado é `Configuration`. A propriedade `Value` da variável, `User::varFolderName`, agora contém C:\Novos Dados de Exemplo.  
  
3.  Salve a alteração e feche o editor de textos.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 4: Testar o pacote de tutorial da Lição 5](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
