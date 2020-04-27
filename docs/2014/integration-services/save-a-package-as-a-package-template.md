---
title: Salvar um pacote como um modelo de pacote | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- reusing packages
- templates [Integration Services]
ms.assetid: efe66cec-3933-4f6e-8d35-fe3d300de66c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 76349c0ca91f24a6d8d7942a89eb9683a91b573d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66056336"
---
# <a name="save-a-package-as-a-package-template"></a>Salvar um pacote como um modelo de pacote
  Este tópico descreve como designar e usar pacotes personalizados como modelos para criar novos pacotes do Integration Services no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Por padrão, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] usa um modelo de pacote que cria um pacote vazio quando você adiciona um novo pacote a um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Você não pode substituir este modelo padrão, mas pode adicionar novos modelos.  
  
 Você pode designar vários pacotes para serem usados como modelos. Antes de implementar os pacotes personalizados como modelos, é preciso criá-los.  
  
 Ao criar um pacote usando os pacotes personalizados como modelos, os novos pacotes apresentam o mesmo nome e GUID do modelo. Para obter a diferenciação dos pacotes, atualize o valor da propriedade `Name` e gere uma nova GUID para a propriedade `ID`. Para obter mais informações, consulte [Criar pacotes no SQL Server Data Tools](create-packages-in-sql-server-data-tools.md) e [Definir Propriedades de Pacote](set-package-properties.md).  
  
### <a name="to-designate-a-custom-package-as-a-package-template"></a>Para designar um pacote personalizado como um modelo de pacote  
  
1.  No sistema de arquivos, localize o pacote que deseja usar como modelo.  
  
2.  Copie o pacote para a pasta DataTransformationItems. Por padrão, esta pasta está em C:\Arquivos de Programas\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject.  
  
3.  Repita as etapas 1 e 2 para cada pacote que quiser usar como modelo.  
  
### <a name="to-use-a-custom-package-as-a-package-template"></a>Para usar um pacote personalizado como um modelo de pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no qual você deseja criar um pacote.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no projeto, aponte para **Adicionar** e clique em **Novo Item**.  
  
3.  Na caixa de diálogo **Adicionar novo\<item – nome do projeto>** , clique no pacote que você deseja usar como modelo.  
  
     A lista de modelos inclui o modelo padrão do pacote chamado Novo Pacote SSIS. O ícone do pacote identifica os modelos que podem ser usados como modelos de pacote.  
  
4.  Clique em **Adicionar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar pacotes no SQL Server Data Tools](create-packages-in-sql-server-data-tools.md)   
 [Pacotes do Integration Services &#40;SSIS&#41;](../../2014/integration-services/integration-services-ssis-packages.md)  
  
  
