---
title: 'Etapa 2: Verificando o pacote de implantação | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 6c13f5c9-c75e-4e52-94dc-2d2db2c578fe
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 163df99c54ed323d1039d50c69e812cb4c1d2286
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53368778"
---
# <a name="step-2-verifying-the-deployment-bundle"></a>Etapa 2: Verificando o pacote de implantação
  Na lição 1, você criou o projeto do Tutorial de Implantação e adicionou pacotes e arquivos auxiliares ao projeto; na tarefa anterior você compilou um utilitário de implantação para o projeto.  
  
 Nesta tarefa, você verificará o conteúdo do pacote de implantação. O pacote de implantação é a pasta que você copiará para o computador de destino e usará para instalar os pacotes. Se você tiver usado o valor padrão – bin\Deployment – como a localização do utilitário de implantação, o pacote de implantação será a pasta Bin\Deployment dentro da pasta Tutorial de Implantação no projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
### <a name="to-verify-the-content-of-deployment-bundle"></a>Para verificar o conteúdo do pacote de implantação  
  
1.  Localize a pasta bin\Deployment em seu computador.  
  
2.  Verifique se os seguintes arquivos estão presentes:  
  
    -   DataTransfer.dtsx  
  
    -   datatransferconfig.dtsconfig  
  
    -   Deployment Tutorial.SSISDeploymentManifest  
  
    -   LoadXMLData.dtsx  
  
    -   loadxmldataconfig.dtsconfig  
  
    -   NewCustomers.txt  
  
    -   orders.xml  
  
    -   orders.xsd  
  
    -   Readme.txt  
  
3.  Clique com o botão direito do mouse em Deployment Tutorial.SSISDeploymentManifest, aponte para **Abrir Com**e clique em **Internet Explorer**. Você também pode abrir o arquivo em um editor de textos como o Bloco de Notas. O código XML do arquivo deve ser o seguinte:  
  
     `<?xml version="1.0"?><DTSDeploymentManifest GeneratedBy="Domain\UserName" GeneratedFromProjectName="Deployment Tutorial" GeneratedDate="2006-02-24T13:29:02.6537669-08:00" AllowConfigurationChanges="true"><Package>DataTransfer.dtsx</Package><Package>LoadXMLData.dtsx</Package><ConfigurationFile>datatransferconfig.dtsconfig</ConfigurationFile><ConfigurationFile>loadxmldataconfig.dtsconfig</ConfigurationFile><MiscellaneousFile>Readme.txt</MiscellaneousFile><MiscellaneousFile>orders.xml</MiscellaneousFile><MiscellaneousFile>NewCustomers.txt</MiscellaneousFile><MiscellaneousFile>orders.xsd</MiscellaneousFile></DTSDeploymentManifest>`  
  
4.  Verificar se o valor da `AllowConfigurationChanges` atributo é **verdadeiro** e o XML inclui um `Package` elemento para cada um dos dois pacotes, um `MiscellaneousFile` elemento para cada um dos quatro arquivos que não são de pacote e um `ConfigurationFile` elemento para cada um dos dois arquivos de configuração XML.  
  
5.  Saia do Internet Explorer ou do editor de textos.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 3: Instalando pacotes](../integration-services/lesson-3-install-ssis-package.md)  
  
![Ícone do Integration Services (pequeno)](media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
  
