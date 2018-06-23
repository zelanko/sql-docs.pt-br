---
title: Atualizando dados (Suplemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 58dbe99a-288d-4f1c-9cd5-704d6836c945
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 126c696da22e2b3e483ae7fb4692469d617f125a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011774"
---
# <a name="refreshing-data-mds-add-in-for-excel"></a>Atualizando dados (suplemento MDS para Excel)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], atualize os dados quando desejar obter as informações mais recentes do repositório do MDS sem abrir uma nova planilha. Você pode atualizar todas as células ou uma seleção de células. Isso pode ser útil quando você insere colunas com fórmulas personalizadas ou outros dados que não são gerenciados no MDS e deseja preservá-los.  
  
## <a name="when-you-can-refresh-mds-managed-data"></a>Quando é possível atualizar dados gerenciados no MDS  
 Você pode atualizar dados gerenciados no MDS em uma planilha ativa quando a planilha ativa já contém dados gerenciados no MDS. Se você tiver alterado os valores dos atributos ou adicionado membros à planilha, será preciso publicar suas alterações antes de poder atualizar.  
  
## <a name="refreshing-a-selection"></a>Atualizando uma seleção  
 Você tem a opção de atualizar todas as células ou apenas as células selecionadas. As células selecionadas devem ser contíguas. Se um conjunto de células contíguas for selecionado, todas as células gerenciadas pelo MDS nesse conjunto serão atualizadas para exibir os valores atualmente armazenados no servidor. As linhas e colunas inalteradas que não forem gerenciadas pelo MDS não serão afetadas de nenhuma forma.  
  
## <a name="what-happens-when-you-refresh-mds-managed-data"></a>O que acontece ao atualizar dados gerenciados no MDS  
 Ao atualizar dados no [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], o que acontece aos dados gerenciados no MDS da planilha depende do que mudou no repositório do MDS desde a última vez que você carregou os dados.  
  
-   Se novos membros tiverem sido adicionados ao repositório, eles serão adicionados ao final da planilha e realçados em verde.  
  
-   Se membros forem excluídos do repositório, eles serão excluídos da planilha.  
  
-   Se um valor de atributo tiver sido alterado no repositório do MDS, o valor será atualizado na planilha com o valor do repositório do MDS. A cor de célula não mudará.  
  
> [!WARNING]  
>  -   Na planilha ativa, se houver dados não gerenciados nas linhas abaixo dos dados gerenciados no MDS, os dados não gerenciados poderão ser substituídos. Isso ocorre quando você atualiza a planilha e novas linhas de dados gerenciados no MDS, que substituem os dados não gerenciados, são adicionadas.  
> -   Ao atualizar, os comentários das células gerenciadas no MDS são excluídos.  
  
## <a name="how-to-refresh-mds-managed-data"></a>Como atualizar dados gerenciados no MDS  
 No grupo **Conectar e Carregar** na faixa de opções, o botão **Atualizar** tem duas opções: **Atualizar Tudo** e **Atualizar Seleção**. A ação padrão do botão de faixa de opções é **Atualizar Tudo**. Para atualizar a planilha inteira com os valores do servidor, clique no botão **Atualizar** ou escolha a opção **Atualizar Tudo** . Para atualizar somente algumas células de uma planilha, selecione as células (deve ser uma seleção contígua) e escolha a opção **Atualizar Seleção** .  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Crie uma conexão com um banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Conectar-se a um repositório do MDS &#40;Suplemento MDS para Excel&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|Carregue os dados do MDS no Excel.|[Carregar dados do MDS no Excel](export-data-to-excel-from-master-data-services.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Conexões &#40;Suplemento MDS para Excel&#41;](connections-mds-add-in-for-excel.md)  
  
-   [Carregando dados &#40;suplemento do MDS para Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [Suplemento do Master Data Services para Microsoft Excel](master-data-services-add-in-for-microsoft-excel.md)  
  
  