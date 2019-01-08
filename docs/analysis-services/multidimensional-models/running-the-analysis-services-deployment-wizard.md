---
title: Executar o Analysis Services Deployment Wizard | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d459bafe395a10af75f8c0a721f0a8a08f39b3c6
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52509680"
---
# <a name="running-the-analysis-services-deployment-wizard"></a>Executando o Assistente para Implantação do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Assistente de implantação pode ser executado das seguintes maneiras:  
  
-   **Interativamente** quando executado interativamente, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Assistente de implantação gera um script de implantação com base em arquivos de entrada, como modificado interativamente pela entrada do usuário. O assistente aplica qualquer modificação de usuário somente ao script de implantação. O assistente não modifica os arquivos de entrada. Para saber mais sobre os arquivos de entrada, veja [Noções básicas sobre arquivos de entrada usados para criar o script de implantação](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md).  
  
-   **No prompt de comando** quando executado no prompt de comando, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Assistente de implantação gera um script de implantação baseado nas opções que você pode usar para executar o assistente. O assistente pode executar qualquer uma destas ações: alertá-lo para entrada de usuário e modificar arquivos de entrada com base naquela entrada; executar uma implantação autônoma silenciosa, que usa os arquivos de entrada como são; ou criar um script de implantação que você pode usar depois.  
  
## <a name="running-the-analysis-services-deployment-wizard-interactively"></a>Executando o Assistente para Implantação do Analysis Services interativamente  
 Quando executado interativamente, o Assistente de Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] lê os valores dos arquivos de entrada e apresenta estas informações a você. Você pode modificar esses valores – como de entrada como destino de implantação, as definições de configuração, as opções de implantação e as senhas de cadeia de caracteres de conexão- ou deixá-los como está. Se você alterar quaisquer valores de entrada, o assistente usará essas mudanças ao gerar o script de implantação. Porém, o assistente não faz nenhuma alteração nos valores do arquivo de entrada.  
  
> [!NOTE]  
>  Se você quiser que o Assistente de Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] modifique os valores de entrada, execute o assistente no prompt de comando e defina o assistente para ser executado no modo de arquivo de resposta.  
  
 Depois de examinar os valores de entrada e fizer qualquer mudança desejada, o assistente gera o script de implantação. Você pode executar esse script de implantação imediatamente no servidor de destino ou salvá-lo para uso posterior.  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-interactively"></a>Para executar o Assistente para Implantação do Analysis Services interativamente  
  
-   Clique em **inicie** > **Microsoft SQL Server** > **o Assistente de implantação**.  
  
     -ou-  
  
-   No **projetos** pasta da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] do projeto, clique duas vezes o \<nome do projeto >. asdatabase.
    > [!NOTE]  
    >  Se você não encontrar o arquivo .asdatabase, use Pesquisar e especifique *.asdatabase. Ou, talvez seja necessário compilar o projeto no SSDT.  
  
## <a name="running-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>Executando o Assistente para Implantação do Analysis Services no prompt de comando  
 O Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] também pode ser executado no prompt de comando. Quando você executa o assistente no prompt de comando, você fornece o caminho completo para o arquivo .asdatabase e executa o assistente em um dos seguintes modos:  
  
 **Modo de arquivo de resposta**  
 No modo de arquivo de resposta, o assistente permite a modificação interativa da entrada de arquivos que foram gerados originalmente na criação do projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. O assistente salva esses arquivos de entrada modificados antes de gerar o script de implantação. Os arquivos de entrada modificados tornam-se o novo ponto de partida na próxima vez que o assistente for executado.  
  
 Para executar o assistente no modo de arquivo de resposta, use o **/a** alternar.  
  
 **Modo sem confirmação**  
 No modo silencioso, o assistente executa uma implantação autônoma silenciosa com base na informação residente nos arquivos de entrada.  
  
 Para executar o assistente no modo silencioso, use o **/s** alternar. Quando você executar o assistente no modo silencioso, serão produzidas mensagens para o console ou, se fornecido, para um arquivo de log.  
  
 **Modo de saída**  
 No modo de saída, o assistente gera um script de implantação para execução posterior com base em arquivos de entrada.  
  
 Para executar o assistente no modo de saída, use o **/o** alternar e forneça um nome de arquivo de saída.  
  
 Para saber mais sobre essas opções de linha de comando, veja [Implantar soluções de modelo com o Utilitário de Implantação](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md).  
  
 O procedimento a seguir descreve como executar o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no prompt de comando.  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>Para executar o Assistente para Implantação do Analysis Services no prompt de comando  
  
1.  Abra um prompt de comando e navegue até o \Microsoft SQL Server\140\Tools\Binn\ManagementStudio C:\Program Files (x86)  
  
2.  Digite **Microsoft.AnalysisServices.Deployment.exe** seguido pelas opções que correspondem ao modo no qual você deseja executar o assistente.  
  
## <a name="see-also"></a>Consulte também  
 [Compreendendo o script de implantação do Analysis Services](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)   
 [Deploy Model Solutions Using the Deployment Wizard](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)  
  
  
