---
title: Criar um local confiável para sites do PowerPivot na administração central | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a666f365-cd93-43a3-9d3d-e429dfc19b66
author: minewiskan
ms.author: owend
ms.openlocfilehash: 104d9dedafafedce505f63a9b8c17291d631ca54
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84540598"
---
# <a name="create-a-trusted-location-for-powerpivot-sites-in-central-administration"></a>Create a trusted location for PowerPivot sites in Central Administration
  Os Serviços do Excel permitem especificar quais locais são repositórios válidos para pastas de trabalho que você abrir em um servidor do SharePoint. Esses locais são chamados de "locais confiáveis" e você pode usar diferentes definições de configuração para cada local confiável que você criar. Para uma implantação do PowerPivot para SharePoint, você pode considerar criar um local confiável para sites que tenham pastas de trabalho PowerPivot, de forma que você possa aplicar as configurações que funcionam melhor para acesso a dados PowerPivot, enquanto preserva valores padrão para o resto do farm.  
  
  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você deve ser um farm ou administrador de serviço para designar uma URL como um local confiável.  
  
 Você deve saber o endereço da URL do site do SharePoint que possui a Galeria de Relatórios PowerPivot ou outra biblioteca que armazenar suas pastas de trabalho. Para obter o endereço, abra o site que contém a biblioteca, clique com o botão direito do mouse em **Galeria PowerPivot**, selecione **Propriedades**e, em seguida, copie a primeira parte do endereço (URL) que contém o nome do servidor e o caminho do site.  
  
##  <a name="overview"></a><a name="overview"></a> Visão geral  
 Uma instalação inicial de Serviços do Excel especifica 'http://' como seu local confiável, o que significa que podem ser abertas pastas de trabalho de qualquer site no farm no servidor. Se você precisar de mais controle sobre quais locais são considerados confiáveis, você poderá criar novos locais confiáveis que sejam mapeados para sites específicos em seu farm e então variar as configurações e permissões para cada um.  
  
 Criar um novo local confiável em Serviços do Excel para sites que hospedam pastas de trabalho PowerPivot é especialmente útil se você deseja preservar valores padrão para o resto do farm, aplicando configurações diferentes que funcionam melhor para acesso a dados PowerPivot. Por exemplo, um local confiável que é otimizado para pastas de trabalho do PowerPivot poderia ter um tamanho de pasta de trabalho máximo de 50 MB, enquanto o resto do farm usa o valor padrão de 10 MB.  
  
 Criar um local confiável é recomendado se você está usando bibliotecas da Galeria PowerPivot para visualizar pastas de trabalho publicadas, e você encontra avisos de atualização de dados em vez da imagem de visualização esperada. A Galeria PowerPivot renderiza imagens em miniatura de relatórios e pastas de trabalho que usam dados e informações de apresentação dentro do documento. Se Avisar ao Atualizar Dados estiver habilitado para um local confiável, a Galeria PowerPivot talvez não tenha permissões suficientes para executar a atualização, levando ao aparecimento de um erro em vez da imagem em miniatura. Adicionar um site que tenha a Galeria PowerPivot como um novo local confiável pode eliminar esse problema.  
  
##  <a name="create-a-trusted-location-for-powerpivot-data-access"></a><a name="create"></a>Criar um local confiável para acesso a dados PowerPivot  
  
1.  Na administração central, em gerenciamento de aplicativos, clique em **gerenciar aplicativos de serviço**.  
  
2.  Clique no Aplicativo de Serviço de Serviços do Excel.  
  
3.  Clique em **Locais de Arquivos Confiáveis**.  
  
4.  Clique em **Adicionar Local de Arquivo Confiável**.  
  
5.  Digite a URL de um site que contém uma biblioteca da Galeria PowerPivot.  
  
6.  Em Tipo de Local, selecione **Microsoft SharePoint Foundation**.  
  
    > [!IMPORTANT]  
    >  Os tipos de local UNC e HTTP não são compatíveis para acesso de dados PowerPivot.  
  
7.  Aceite todas as configurações padrão de propriedades em Gerenciamento de Sessão, Propriedades da Pasta de trabalho e Comportamento de Cálculo.  
  
8.  Em Propriedades da Pasta de Trabalho, defina **Tamanho Máximo da Pasta de Trabalho** como **50**. Isto alinha o limite superior para tamanho de arquivo de pasta de trabalho com o limite superior para carregamentos de arquivo para o aplicativo de site pai. Se suas pastas de trabalho forem maiores que 50 megabytes, você deverá aumentar o limite de tamanho de arquivo. Para obter mais informações, consulte [Configurar o tamanho máximo de upload de arquivo &#40;PowerPivot para SharePoint&#41;](configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).  
  
9. Em Dados Externos, verifique se Permitir Dados Externos está definido como **Bibliotecas de conexões de dados confiáveis e incorporadas**. Essa configuração é necessária para o acesso a dados PowerPivot em uma pasta de trabalho.  
  
10. Também em Dados Externos, para Aviso de Atualização, desmarque a caixa de seleção **Aviso de atualização habilitado**. Desmarcar a caixa de seleção permite que a Galeria PowerPivot ignore mensagens de aviso rotineiras e, no lugar, mostre imagens de visualização de apresentação de uma pasta de trabalho.  
  
11. Clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Galeria PowerPivot](../../2014-toc/index.yml)  
 [Criar e personalizar a galeria do PowerPivot](create-and-customize-power-pivot-gallery.md)   
 [Usar a Galeria PowerPivot](use-power-pivot-gallery.md)  
  
  
