---
title: Criar e gerenciar funções (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.rolemanager.f1
- sql12.asvs.bidtoolset.roledb.f1
ms.assetid: e23d27a8-e968-4082-9dbe-963fc724b5d9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 10e5e26142cd1819e4f2c5f884af9c2f2af10812
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67284901"
---
# <a name="create-and-manage-roles-ssas-tabular"></a>Criar e Gerenciar Funções (SSAS tabular)
  Funções, em modelos tabulares, definem permissões de membro para um modelo. As funções são definidas para um projeto de modelo usando a caixa de diálogo Gerenciador de Funções no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Quando um modelo é implantado, os administradores de banco de dados podem gerenciar funções usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 As tarefas neste tópico descrevem como criar e gerenciar funções durante a criação do modelo usando a caixa de diálogo Gerenciador de Funções no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para obter informações sobre como gerenciar as funções em um modelo de banco de dados implantado, consulte [Funções de modelo tabular &#40;SSAS Tabular&#41;](roles-ssas-tabular.md).  
  
## <a name="tasks"></a>Tarefas  
 Para criar, editar, copiar e excluir funções, você usará a caixa de diálogo **Gerenciador de Funções** . Para exibir a caixa de diálogo **Gerenciador de Funções** , no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Gerenciador de Funções**.  
  
###  <a name="bkmk_new_role"></a>Para criar uma nova função  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Gerenciador de Funções**.  
  
2.  Na caixa de diálogo **Gerenciador de Funções** , clique em **Novo**.  
  
     Uma nova função realçada é adicionada à lista de Funções.  
  
3.  Na lista de **Funções** , no campo **Nome** , digite um nome para a função.  
  
     Por padrão, o nome da função padrão será numerado incrementalmente para cada nova função. É recomendado que você digite um nome que claramente identifique o tipo de membro, por exemplo, Gerentes Financeiros ou Especialistas de Recursos Humanos.  
  
4.  No campo **Permissões** , clique na seta para baixo e selecione um dos tipos de permissão a seguir:  
  
    |Permissão|DESCRIÇÃO|  
    |----------------|-----------------|  
    |**Nenhuma**|Os membros não podem fazer modificações ao esquema modelo e não podem consultar dados.|  
    |**Ler**|Os membros têm permissão de consultar dados (com base em filtros de linha) mas não podem fazer nenhuma alteração ao esquema modelo.|  
    |**Leitura e processo**|Os membros têm permissão de consultar dados (com base em filtros de nível de linha) e executar operações de Processar e Processar Tudo, mas não podem fazer nenhuma alteração ao esquema modelo.|  
    |**Processo**|Os membros podem executar as operações Processar e Processar Tudo. Não podem modificar o esquema do modelo e não podem consultar dados.|  
    |**Administradores**|Os membros podem fazer modificações ao esquema modelo e podem consultar todos os dados.|  
  
5.  Para inserir uma descrição para a função, clique no campo **Descrição** e digite uma descrição.  
  
6.  Se a função que você está criando tem permissão de Leitura ou Leitura e Processamento, você pode adicionar filtros de linha usando uma fórmula DAX. Para adicionar filtros de linha, clique na guia **Filtros de Linha** , selecione uma tabela, clique no campo **Filtro DAX** e digite uma fórmula DAX.  
  
7.  Para adicionar membros à função, clique na guia **Membros** e clique em **Adicionar**.  
  
    > [!NOTE]  
    >  Os membros de função também podem ser adicionados a um modelo implantado usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [Gerenciar funções usando SSMS &#40;SSAS Tabular&#41;](manage-roles-by-using-ssms-ssas-tabular.md).  
  
8.  Na caixa de diálogo **Selecionar Usuários ou Grupos** , insira os objetos usuário do Windows ou grupo do Windows como membros.  
  
9. Clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;SSAS de tabela&#41;](roles-ssas-tabular.md)   
 [Perspectivas &#40;SSAS de tabela&#41;](perspectives-ssas-tabular.md)   
 [Analisar no Excel &#40;SSAS de tabela&#41;](analyze-in-excel-ssas-tabular.md)   
 [Função de nome de usuário &#40;DAX&#41;](/dax/username-function-dax)   
 [Função CUSTOMDATA &#40;DAX&#41;](/dax/customdata-function-dax)  
  
  
