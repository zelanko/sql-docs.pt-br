---
title: Adicionar caixa de diálogo de referência (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.addreference.f1
- sql12.asvs.bidevstudio.assembly.addassembly.f1
helpviewer_keywords:
- Add Reference dialog box
ms.assetid: 457958c4-6baa-474d-99a0-34c195ceba09
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a2a44c1f7a37cc7e7e010ea15c72d35255b443e4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48174176"
---
# <a name="add-reference-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Adicionar Referência (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Adicionar Referência** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para adicionar uma referência a um assembly do [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework ou a outro projeto em seu projeto de desenvolvimento. É possível exibir a caixa de diálogo **Adicionar Referência** clicando com o botão direito do mouse na pasta **Assemblies** de um projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no **Gerenciador de Soluções** e selecionando **Nova Referência de Assembly** no menu de contexto.  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**.NET**|Selecione esta guia para adicionar uma referência a um componente registrado. Essa guia exibe uma grade que contém uma lista de componentes do .NET Framework registrados. Selecione um ou mais itens na grade e clique em **Adicionar** para adicionar os componentes do .NET selecionados a **Produtos e componentes selecionados**. A grade contém as seguintes colunas:<br /><br /> **Nome do componente**: o nome completo ou "amigável" do componente. Selecione o título para classificar pelo nome do componente.<br /><br /> **Versão**: O número de versão listados do componente. Selecione o título para classificar pela versão.<br /><br /> **Tempo de execução**: A versão do .NET Framework na qual o componente é baseado. Selecione o título para classificar pela versão do tempo de execução.<br /><br /> **Caminho**: O nome do arquivo do componente e o caminho onde ele está localizado. Selecione o título para classificar pelo caminho.|  
|**Procurar**|Clique para procurar o sistema de arquivos para um assembly não listado nas guias **.NET** ou **Recente** . Essa guia exibe as seguintes opções:<br /><br /> **Procure no**: selecione uma pasta nesta lista suspensa. A seleção de uma pasta nessa lista exibe o conteúdo da pasta no painel principal.<br /><br /> **Vá para a última pasta visitada**: retorna **xaminar** para o local anterior.<br /><br /> **Um nível acima**: localiza a próxima pasta mais alta na hierarquia.<br /><br /> **Criar nova pasta**: Selecione para criar uma nova pasta filho sob a pasta selecionada na **xaminar**.<br /><br /> **Exibir Menu**: Selecione para alterar a exibição do conteúdo no painel principal.  Para obter mais informações sobre a opções do **Menu Exibir**consulte o tópico "Visão geral da exibição de arquivos e pastas" na documentação do [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows. As seguintes opções estão disponíveis:<br />Miniaturas<br />Lado a lado<br />Ícones<br />Lista<br />Detalhes<br /><br /> **Painel primário**: exibe o conteúdo da pasta selecionada na **xaminar**. Selecione um ou mais itens e, em seguida, clique em **Add** para adicionar os arquivos selecionados **produtos e componentes selecionados**. Para obter mais informações sobre a opções e o menu de contexto no painel primário, consulte o tópico "Visão geral da exibição de arquivos e pastas" na documentação do Windows.<br /><br /> **Nome do arquivo**: Use esta opção para filtrar os arquivos e pastas que são exibidos. Digite um nome completo ou parcial do arquivo pelo qual filtrar. Você pode usar o asterisco (\*) como um curinga. Digite vários nomes de arquivos (com cada nome incluído entre aspas (") e delimitado por um espaço) para selecionar vários arquivos. Também é possível selecionar arquivos revistos anteriormente selecionando um nome de arquivo na lista suspensa. Dica: Você pode localizar servidores Web e computadores da rede, inserindo um URL ou caminho de rede no **nome do arquivo**. Por exemplo, "http://mywebsite" exibe os arquivos disponíveis no local da Web "meusite" e "\\\meuservidor\meucompartilhamento" exibe os arquivos disponíveis no local "meucompartilhamento" em "meuservidor".<br /><br /> **Arquivos do tipo**: Use esta opção para filtrar o conteúdo da pasta ou diretório selecionado em **xaminar** para um tipo de arquivo específico.|  
|**Recentes**|Exibe uma lista de referências de componentes recém-adicionada a projetos no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Selecione um ou mais itens na grade e clique em **Adicionar** para adicionar os assemblies do .NET Framework selecionados a **Produtos e componentes selecionados**. A grade contém as seguintes colunas:<br /><br /> **Nome do componente**: o nome completo ou "amigável" do componente. Selecione o título para classificar pelo nome do componente.<br /><br /> **Versão**: O número de versão listados do componente. Selecione o título para classificar pela versão.<br /><br /> **Tempo de execução**: A versão do .NET Framework na qual o componente é baseado. Selecione o título para classificar pela versão do tempo de execução.<br /><br /> **Caminho**: O nome do arquivo do componente e o caminho onde ele está localizado. Selecione o título para classificar pelo caminho.|  
|**Adicionar**|Clique para adicionar um componente selecionado nas guias **.NET**, **Procurar**ou **Recente** a **Projetos e componentes selecionados**.|  
|**Remover**|Clique para remover um componente selecionado em **Projetos e componentes selecionados**.|  
|**Projetos e componentes selecionados**|Exibe uma lista de referências de componentes a serem adicionadas ao projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Selecione um ou mais itens na grade e clique em **Remover** para remover os componentes selecionados da grade. A grade contém as seguintes colunas:<br /><br /> **Nome do componente**: o nome completo ou "amigável" do componente. Selecione o título para classificar pelo nome do componente.<br /><br /> **Versão**: O número de versão listados do componente. Selecione o título para classificar pela versão.<br /><br /> **Tempo de execução**: A versão do .NET Framework na qual o componente é baseado. Selecione o título para classificar pela versão do tempo de execução.<br /><br /> **Caminho**: O nome do arquivo do componente e o caminho onde ele está localizado. Selecione o título para classificar pelo caminho.|  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Gerenciamento de Assemblies de modelo multidimensional](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
