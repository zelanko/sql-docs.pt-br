---
title: Opções de implantação de modelo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cf1b17b4-47d5-4eba-83f9-fb0555806867
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 86c556fb4365df12d573294b0c937c36d91dffb3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52813328"
---
# <a name="model-deployment-options-master-data-services"></a>Opções de implantação de modelo (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], quando você implantar um arquivo de pacote de modelo, deverá decidir se deve implantar um modelo novo ou clonado ou atualizar um modelo clonado anteriormente.  
  
## <a name="workflows"></a>Fluxos de trabalho  
 Ao trabalhar com pacotes de modelo, há dois fluxos de trabalho primários.  
  
-   Crie um pacote de um modelo em um ambiente de teste e implante um clone do modelo para um ambiente de produção. Com o tempo, implante atualizações do ambiente de teste no ambiente de produção.  
  
-   Crie um pacote com base em um modelo e implante-o como um novo modelo no mesmo ambiente. Nesse caso, você deve atribuir um novo nome ao modelo.  
  
## <a name="options"></a>Opções  
 No banco de dados do MDS, cada objeto de modelo tem um identificador exclusivo (ID). Essas IDs são incluídas em pacotes de implantação de modelo. Quando você implanta o pacote, deve escolher o que fazer com essas IDs.  
  
 A tabela a seguir deve ajudar a determinar qual escolha fazer ao implantar um modelo usando o assistente de implantação de modelo de Administração do Sistema ou a ferramenta MDSModelDeploy.  
  
|Opção|Descrição|Observações|  
|------------|-----------------|-----------|  
|Nova|Crie um novo modelo com um nome exclusivo. São criados novos identificadores para todos os objetos de modelo.|Se você criar um novo modelo com novos identificadores, não poderá usar ferramentas de implantação de modelo para aplicar atualizações posteriormente ao modelo. Ao usar o assistente no aplicativo Web para implantar um pacote de modelo, você tem a opção de só criar um novo modelo se um modelo com o mesmo nome ou ID já existir.|  
|Clonar|Crie um novo modelo que seja um clone exato do modelo no pacote. Isso só funcionará se o modelo não existir (por nome ou identificador) no ambiente de destino. Use "clonar" quando você quiser ter o mesmo modelo em vários ambientes e atualizar o modelo clonado com o tempo.|Esse é o comportamento padrão do assistente no aplicativo Web. Se um modelo com o mesmo nome ou a ID já existir, você será solicitado a criar um novo modelo.|  
|Update|Atualize um modelo existente com o modelo no pacote. Os identificadores devem ser iguais nos dois modelos. Usado para atualizar um modelo que você clonou antes.|Você só pode atualizar modelos que foram clonados previamente. (Os nomes e IDs devem corresponder.)|  
  
## <a name="see-also"></a>Consulte Também  
 [Implantar um pacote de implantação de modelo usando MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)   
 [Implantar um pacote de implantação de modelo usando o Assistente](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)   
 [Implantando modelos &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md)  
  
  
