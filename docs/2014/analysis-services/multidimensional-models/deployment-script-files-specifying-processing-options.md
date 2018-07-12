---
title: Especificando opções de processamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services deployments, processing options
- input files [Analysis Services]
- deploying [Analysis Services], processing options
- modifying processing options
- Analysis Services Deployment Wizard, processing options
ms.assetid: e9e50817-908e-4210-bc3d-8e2957568241
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c5f20e9061aae762eda6b773c7bdb345273fd1b5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37149097"
---
# <a name="specifying-processing-options"></a>Especificando opções de processamento
  O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Assistente de implantação do lê as opções de processamento das \< *nome do projeto*>. deploymentoptions arquivo. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] cria esse arquivo quando você cria o projeto [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa as opções de processamento especificadas na **implantação** página do  *\<nome do projeto >* **páginas de propriedades** caixa de diálogo para criar o \< *nome do projeto*>. deploymentoptions arquivo.  
  
## <a name="reviewing-the-processing-options-for-deployment"></a>Revisando as opções de processamento para implantação  
 As definições de configuração armazenadas dentro de \< *nome do projeto*> arquivo. deploymentoptions são as seguintes:  
  
-   **Método de Processamento** Essa configuração controla se os objetos implantados são processados após a implantação e o tipo de processamento executados. Há três opções de processamento:  
  
    -   Processamento padrão  
  
    -   Processamento completo  
  
    -   Nenhum  
  
-   **Opções de Tabelas de Write-back** Se o write-back estiver habilitado no projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , essa configuração definirá como o write-back será manipulado. Há três opções de tabela de write-back:  
  
    -   Por padrão, a tabela de write-back existente será usada, se existir. Se uma tabela de write-back não existir, uma nova tabela será criada.  
  
    -   Se uma tabela de write-back já existir, a implantação falhará. Se uma tabela de write-back não existir, uma nova tabela será criada.  
  
    -   Independentemente da existência de uma tabela de write-back, uma nova tabela será criada. Nesse caso, o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] excluirá qualquer tabela existente e vai substituí-la por uma nova.  
  
-   **Implantação Transacional** Essa configuração controla se a implantação das alterações de metadados e dos comandos de processo ocorre em uma única transação ou em transações separadas.  
  
    -   Se essa opção estiver `True` (padrão), [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implanta todas as alterações de metadados e todos os comandos de processo em uma única transação.  
  
    -   Se essa opção estiver `False`, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implante as alterações de metadados em uma única transação e implanta cada comando de processamento em sua própria transação.  
  
## <a name="modifying-the-processing-options-for-deployment"></a>Modificando as opções de processamento para implantação  
 No entanto, talvez você precise implantar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando as opções de processamento diferentes das armazenadas do projeto a \< *nome do projeto*>. deploymentoptions arquivo. Por exemplo, você pode processar por completo todos os objetos, processar usando a opção padrão ou não processá-los. Se os cubos ou dimensões forem habilitados para gravação, é possível especificar se uma tabela de write-back nova ou existente será usada.  
  
 Para modificar as opções de processamento usadas durante a implantação, edite e recrie o projeto ou altere as opções de processamento do arquivo de entrada usando um dos métodos conforme descrito no procedimento a seguir.  
  
#### <a name="to-change-processing-options-after-the-input-files-have-been-generated"></a>Para alterar as opções de processamento depois que os arquivos de entrada tiverem sido gerados  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de modo interativo. Na página **Opções de Processamento** , especifique as opções de processamento para o projeto que está sendo implantado.  
  
     — ou —  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no prompt de comando e defina o assistente para executar em modo de arquivo de resposta. Para obter mais informações sobre o modo de arquivo de resposta, consulte [Running the Analysis Services Deployment Wizard](running-the-analysis-services-deployment-wizard.md).  
  
     — ou —  
  
-   Modificar a \< *nome do projeto*> arquivo. deploymentoptions usando qualquer editor de texto.  
  
## <a name="see-also"></a>Consulte também  
 [Especificando o destino de instalação](deployment-script-files-specifying-the-installation-target.md)   
 [Especificando opções de implantação de função e de partição](deployment-script-files-partition-and-role-deployment-options.md)   
 [Especificando definições de configuração para implantação de solução](deployment-script-files-solution-deployment-config-settings.md)  
  
  
