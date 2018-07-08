---
title: Barra de ferramentas (guia navegador, Designer de dimensão) (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d0abb2a7-e981-4b0a-a442-80c819aca2ae
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cb561ed65f629879f48aa8c47cf470dfecedff74
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37192367"
---
# <a name="toolbar-browser-tab-dimension-designer-analysis-services---multidimensional-data"></a>Barra de Ferramentas (guia Navegador, Designer de Dimensão) (Analysis Services - Dados Multidimensionais)
  Use o painel **Barra de Ferramentas** para executar operações comuns na guia **Navegador** do **Designer de Dimensão**.  
  
## <a name="options"></a>Opções  
 **Processar**  
 Clique para abrir a caixa de diálogo **Processo** e processar a dimensão selecionada.  
  
 **Reconectar-se**  
 Clique para reconectar a guia **Navegador** com a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e com o banco de dados que contém a dimensão se a sessão da guia **Navegador** for desconectada devido a perda ou tempo limite de conexão.  
  
 **Atualizar**  
 Clique para recarregar a guia **Navegador** com dados e metadados da dimensão.  
  
 **Propriedades do membro**  
 Clique para exibir e selecionar propriedades do membro a serem exibidas no painel **Nível e Membros** . Selecionar **(Mostrar Tudo)** exibe todas as propriedades dos membros listados.  
  
 Cada propriedade do membro selecionada em **Propriedades do Membro** é exibida em **Nível e Membros** como uma coluna separada, para permitir a edição dos valores de propriedade do membro em modo de write-back.  
  
 **Filtrar membros**  
 Clique para exibir a caixa de diálogo **Filtrar Membros** e filtrar os membros exibidos em **Nível e Membros** na hierarquia selecionada.  
  
 **Write-back**  
 Selecione para definir o painel **Nível e Membros** em modo de write-back de dimensão.  
  
 **Diminuir Recuo**  
 Clique para tornar o membro selecionado em **Nível e Membros** um irmão de seu membro pai.  
  
> [!NOTE]  
>  Esta opção será habilitada somente se o modo de write-back for habilitado.  
  
 **Aumentar recuo**  
 Clique para tornar o membro selecionado em **Nível e Membros** um filho do irmão que precede imediatamente o membro selecionado.  
  
> [!NOTE]  
>  Esta opção será habilitada somente se o modo de write-back for habilitado.  
  
 **Hierarchy**  
 Selecione a hierarquia por meio da qual serão exibidos os membros no painel **Nível e Membros** .  
  
 **Idioma**  
 Selecione a linguagem usada para exibir membros no painel **Nível e Membros** .  
  
 Se for selecionado um idioma para o qual não foi definida uma conversão, o idioma padrão será usado para exibir membros no painel **Nível e Membros** . Porém, o modo de write-back será desabilitado se for selecionada uma linguagem para a qual não foi definida uma conversão.  
  
  
