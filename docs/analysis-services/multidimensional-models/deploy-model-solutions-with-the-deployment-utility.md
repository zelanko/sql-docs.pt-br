---
title: "Implantar soluções modelo com o utilitário de implantação | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deploying [Analysis Services], command prompt
- command prompt utilities [SQL Server], Microsoft.AnalysisServices.Deployment
- Microsoft.AnalysisServices.Deployment utility
- Analysis Services deployments, command prompt
ms.assetid: 584f78ac-5f18-41e0-b292-d1949ec05196
caps.latest.revision: "23"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1e094ee032e236d39003fe6e2f572edfea6241a5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="deploy-model-solutions-with-the-deployment-utility"></a>Implantar soluções modelo com o Utilitário de Implantação
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]O **Microsoft.AnalysisServices.Deployment** utilitário permite que você inicie a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mecanismo de implantação do prompt de comando. Como arquivo de entrada, o utilitário usa os arquivos de saída XML gerados pela construção de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Os arquivos de entrada são facilmente modificáveis para personalizar a implantação de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . O script de implantação gerado pode ser executado imediatamente ou pode ser salvo para implantação posterior.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Microsoft.AnalysisServices.Deployment [ASdatabasefile]   
    {[/s[:logfile]] | [/a] | [[/o[:output_script_file]] [/d]]}  
```  
  
##  <a name="Arguments"></a> Argumentos  
 *ASdatabasefile*  
 O caminho completo da pasta na qual o arquivo de script de implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (.asdatabase) está localizado. Esse arquivo é gerado quando você implanta um projeto no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Ele está localizado na pasta bin do projeto. O arquivo .asdatabase que contém as definições de objetos a serem implantados está localizado. Se não for especificada, a pasta atual será usada.  
  
 **/s**  
 Executa o utilitário em modo sem confirmação e não exibe nenhuma caixa de diálogo. Para obter mais informações sobre modos, consulte a seção, [Modos](#Modes), mais adiante neste tópico.  
  
 *logfile*  
 O caminho completo e o nome do arquivo de log. Eventos de rastreamento serão registrados no arquivo de log especificado. Se o arquivo de log já existir, seu conteúdo será substituído.  
  
 **/a**  
 Executa o utilitário em modo de resposta. Todas as respostas feitas durante a parte do assistente do utilitário devem ser gravadas novamente nos arquivos de entrada, mas nenhuma alteração será realmente feita nos destinos da implantação.  
  
 **/o**  
 Executa o utilitário em modo de saída. A implantação não ocorrerá, mas o script XMLA (XML for Analysis) que normalmente é enviado aos destinos da implantação é salvo no arquivo de script de saída especificado. Se o *output_script_file* não for especificado, o utilitário tentará usar o arquivo de script de saída especificado no arquivo de entrada de opções da implantação (.deploymentoptions). Se um arquivo de script de saída não for especificado no arquivo de entrada de opções da implantação, ocorrerá um erro.  
  
 Para obter mais informações sobre modos, consulte a seção, [Modos](#Modes), mais adiante neste tópico.  
  
 *output_script_file*  
 O caminho completo e o nome do arquivo de script de saída.  
  
 **/d**  
 Caso o argumento **/o** seja usado, especifica que o utilitário não deve se conectar à instância de destino. Como nenhuma conexão é feita com os destinos da implantação, o script de saída é gerado com base apenas nas informações recuperadas dos arquivos de entrada.  
  
> [!NOTE]  
>  O argumento **/d** é usado apenas no modo de saída. Esse argumento será ignorado se especificado em modo de resposta ou sem confirmação. Para obter mais informações sobre modos, consulte a seção, [Modos](#Modes), mais adiante neste tópico.  
  
## <a name="remarks"></a>Remarks  
 O utilitário **Microsoft.AnalysisServices.Deployment** usa um conjunto de arquivos que fornecem as definições de objetos, destinos da implantação, opções da implantação e definições da configuração e tenta implantar as definições de objetos nos destinos de implantação especificados usando as opções de implantação e os parâmetros de configuração especificados. Esse utilitário pode fornecer uma interface do usuário quando invocado em modo de arquivo de resposta ou de saída. Para obter mais informações sobre como usar a interface do usuário fornecida para esse utilitário para criar arquivos de resposta, consulte [Implantar soluções modelo usando o Assistente de Implantação](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md).  
  
 O utilitário está localizado na pasta \Arquivos de programas (x86)\Microsoft SQL Server\110\Binn\ManagementStudio.  
  
##  <a name="Modes"></a> Modos  
 O utilitário pode ser executado nos modos listados na tabela a seguir.  
  
|Modo|Description|  
|----------|-----------------|  
|Modo sem confirmação|Nenhuma interface do usuário é exibida e todas as informações necessárias para a implantação são fornecidas pelos arquivos de entrada. Nenhum progresso é exibido pelo utilitário em modo sem confirmação. Em vez disso, um arquivo de log opcional pode ser usado para capturar o progresso e informações de erro para revisão posterior.|  
|Modo de resposta|A interface do usuário do Assistente para Implantação é exibida e as respostas do usuário são salvas nos arquivos de entrada especificados para implantação posterior. A implantação não acontece em modo de resposta. O único propósito do modo de resposta é capturar respostas do usuário.|  
|Modo de saída|Nenhuma interface do usuário é exibida e todas as informações necessárias para a implantação são fornecidas pelos arquivos de entrada.<br /><br /> No entanto, ao contrário do modo sem confirmação, a saída do utilitário é gravada em um arquivo de script de saída e não é enviada aos destinos de implantação indicados nos arquivos de entrada. A menos que o argumento **/d** seja especificado, o utilitário se conecta à cada destino de implantação para comparar metadados ao gerar o arquivo de script de saída.|  
  
 [Voltar para Argumentos](#Arguments)  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como implantar um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em modo sem confirmação, registrando as mensagens de progresso e de erro para revisão posterior:  
  
 `Microsoft.AnalysisServices.Deployment.exe`  
  
 `<drive>:\My Documents\Visual Studio 2010\Projects\AdventureWorksProject\Project1\bin`  
  
 `/s: C:\ My Documents\Visual Studio 2010\Projects\AdventureWorksProject\Project1\bin\deployment.log`  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de utilitários de prompt de comando &#40;Mecanismo de Banco de Dados&#41;](../../tools/command-prompt-utility-reference-database-engine.md)  
  
  
