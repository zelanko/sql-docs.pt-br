---
title: Especificando opções de processamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services deployments, processing options
- input files [Analysis Services]
- deploying [Analysis Services], processing options
- modifying processing options
- Analysis Services Deployment Wizard, processing options
ms.assetid: e9e50817-908e-4210-bc3d-8e2957568241
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ea766d26034b9ee0d1fcefbd215f41c19da1f9ef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66075233"
---
# <a name="specifying-processing-options"></a>Especificando opções de processamento
  O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] assistente de implantação lê as opções de processamento \<do arquivo *nome do projeto*>. deploymentoptions. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]cria esse arquivo quando você compila o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]usa as opções de processamento especificadas na página **implantação** do * \<nome do projeto>* caixa de diálogo **páginas de propriedades** para criar o nome do \< *projeto*> arquivo. deploymentoptions.  
  
## <a name="reviewing-the-processing-options-for-deployment"></a>Revisando as opções de processamento para implantação  
 As definições de configuração armazenadas no \<arquivo de *nome do projeto*>. deploymentoptions são as seguintes:  
  
-   **Método de processamento** Essa configuração controla se os objetos implantados são processados após a implantação e o tipo de processamento que será executado. Há três opções de processamento:  
  
    -   Processamento padrão  
  
    -   Processamento completo  
  
    -   Nenhum  
  
-   **Opções de tabela de write-back** Se o Write-back estiver [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] habilitado no projeto, essa configuração definirá como o Write-back é manipulado. Há três opções de tabela de write-back:  
  
    -   Por padrão, a tabela de write-back existente será usada, se existir. Se uma tabela de write-back não existir, uma nova tabela será criada.  
  
    -   Se uma tabela de write-back já existir, a implantação falhará. Se uma tabela de write-back não existir, uma nova tabela será criada.  
  
    -   Independentemente da existência de uma tabela de write-back, uma nova tabela será criada. Nesse caso, o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] excluirá qualquer tabela existente e vai substituí-la por uma nova.  
  
-   **Implantação transacional** Essa configuração controla se a implantação de alterações de metadados e comandos de processo ocorre em uma única transação ou em transações separadas.  
  
    -   Se essa opção for `True` (padrão), o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implantará todas as alterações de metadados e todos os comandos de processo em uma única transação.  
  
    -   Se essa opção for `False`, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implantará as alterações de metadados em uma única transação e cada comando de processamento será implantado em sua própria transação.  
  
## <a name="modifying-the-processing-options-for-deployment"></a>Modificando as opções de processamento para implantação  
 No entanto, talvez seja necessário implantar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o projeto usando opções de processamento diferentes das armazenadas no \<arquivo *nome do projeto*>. deploymentoptions. Por exemplo, você pode processar por completo todos os objetos, processar usando a opção padrão ou não processá-los. Se os cubos ou dimensões forem habilitados para gravação, é possível especificar se uma tabela de write-back nova ou existente será usada.  
  
 Para modificar as opções de processamento usadas durante a implantação, edite e recrie o projeto ou altere as opções de processamento do arquivo de entrada usando um dos métodos conforme descrito no procedimento a seguir.  
  
#### <a name="to-change-processing-options-after-the-input-files-have-been-generated"></a>Para alterar as opções de processamento depois que os arquivos de entrada tiverem sido gerados  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de modo interativo. Na página **Opções de Processamento** , especifique as opções de processamento para o projeto que está sendo implantado.  
  
     -ou-  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no prompt de comando e defina o assistente para executar em modo de arquivo de resposta. Para obter mais informações sobre o modo de arquivo de resposta, consulte [executando o assistente de implantação de Analysis Services](running-the-analysis-services-deployment-wizard.md).  
  
     -ou-  
  
-   Modifique o \<arquivo de *nome do projeto*>. deploymentoptions usando qualquer editor de texto.  
  
## <a name="see-also"></a>Consulte Também  
 [Especificando o destino de instalação](deployment-script-files-specifying-the-installation-target.md)   
 [Especificando opções de implantação de partição e função](deployment-script-files-partition-and-role-deployment-options.md)   
 [Especificando definições de configuração para implantação de solução](deployment-script-files-solution-deployment-config-settings.md)  
  
  
