---
title: Implantar soluções modelo com o utilitário de implantação | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fbc272eacb7c5bccd3faeab799ffb32b5bad3aaa
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-model-solutions-with-the-deployment-utility"></a>Implantar soluções modelo com o Utilitário de Implantação
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  O utilitário **Microsoft.AnalysisServices.Deployment** permite iniciar o mecanismo de implantação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no prompt de comando. Como arquivo de entrada, o utilitário usa os arquivos de saída XML gerados pela construção de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Os arquivos de entrada são facilmente modificáveis para personalizar a implantação de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . O script de implantação gerado pode ser executado imediatamente ou pode ser salvo para implantação posterior.  
  
> [!NOTE]
> O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilitário da Assistente de implantação é instalado com o [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) (SSMS). Certifique-se de que você está usando a versão mais recente. Por padrão, a versão mais recente do Assistente de implantação é instalada em C:\Program Files (x86) \Microsoft SQL Server\140\Tools\Binn\ManagementStudio. 

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
  
## <a name="remarks"></a>Comentários  
 O utilitário **Microsoft.AnalysisServices.Deployment** usa um conjunto de arquivos que fornecem as definições de objetos, destinos da implantação, opções da implantação e definições da configuração e tenta implantar as definições de objetos nos destinos de implantação especificados usando as opções de implantação e os parâmetros de configuração especificados. Esse utilitário pode fornecer uma interface do usuário quando invocado em modo de arquivo de resposta ou de saída. Para obter mais informações sobre como usar a interface do usuário fornecida para esse utilitário para criar arquivos de resposta, consulte [Implantar soluções modelo usando o Assistente de Implantação](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md).  
  
 O utilitário está localizado na pasta \Program files (x86) \Microsoft SQL Server\140\Binn\ManagementStudio.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de utilitários de prompt de comando &#40;Mecanismo de Banco de Dados&#41;](../../tools/command-prompt-utility-reference-database-engine.md)  
  
  
