---
title: Implantar um pacote de implantação de modelo usando o MDSModelDeploy | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fb2a4df4-5e0d-4b34-818f-383dbde1b15c
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e99859dcdfcc2061622e955399b6d7bdac8bcbf4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007523"
---
# <a name="deploy-a-model-deployment-package-by-using-mdsmodeldeploy"></a>Implantar um pacote de implantação de modelo usando MDSModelDeploy
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], use a ferramenta MDSModelDeploy para implantar um pacote que contém:  
  
-   Somente objetos de modelo.  
  
-   Objetos de modelo e dados.  
  
 Se desejar implantar um pacote que contém apenas objetos de modelo, você poderá usar o assistente de implantação de modelo no aplicativo Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Para obter mais informações, consulte [Implantar um pacote de implantação de modelo usando o Assistente](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md).  
  
> [!IMPORTANT]  
>  Os pacotes podem ser implantados somente na edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] na qual eles foram criados. Isso significa que os pacotes criados no [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] não podem ser implantados no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] ou superior.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deverá ter permissão para acessar a área funcional **Administração do Sistema** no ambiente [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] de destino.  
  
-   Um pacote de implantação de modelo deverá existir. Para obter mais informações, consulte  [Criar um pacote de implantação de modelo usando MDSModelDeploy](../../2014/master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
-   Você deve ser um administrador no ambiente onde está implantando o modelo. Para obter mais informações, veja [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Se estiver atualizando um modelo com dados, a versão que está sendo implantada não poderá ser **Bloqueada** nem **Confirmada**.  
  
### <a name="to-deploy-a-model-deployment-package"></a>Para implantar um pacote de implantação de modelo  
  
1.  Determine se você está implantando um novo modelo, um clone de um modelo ou atualizando um modelo clonado previamente. Para obter mais informações, consulte [Opções de implantação de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-deployment-options-master-data-services.md).  
  
2.  Abra um prompt de comando e navegue para MDSModelDeploy.exe.  
  
    -   Se o MDS estiver instalado no local padrão, a ferramenta está disponível em *unidade*: \Program Files\Microsoft SQL Server\120\Master Data Services\Configuration\MDSModelDeploy.exe  
  
    -   Se o MDS não estiver instalado no local padrão, pesquise MDSModelDeploy.exe no comutador local.  
  
3.  Opcional. Exiba as opções e a ajuda.  
  
    -   Para exibir todas as opções disponíveis, digite `MDSModelDeploy` e pressione Enter.  
  
    -   Para exibir a ajuda para uma opção, digite o seguinte, em que *OptionName* é o nome da opção: `MDSModelDeploy help OptionName`.  
  
4.  Opcional. Se houver vários aplicativos Web, determine o nome do serviço no qual você implantará digitando este comando e pressionando Enter:  
  
    ```  
    MDSModelDeploy listservices  
    ```  
  
     Uma lista de valores é retornada, por exemplo, `MDS1, Default Web Site, MDS`. O primeiro valor nesta lista (neste caso, `MDS1`) é necessário para implantar o modelo.  
  
5.  Dependendo de se você está criando um modelo, clonando um modelo ou atualizando um modelo, no prompt de comando, digite o seguinte e pressione Enter.  
  
    -   Para criar um novo modelo:  
  
        ```  
        MDSModelDeploy deploynew –package PackageName -model ModelName -service ServiceName  
        ```  
  
    -   Para criar um clone de um modelo:  
  
        ```  
        MDSModelDeploy deployclone –package PackageName  
        ```  
  
    -   Para atualizar um modelo existente e seus dados:  
  
        ```  
        MDSModelDeploy deployupdate –package PackageName –version VersionName  
        ```  
  
    > [!IMPORTANT]  
    >  Se você usar a ferramenta MDSModelDeploy para atualizar um modelo existente e seus dados, e o pacote não contiver uma entidade, um atributo ou um membro que exista no modelo de destino, MDSModelDeploy não excluirá a entidade, o atributo ou o membro do modelo.  
  
     Em que *PackageName* é o nome do arquivo do pacote (.pkg), *ModelName* é o nome do novo modelo, *VersionName* é o nome da versão e *ServiceName* é o nome do serviço retornado na etapa anterior. Verifique se os nomes do modelo e da versão correspondem aos nomes exatos com diferenciação de maiúsculas e minúsculas.  
  
6.  Quando o pacote é implantado com êxito, uma mensagem é exibida informando que "A operação MDSModelDeploy foi concluída com êxito".  
  
 **Observações:**  
  
-   Se uma exibição de assinatura no pacote tiver o mesmo nome de uma exibição de assinatura em um modelo existente, a exibição é criada como *modelname.subscriptionviewname*. Se esse nome já estiver em uso, a exibição de assinatura não será criada.  
  
-   O processo de implantação tem quatro etapas:  
  
    1.  Os objetos de modelo são criados.  
  
    2.  As regras de negócio são criadas.  
  
    3.  As exibições de assinatura são criadas.  
  
    4.  Os dados mestre são preenchidos.  
  
-   Ao criar um modelo novo ou clonado, se o processo falhar durante alguma etapa, o modelo será excluído.  
  
     Na atualização de um modelo, se o processo falhar durante as três primeiras etapas, ele não continuará; no entanto, as alterações já feitas não serão revertidas. Se o processo falhar na etapa 4, os membros que podem ser atualizados serão atualizados.  
  
## <a name="next-steps"></a>Próximas etapas  
 Metadados definidos pelo usuário, atributos de arquivo e permissões de usuário e de grupo não estão incluídos em pacotes de implantação de modelo. Depois de implantar um modelo, você deve atualizar esses objetos manualmente. Para obter mais informações, consulte:  
  
-   [Adicionar metadados &#40;Master Data Services&#41;](../../2014/master-data-services/add-metadata-master-data-services.md)  
  
-   [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Implantando modelos &#40;Master Data Services&#41;](../../2014/master-data-services/deploying-models-master-data-services.md)  
  
  