---
title: "Criar um local confiável para sites do Power Pivot na Administração Central | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a666f365-cd93-43a3-9d3d-e429dfc19b66
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9f2913ee3aa26a01a704fbdd94a4d01b7044f73a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-trusted-location-for-power-pivot-sites-in-central-administration"></a>Criar um local confiável para sites do Power Pivot na Administração Central
  Os Serviços do Excel permitem especificar quais locais são repositórios válidos para pastas de trabalho que você abrir em um servidor do SharePoint. Esses locais são chamados de "locais confiáveis" e você pode usar diferentes definições de configuração para cada local confiável que você criar. Para uma implantação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, você pode considerar criar um local confiável para sites que tenham pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , de forma que você possa aplicar as configurações que funcionam melhor para acesso a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , enquanto preserva valores padrão para o resto do farm.  
  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você deve ser um farm ou administrador de serviço para designar uma URL como um local confiável.  
  
 Você deve saber o endereço da URL do site do SharePoint que contém a Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou outra biblioteca que armazena suas pastas de trabalho. Para obter o endereço, abra o site que contém a biblioteca, clique com o botão direito do mouse em **Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**, selecione **Propriedades** e copie a primeira parte do Endereço (URL) que contém o nome do servidor e o caminho do site.  
  
##  <a name="overview"></a> Visão geral  
 Uma instalação inicial de Serviços do Excel especifica 'http://' como seu local confiável, o que significa que podem ser abertas pastas de trabalho de qualquer site no farm no servidor. Se você precisar de mais controle sobre quais locais são considerados confiáveis, você poderá criar novos locais confiáveis que sejam mapeados para sites específicos em seu farm e então variar as configurações e permissões para cada um.  
  
 Criar um novo local confiável para sites que hospedam pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é especialmente útil se você deseja preservar valores padrão para o resto do farm, aplicando configurações diferentes que funcionam melhor para acesso a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Por exemplo, um local confiável que é otimizado para pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] poderia ter um tamanho de pasta de trabalho máximo de 50 MB, enquanto o resto do farm usa o valor padrão de 10 MB.  
  
 Criar um local confiável será recomendado se você estiver usando bibliotecas da Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para visualizar pastas de trabalho publicadas e encontrar avisos de atualização de dados em vez da imagem de visualização esperada. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] A Galeria renderiza imagens em miniatura de relatórios e pastas de trabalho que usam dados e informações de apresentação dentro do documento. Se Avisar ao Atualizar Dados estiver habilitado para um local confiável, a Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] talvez não tenha permissões suficientes para executar a atualização, levando ao aparecimento de um erro em vez da imagem em miniatura. Adicionar um site que tenha a Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] como um novo local confiável pode eliminar esse problema.  
  
##  <a name="create"></a> Criar um local confiável para acesso a dados do Power Pivot  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Clique no Aplicativo de Serviço de Serviços do Excel.  
  
3.  Clique em **Locais de Arquivos Confiáveis**.  
  
4.  Clique em **Adicionar Local de Arquivo Confiável**.  
  
5.  Digite a URL de um site que contenha uma biblioteca da Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
6.  Em Tipo de Local, selecione **Microsoft SharePoint Foundation**.  
  
    > [!IMPORTANT]  
    >  Os tipos de local UNC e HTTP não têm suporte para acesso a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
7.  Aceite todas as configurações padrão de propriedades em Gerenciamento de Sessão, Propriedades da Pasta de trabalho e Comportamento de Cálculo.  
  
8.  Em Propriedades da Pasta de Trabalho, defina **Tamanho Máximo da Pasta de Trabalho** como **50**. Isto alinha o limite superior para tamanho de arquivo de pasta de trabalho com o limite superior para carregamentos de arquivo para o aplicativo de site pai. Se suas pastas de trabalho forem maiores que 50 megabytes, você deverá aumentar o limite de tamanho de arquivo. Para obter mais informações, consulte [Configurar o tamanho máximo de upload de arquivo &#40;Power Pivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).  
  
9. Em Dados Externos, verifique se Permitir Dados Externos está definido como **Bibliotecas de conexões de dados confiáveis e incorporadas**. Essa configuração é necessária para o acesso a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em uma pasta de trabalho.  
  
10. Também em Dados Externos, para Aviso de Atualização, desmarque a caixa de seleção **Aviso de atualização habilitado**. Desmarcar a caixa de seleção permite que a Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ignore mensagens de aviso rotineiras e, no lugar, mostre imagens de visualização de uma pasta de trabalho.  
  
11. Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Galeria do Power Pivot](http://msdn.microsoft.com/library/2a0db616-e08e-4062-aac8-979f8cad7794)   
 [Criar e personalizar a Galeria do Power Pivot](../../analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery.md)   
 [Usar a Galeria Power Pivot](../../analysis-services/power-pivot-sharepoint/use-power-pivot-gallery.md)  
  
  

