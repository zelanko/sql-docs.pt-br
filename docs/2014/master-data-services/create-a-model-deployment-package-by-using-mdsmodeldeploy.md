---
title: Criar um pacote de implantação de modelo usando o MDSModelDeploy | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c2687e39-dc20-494f-a707-2aa29f4c329e
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 399c6743f302bd616fe0a232527fcb5fc0af62ab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120814"
---
# <a name="create-a-model-deployment-package-by-using-mdsmodeldeploy"></a>Criar um pacote de implantação de modelo usando o MDSModelDeploy
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], use a ferramenta MDSModelDeploy para criar um pacote. Dependendo dos comandos especificados, o pacote poderá conter:  
  
-   Somente objetos de modelo.  
  
-   Objetos de modelo e dados.  
  
 Se desejar implantar um pacote que contém apenas objetos de modelo, você poderá usar o assistente de implantação de modelo no aplicativo Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Para obter mais informações, consulte [Criar um pacote de implantação de modelo usando o assistente](../../2014/master-data-services/create-a-model-deployment-package-by-using-the-wizard.md).  
> [!NOTE]  
> Esta versão da ferramenta MDSModelDeploy não é possível usar mais de gigabytes (GB) de memória. Quando você criar ou implantar modelos grandes usando **objetos e dados de modelo** opção, você pode enfrentar erros de "Fluxo era muito longo" ou "memória insuficiente". Para resolver esse problema, use o MDS de preparação para implantar os dados. ou atualize para o MDS 2016 ou posterior, que inclui a versão atualizada da ferramenta MDSModelDeploy.
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
1.  As permissões básicas exigidas para executar a ferramenta MDSModelDeploy são as seguintes:  
  
    -   A mesma permissão do Windows como o MDS Configuration Manager (administrador do Windows)  
  
    -   Permissão DBA no banco de dados do MDS.  
  
2.  As permissões necessárias para criar o pacote usando a ferramenta MDSModelDeploy são as seguintes:  
  
    -   Permissão de administrador de modelo do MDS no modelo de dados.  
  
    -   Permissão de função do Gerenciamento de Integração do MDS.  
  
3.  As permissões necessárias para implantar um modelo usando a ferramenta MDSModelDeploy são as seguintes:  
  
    -   Permissão de função do MDS Explorer  
  
    -   Permissão de função do Gerenciamento de Integração do MDS  
  
    -   Permissão de função da Administração do Sistema do MDS.  
  
4.  As permissões necessárias para listar modelos usando a ferramenta MDSModelDeploy são as seguintes:  
  
    -   Permissão de função do MDS Explorer  
  
    -   A permissão de administrador de modelo do MDS no modelo de dados para ver o modelo na lista.  
  
 Deve existir um modelo como base para o pacote que será criado. Para obter mais informações, consulte [Criar um modelo &#40;Master Data Services&#41;](create-a-model-master-data-services.md).  
  
 Para obter mais informações, veja [Administrators &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md).  
  
### <a name="to-create-a-model-deployment-package-by-using-mdsmodeldeploy"></a>Para criar um pacote de implantação de modelo usando o MDSModelDeploy  
  
1.  Abra um prompt de comando.  
  
2.  Navegue até o local de MDSModelDeploy.exe.  
  
    -   Se o MDS estiver instalado na local padrão, o arquivo estará em *drive*: \Arquivos de Programas\Microsoft SQL Server\120\Master Data Services\Configuration.  
  
    -   Se o MDS não estiver instalado no local padrão, pesquise MDSModelDeploy.exe no comutador local.  
  
3.  Opcional. Exiba as opções e a ajuda.  
  
    -   Para exibir todas as opções disponíveis, digite `MDSModelDeploy` e pressione Enter.  
  
    -   Para exibir a ajuda para uma opção, digite o seguinte, em que *OptionName* é o nome da opção: `MDSModelDeploy help OptionName`.  
  
4.  Opcional. Se houver vários aplicativos Web, determine o nome do serviço no qual você implantará digitando este comando e pressionando Enter:  
  
    ```  
    MDSModelDeploy listservices  
    ```  
  
     Uma lista de valores é retornada, por exemplo, `MDS1, Default Web Site, MDS`. O primeiro valor nesta lista (neste caso, `MDS1`) é necessário para implantar o modelo.  
  
5.  Para criar um pacote que contém objetos de modelo e dados, digite o seguinte, onde *ModelName*, *VersionName*, *ServiceName*e *PackageName* são os nomes do modelo, da versão, do serviço e do arquivo de saída .pkg respectivamente:  
  
    ```  
    MDSModelDeploy createpackage -model ModelName -version VersionName -service ServiceName -package PackageName -includedata  
    ```  
  
     Para incluir dados, não use as opções `-version` e `-includedata` .  
  
6.  Pressione Enter. Quando o pacote é criado com êxito, uma mensagem é exibida informando que "A operação MDSModelDeploy foi concluída com êxito".  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   [Implantar um pacote de implantação de modelo usando MDSModelDeploy](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
## <a name="see-also"></a>Consulte também  
 [Opções de implantação de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-deployment-options-master-data-services.md)   
 [Implantando modelos &#40;Master Data Services&#41;](../../2014/master-data-services/deploying-models-master-data-services.md)  
  
  