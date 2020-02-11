---
title: Compilar projetos de Analysis Services (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- projects [Analysis Services], building
- Business Intelligence Development Studio, project building [Analysis Services]
ms.assetid: caac03cb-b2b4-4652-8913-3dd39c4b0127
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97e32b80d19675b3763101d1c226529a48e23e68
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66076768"
---
# <a name="build-analysis-services-projects-ssdt"></a>Criar projetos do Analysis Services (SSDT)
  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você cria um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] como faria com qualquer projeto de programação no Visual Studio. Quando você constrói o projeto, é criado conjunto de arquivos XML no diretório de saída. Eles usam o Analysis Services Scripting Language (ASSL), um dialeto XML que os aplicativos cliente, inclusive o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] , usam para se comunicar com uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para criar ou modificar objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Esses arquivos XML são usados para implantar definições de objeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para uma instância especificada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="building-a-project"></a>Construindo um projeto  
 Quando você criar um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] construirá um conjunto completo de arquivos XML na pasta de saída que contém todos os comandos ASSL necessários para construir todos os objetos do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no projeto. Se o projeto já foi construído e a implantação incremental foi especificada na configuração ativa, o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] construirá também um arquivo XML contendo os comandos ASSL para executar a atualização incremental dos objetos implantados. Esse arquivo XML é gravado na pasta ..\obj\\<configuração ativa\> do projeto. Construções incrementais podem poupar tempo na hora de implantar e processar um projeto ou banco de dados muito grande.  
  
> [!NOTE]  
>  Você pode usar o comando Reconstruir Tudo para ignorar a configuração de implantação incremental.  
  
 A construção de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] valida as definições de objeto do projeto. A validação inclui todos os assemblies de referência. Erros de construção aparecem na janela Lista de Tarefas, com o texto do erro do Objetos de Gerenciamento de Análise (AMO). Você pode clicar em um erro para abrir o designer, necessário para corrigir o erro.  
  
 A validação bem-sucedida não garante que os objetos poderão ser criados no servidor de destino durante a implantação nem processados com êxito após a implantação. Os problemas a seguir podem impedir a implantação bem-sucedida ou o processando após a implantação:  
  
-   As verificações de segurança do servidor não são executadas, portanto, bloqueios podem impedir a implantação.  
  
-   Locais físicos não são validados no servidor.  
  
-   Detalhes das exibições da fontes de dados não são verificados na fonte de dados real do servidor de destino.  
  
 Se a validação for bem-sucedida, o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] gerará os arquivos XML. Depois da construção, a pasta de saída conterá os arquivos descritos na tabela a seguir.  
  
|Arquivos (em pasta de compartimento)|DESCRIÇÃO|  
|-----------------------------|-----------------|  
|*ProjectName*. asdatabase|Contém os elementos ASSL que definem metadados para os objetos do projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em um arquivo de script de implantação. Esse arquivo é usado pelo mecanismo de implantação para implantar os objetos em um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|*ProjectName*. configsettings|Contém os parâmetros de configuração usados na implantação que você pode modificar diretamente ou usando o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (por exemplo, a cadeia de conexão das fontes de dados).|  
|*ProjectName*. deploymenttargets|Contém as configurações de destino usadas na implantação que você pode modificar diretamente ou usando o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (por exemplo, os nomes do servidor e do banco de dados).|  
|*ProjectName*. deploymentoptions|Contém as várias configurações opcionais usadas na implantação que você pode modificar diretamente ou usando o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (por exemplo, os locais de armazenamento)|  
|*AssemblyName*/*DllName.* dll|Pastas separadas para cada assembly de referência; cada pasta contém a DLL do assembly, todos os assemblies de referência e todos os arquivos .pdb associados para as informações de depuração da saída.|  
  
|Arquivos (na pasta obj)|DESCRIÇÃO|  
|-----------------------------|-----------------|  
|\<Nome da configuração> \LastBuilt.xml|Contém o carimbo de hora e código hash que identificam a data da última construção do projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
  
 Esses arquivos XML não contêm \<marcas Create> e \<ALTER>, que são construídas durante a implantação.  
  
 Os assemblies de referência (exceto os assemblies padrão do sistema e do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ) são copiados no diretório de saída. Se houver referências para outros objetos da solução, esses projetos serão criados primeiro, usando a configuração do projeto apropriada e as dependências de construção estabelecidas pelas referências do projeto e, em seguida, eles serão copiados para a pasta de saída do projeto.  
  
## <a name="see-also"></a>Consulte Também  
 [Analysis Services linguagem de script &#40;referência de&#41; do ASSL](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [Implantar projetos de Analysis Services &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)  
  
  
