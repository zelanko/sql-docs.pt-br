---
title: Editar um pacote de implantação de modelo
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 6b0fdb7d-83dd-4392-9011-4ae642c471f1
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 12cacedc8f195a965b7632760976008ba4b422b0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73728223"
---
# <a name="edit-a-model-deployment-package"></a>Editar um pacote de implantação de modelo

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Este tópico descreve como implantar partes selecionadas de um modelo em MDS, e não um modelo inteiro. Para fazer isso, edite um pacote de modelo MDS usando o Editor de Pacote de Modelo.  
  
 O assistente de Editor de Pacote de Modelo permite que você selecione as entidades específicas, hierarquias derivadas, exibições de assinatura e regras de negócio em um modelo a ser incluído em um pacote MDS e, posteriormente, implante-as. É possível omitir essas partes do modelo que você não deseja implantar. Quando você seleciona uma entidade, todos os objetos dependentes dessa entidade também são selecionados automaticamente.  
  
 Você usa o Editor de Pacote de Modelo para selecionar partes de um modelo em um arquivo de pacote que foi criado pela ferramenta MDSModelDeploy (que cria um arquivo de pacote que inclui objetos e dados) ou o assistente de implantação de modelo (que cria um arquivo que inclui apenas a estrutura do modelo). Depois de editar o modelo no pacote, use a ferramenta MDSModelDeploy para implantar objetos e dados, ou o assistente de implantação de modelo, para implantar apenas a estrutura do modelo.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Deve existir um pacote de modelo a ser editado. Para obter mais informações, consulte [Implantando modelos &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md) e [Criar um pacote de implantação de modelo usando o Assistente](../master-data-services/create-a-model-deployment-package-by-using-the-wizard.md) ou [Criar um pacote de implantação de modelo usando MDSModelDeploy](../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
### <a name="to-edit-a-model-deployment-package"></a>Para editar um pacote de implantação de modelo  
  
1.  No Windows Explorer, no servidor MDS, vá para *drive*:\Program Files\Microsoft SQL Server\130\Master Data Services\Configuration.  
  
2.  Execute ModelPackageEditor.exe.  
  
3.  No assistente de Editor de Pacote de Modelo, clique em **Procurar**, vá até a pasta que contém seus pacotes, selecione um pacote e clique em **Abrir**. Clique em **Avançar**.  
  
4.  Selecione essas entidades, hierarquias derivadas, exibições de assinaturas ou regras de negócio a serem implantadas. Cancele a seleção do que você não deseja implantar. Clique em **Avançar**.  
  
5.  Verifique a lista de seleções a ser implantada. Para alterar, clique em **Voltar** e repita a etapa 4.  
  
6.  Clique em **Procurar**, vá para a pasta na qual você deseja salvar o pacote parcial e insira o nome de arquivo do pacote parcial (com uma extensão .pkg). Clique em **Salvar**.  
  
7.  Clique em **Concluir**.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   [Implantar um pacote de implantação de modelo usando o Assistente](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)  
  
-   [Implantar um pacote de implantação de modelo usando MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
  
