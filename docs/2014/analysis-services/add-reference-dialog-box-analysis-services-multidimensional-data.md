---
title: Caixa de diálogo Adicionar referência (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.addreference.f1
- sql12.asvs.bidevstudio.assembly.addassembly.f1
helpviewer_keywords:
- Add Reference dialog box
ms.assetid: 457958c4-6baa-474d-99a0-34c195ceba09
author: minewiskan
ms.author: owend
ms.openlocfilehash: e35eeae8f48fe25e8f0c79455271d83ca1c609f8
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528272"
---
# <a name="add-reference-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Adicionar Referência (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Adicionar Referência** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para adicionar uma referência a um assembly do [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework ou a outro projeto em seu projeto de desenvolvimento. É possível exibir a caixa de diálogo **Adicionar Referência** clicando com o botão direito do mouse na pasta **Assemblies** de um projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no **Gerenciador de Soluções** e selecionando **Nova Referência de Assembly** no menu de contexto.  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**.NET**|Selecione esta guia para adicionar uma referência a um componente registrado. Essa guia exibe uma grade que contém uma lista de componentes do .NET Framework registrados. Selecione um ou mais itens na grade e clique em **Adicionar** para adicionar os componentes do .NET selecionados a **Produtos e componentes selecionados**. A grade contém as seguintes colunas:<br /><br /> **Nome do componente**: o nome completo ou "amigável" do componente. Selecione o título para classificar pelo nome do componente.<br /><br /> **Versão**: o número de versão listado do componente. Selecione o título para classificar pela versão.<br /><br /> **Tempo de execução**: a versão do .NET Framework no qual o componente é baseado. Selecione o título para classificar pela versão do runtime.<br /><br /> **Caminho**: o nome do arquivo do componente e o caminho onde ele está localizado. Selecione o título para classificar pelo caminho.|  
|**Procurar**|Clique para procurar o sistema de arquivos para um assembly não listado nas guias **.NET** ou **Recente** . Essa guia exibe as seguintes opções:<br /><br /> **Examinar**: selecione uma pasta nessa lista suspensa. A seleção de uma pasta nessa lista exibe o conteúdo da pasta no painel principal.<br /><br /> **Ir para a última pasta visitada**: retorna a **aparência** para o local anterior.<br /><br /> **Um nível acima**: localiza a próxima pasta superior na hierarquia.<br /><br /> **Criar nova pasta**: Selecione para criar uma nova pasta filho na pasta selecionada em **examinar**.<br /><br /> **Menu Exibir**: Selecione para alterar a exibição do conteúdo no painel primário.  Para obter mais informações sobre a opções do **Menu Exibir**consulte o tópico "Visão geral da exibição de arquivos e pastas" na documentação do [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows. As seguintes opções estão disponíveis:<br />Miniaturas<br />Blocos<br />Ícones<br />Lista<br />Detalhes<br /><br /> **Painel primário**: exibe o conteúdo da pasta selecionada em **examinar**. Selecione um ou mais itens e clique em **Adicionar** para adicionar os arquivos selecionados aos **produtos e componentes selecionados**. Para obter mais informações sobre a opções e o menu de contexto no painel primário, consulte o tópico "Visão geral da exibição de arquivos e pastas" na documentação do Windows.<br /><br /> **Nome do arquivo**: Use essa opção para filtrar os arquivos e pastas que são exibidos. Digite um nome completo ou parcial do arquivo pelo qual filtrar. Você pode usar o asterisco (\*) como um curinga. Digite vários nomes de arquivos (com cada nome incluído entre aspas (") e delimitado por um espaço) para selecionar vários arquivos. Também é possível selecionar arquivos revistos anteriormente selecionando um nome de arquivo na lista suspensa. Dica: você pode localizar servidores Web e computadores de rede inserindo uma URL ou um caminho de rede no **nome do arquivo**. Por exemplo, "http://mywebsite" exibe os arquivos disponíveis no local da Web "meusite" e "\\\meuservidor\meucompartilhamento" exibe os arquivos disponíveis no local "meucompartilhamento" em "meuservidor".<br /><br /> **Arquivos do tipo**: Use esta opção para filtrar o conteúdo da pasta ou diretório selecionado em **examinar** para um tipo de arquivo específico.|  
|**Recente**|Exibe uma lista de referências de componentes recém-adicionada a projetos no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Selecione um ou mais itens na grade e clique em **Adicionar** para adicionar os assemblies do .NET Framework selecionados a **Produtos e componentes selecionados**. A grade contém as seguintes colunas:<br /><br /> **Nome do componente**: o nome completo ou "amigável" do componente. Selecione o título para classificar pelo nome do componente.<br /><br /> **Versão**: o número de versão listado do componente. Selecione o título para classificar pela versão.<br /><br /> **Tempo de execução**: a versão do .NET Framework no qual o componente é baseado. Selecione o título para classificar pela versão do runtime.<br /><br /> **Caminho**: o nome do arquivo do componente e o caminho onde ele está localizado. Selecione o título para classificar pelo caminho.|  
|**Adicionar**|Clique para adicionar um componente selecionado nas guias **.NET**, **Procurar**ou **Recente** a **Projetos e componentes selecionados**.|  
|**Removerr**|Clique para remover um componente selecionado em **Projetos e componentes selecionados**.|  
|**Projetos e componentes selecionados**|Exibe uma lista de referências de componentes a serem adicionadas ao projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Selecione um ou mais itens na grade e clique em **Remover** para remover os componentes selecionados da grade. A grade contém as seguintes colunas:<br /><br /> **Nome do componente**: o nome completo ou "amigável" do componente. Selecione o título para classificar pelo nome do componente.<br /><br /> **Versão**: o número de versão listado do componente. Selecione o título para classificar pela versão.<br /><br /> **Tempo de execução**: a versão do .NET Framework no qual o componente é baseado. Selecione o título para classificar pela versão do runtime.<br /><br /> **Caminho**: o nome do arquivo do componente e o caminho onde ele está localizado. Selecione o título para classificar pelo caminho.|  
  
## <a name="see-also"></a>Consulte Também  
 [Analysis Services designers e caixas de diálogo &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Gerenciamento de assemblies de modelo multidimensional](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
