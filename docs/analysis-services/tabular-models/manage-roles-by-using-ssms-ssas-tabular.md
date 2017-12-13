---
title: "Gerenciar funções usando SSMS (SSAS Tabular) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 652faac0-1cfc-438b-8119-2f4b090a2381
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: af36d37d9cbbaa0554719fd97e22e193d08b696a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="manage-roles-by-using-ssms-ssas-tabular"></a>Gerenciar funções usando SSMS (SSAS tabular)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Você pode criar, editar e gerenciar funções para um modelo tabular implantado usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Tarefas neste tópico:  
  
-   [Para criar uma nova função](#bkmk_new_role)  
  
-   [Para copiar uma função](#bkmk_copy_role)  
  
-   [Para editar uma função](#bkmk_edit_role)  
  
-   [Para excluir uma função](#bkmk_deletet_role)  
  
> [!CAUTION]  
>  Reimplantar um projeto de modelo de tabela com funções definidas usando o Gerenciador de Função no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] substituirá as funções definidas em um modelo de tabela implantado.  
  
> [!CAUTION]  
>  Usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para gerenciar um banco de dados de espaço de trabalho de modelo de tabela enquanto o projeto de modelo está aberto no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] pode corromper o arquivo Model.bim. Ao criar e gerenciar funções para um banco de dados de espaço de trabalho de modelo de tabela, use o Gerenciador de Função no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
###  <a name="bkmk_new_role"></a> Para criar uma nova função  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o modelo de banco de dados de tabela para o qual você quer criar uma nova função, clique com o botão direito do mouse em **Funções**e, em seguida, clique em **Nova Função**.  
  
2.  Na caixa de diálogo **Criar Função** , na janela Selecionar uma página, clique em **Geral**.  
  
3.  Na janela de configurações gerais, no campo **Nome** , digite um nome para a função.  
  
     Por padrão, o nome da função padrão será numerado incrementalmente para cada nova função. É recomendado que você digite um nome que claramente identifique o tipo de membro, por exemplo, Gerentes Financeiros ou Especialistas de Recursos Humanos.  
  
4.  Em **Defina as permissões de banco de dados para essa função**, selecione uma das opções de permissão a seguir:  
  
    |Permissão|Description|  
    |----------------|-----------------|  
    |**Controle total (Administrador)**|Os membros podem fazer modificações ao esquema modelo e podem exibir todos os dados.|  
    |**Processar banco de dados**|Membros podem executar operações de Processar e Processar Tudo. Não é possível modificar o esquema modelo e não é possível exibir dados.|  
    |**Leitura**|Os membros têm permissão de exibir dados (com base em filtros de linha) mas não podem fazer nenhuma alteração ao esquema modelo.|  
  
5.  Na caixa de diálogo **Criar Função** , na janela Selecionar uma página, clique em **Associação**.  
  
6.  Na janela de configurações de associação, clique em **Adicionar**e, na caixa de diálogo **Selecionar Usuários ou Grupos** , adicione os usuários ou grupos do Windows que você deseja adicionar como membros.  
  
7.  Se a função que você está criando tem permissões de Leitura, você pode adicionar filtros de linha para qualquer tabela usando uma fórmula DAX. Para adicionar filtros de linha, no **propriedades da função - \<rolename >** na caixa **selecionar uma página**, clique em **filtros de linha**.  
  
8.  Na janela de filtros de linha, selecione uma tabela, clique no **filtro DAX** campo e, em seguida, o **filtro DAX - \<tablename >** , digite uma fórmula DAX.  
  
    > [!NOTE]  
    >  O filtro DAX - \<tablename > campo não contém um editor de consultas de preenchimento automático ou recurso de Inserir função. Para usar o Preenchimento Automático ao escrever uma fórmula DAX, você deverá usar um editor de fórmula DAX no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
9. Clique em **OK** para salvar a função.  
  
###  <a name="bkmk_copy_role"></a> Para copiar uma função  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o modelo de banco de dados de tabela que contém a função que você deseja copiar, expanda **Funções**e, em seguida, clique com o botão direito do mouse na função e clique em **Duplicar**.  
  
###  <a name="bkmk_edit_role"></a> Para editar uma função  
  
-   No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o modelo de banco de dados de tabela que contém a função que você deseja editar, expanda **Funções**e, em seguida, clique com o botão direito do mouse na função e clique em **Propriedades**.  
  
     No **propriedades de função** \<rolename > caixa de diálogo, você pode alterar as permissões, adicionar ou remover membros, e filtros de linha de adicionar/editar.  
  
###  <a name="bkmk_deletet_role"></a> Para excluir uma função  
  
-   No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o modelo de banco de dados de tabela que contém a função que você deseja excluir, expanda **Funções**e, em seguida, clique com o botão direito do mouse na função e clique em **Excluir**.  
  
## <a name="see-also"></a>Consulte também  
 [Funções &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
