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
ms.topic: article
helpviewer_keywords:
- Analysis Services deployments, processing options
- input files [Analysis Services]
- deploying [Analysis Services], processing options
- modifying processing options
- Analysis Services Deployment Wizard, processing options
ms.assetid: e9e50817-908e-4210-bc3d-8e2957568241
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7035045d1d55e9158431dd4245b9d5112b2df0a4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009249"
---
# <a name="specifying-processing-options"></a>Especificando opções de processamento
  O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Assistente de implantação do lê as opções de processamento de \< *nome do projeto*>. deploymentoptions. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] cria esse arquivo quando você cria o projeto [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa as opções de processamento especificadas no **implantação** página de  *\<nome do projeto >* **páginas de propriedades** caixa de diálogo para criar o \< *nome do projeto*>. deploymentoptions.  
  
## <a name="reviewing-the-processing-options-for-deployment"></a>Revisando as opções de processamento para implantação  
 As definições de configuração armazenadas no \< *nome do projeto*>. deploymentoptions são as seguintes:  
  
-   **Método de Processamento** Essa configuração controla se os objetos implantados são processados após a implantação e o tipo de processamento executados. Há três opções de processamento:  
  
    -   Processamento padrão  
  
    -   Processamento completo  
  
    -   Nenhum  
  
-   **Opções de Tabelas de Write-back** Se o write-back estiver habilitado no projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , essa configuração definirá como o write-back será manipulado. Há três opções de tabela de write-back:  
  
    -   Por padrão, a tabela de write-back existente será usada, se existir. Se uma tabela de write-back não existir, uma nova tabela será criada.  
  
    -   Se uma tabela de write-back já existir, a implantação falhará. Se uma tabela de write-back não existir, uma nova tabela será criada.  
  
    -   Independentemente da existência de uma tabela de write-back, uma nova tabela será criada. Nesse caso, o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] excluirá qualquer tabela existente e vai substituí-la por uma nova.  
  
-   **Implantação Transacional** Essa configuração controla se a implantação das alterações de metadados e dos comandos de processo ocorre em uma única transação ou em transações separadas.  
  
    -   Se essa opção for `True` (padrão), [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implanta todos os comandos de processo em uma única transação e todas as alterações de metadados.  
  
    -   Se essa opção for `False`, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implanta as alterações de metadados em uma única transação e implanta cada comando de processamento em sua própria transação.  
  
## <a name="modifying-the-processing-options-for-deployment"></a>Modificando as opções de processamento para implantação  
 No entanto, você precisará implantar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto usando opções de processamento diferentes das armazenadas no \< *nome do projeto*>. deploymentoptions. Por exemplo, você pode processar por completo todos os objetos, processar usando a opção padrão ou não processá-los. Se os cubos ou dimensões forem habilitados para gravação, é possível especificar se uma tabela de write-back nova ou existente será usada.  
  
 Para modificar as opções de processamento usadas durante a implantação, edite e recrie o projeto ou altere as opções de processamento do arquivo de entrada usando um dos métodos conforme descrito no procedimento a seguir.  
  
#### <a name="to-change-processing-options-after-the-input-files-have-been-generated"></a>Para alterar as opções de processamento depois que os arquivos de entrada tiverem sido gerados  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de modo interativo. Na página **Opções de Processamento** , especifique as opções de processamento para o projeto que está sendo implantado.  
  
     — ou —  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no prompt de comando e defina o assistente para executar em modo de arquivo de resposta. Para obter mais informações sobre o modo de arquivo de resposta, consulte [Running the Analysis Services Deployment Wizard](running-the-analysis-services-deployment-wizard.md).  
  
     — ou —  
  
-   Modificar o \< *nome do projeto*>. deploymentoptions usando qualquer editor de texto.  
  
## <a name="see-also"></a>Consulte também  
 [Especificar o destino de instalação](deployment-script-files-specifying-the-installation-target.md)   
 [Especificando opções de implantação de função e de partição](deployment-script-files-partition-and-role-deployment-options.md)   
 [Especificando definições de configuração para implantação de solução](deployment-script-files-solution-deployment-config-settings.md)  
  
  