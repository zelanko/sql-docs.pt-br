---
title: 'Etapa 3: modificar o valor de configuração da propriedade de diretório | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8675de132f15b723b6d7d2a651d31ef7b3e85063
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304266"
---
# <a name="step-3-modifying-the-directory-property-configuration-value"></a>Etapa 3: Modificando o valor de configuração da propriedade de diretório
  Nesta tarefa, você modificará a definição de configuração, armazenada no arquivo SSISTutorial.dtsConfig, da propriedade Value da variável no nível de pacote `User::varFolderName`. A variável atualiza a propriedade Directory do contêiner Loop Foreach. O valor modificado apontará para o `New Sample Data` pasta que você criou na tarefa anterior. Depois de modificar a definição de configuração e executar o pacote, a propriedade Directory será atualizada pela variável, usando o valor populado do arquivo de configuração, em vez do valor de diretório originalmente configurado no pacote.  
  
### <a name="to-modify-the-configuration-setting-of-the-directory-property"></a>Para modificar a definição de configuração da propriedade de diretório  
  
1.  No Bloco de notas ou em qualquer outro editor de texto, localize e abra o arquivo de configuração SSISTutorial.dts criado usando o Assistente para Configuração de Pacote na tarefa anterior.  
  
2.  Altere o valor da **ConfiguredValue** elemento para coincidir com o caminho da `New Sample Data` pasta que você criou na tarefa anterior. Não coloque o caminho entre aspas. Se o `New Sample Data` pasta está no nível raiz da unidade (por exemplo, c\\), o XML atualizado deverá ser semelhante ao exemplo a seguir:  
  
     `<?xml version="1.0"?><DTSConfiguration><DTSConfigurationHeading><DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFA61D3FA}" GeneratedDate="6/10/2012 8:16:50 AM"/></DTSConfigurationHeading><Configuration ConfiguredType="Property" Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String"><ConfiguredValue></ConfiguredValue></Configuration></DTSConfiguration>`  
  
     As informações de cabeçalho `GeneratedBy`, `GeneratedFromPackageID`, e **GeneratedDate** serão diferentes em seu arquivo, é claro. O elemento a ser anotado é `Configuration`. A propriedade `Value` da variável, `User::varFolderName`, agora contém C:\Novos Dados de Exemplo.  
  
3.  Salve a alteração e feche o editor de textos.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 4: Testando o pacote de tutorial da Lição 5](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
