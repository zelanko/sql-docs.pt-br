---
title: Criar e gerenciar funções | Microsoft Docs
ms.date: 09/17/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: daeef8b6d8b6953e33605816940f81ec04e0d5ab
ms.sourcegitcommit: aa9d2826e3c451f4699c0e69c9fcc8a2781c6213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/17/2018
ms.locfileid: "45975665"
---
# <a name="create-and-manage-roles"></a>Criar e gerenciar funções 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Funções, em modelos tabulares, definem permissões de membro para um modelo. As funções são definidas para um projeto de modelo usando a caixa de diálogo Gerenciador de Funções no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. 

> [!IMPORTANT]
> Se você estiver implantando seu projeto ao Azure Analysis Services, use **espaço de trabalho integrado** como seu banco de dados do espaço de trabalho. Para obter mais informações, consulte [banco de dados do espaço de trabalho](workspace-database-ssas-tabular.md).
  
 As tarefas neste artigo descrevem como criar e gerenciar funções durante a criação de modelo usando a caixa de diálogo Gerenciador de funções no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para obter informações sobre como gerenciar funções em um banco de dados modelo implantado, consulte [funções de modelo Tabular](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md).  
  
## <a name="tasks"></a>Tarefas  
 Para criar, editar, copiar e excluir funções, você usará a caixa de diálogo **Gerenciador de Funções** . Para exibir a caixa de diálogo **Gerenciador de Funções** , no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Gerenciador de Funções**.  
  
###  <a name="bkmk_new_role"></a> Para criar uma nova função  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Gerenciador de Funções**.  
  
2.  Na caixa de diálogo **Gerenciador de Funções** , clique em **Novo**.  
  
     Uma nova função realçada é adicionada à lista de Funções.  
  
3.  Na lista de **Funções** , no campo **Nome** , digite um nome para a função.  
  
     Por padrão, o nome da função padrão será numerado incrementalmente para cada nova função. É recomendado que você digite um nome que claramente identifique o tipo de membro, por exemplo, Gerentes Financeiros ou Especialistas de Recursos Humanos.  
  
4.  No campo **Permissões** , clique na seta para baixo e selecione um dos tipos de permissão a seguir:  
  
    |Permissão|Description|  
    |----------------|-----------------|  
    |**Nenhuma**|Os membros não podem fazer modificações ao esquema modelo e não podem consultar dados.|  
    |**Leitura**|Os membros têm permissão de consultar dados (com base em filtros de linha) mas não podem fazer nenhuma alteração ao esquema modelo.|  
    |**Leitura e processo**|Os membros têm permissão de consultar dados (com base em filtros de nível de linha) e executar operações de Processar e Processar Tudo, mas não podem fazer nenhuma alteração ao esquema modelo.|  
    |**Processar**|Membros podem executar operações de Processar e Processar Tudo. Não é possível modificar o esquema modelo e não é possível consultar dados.|  
    |**Administrador**|Os membros podem fazer modificações ao esquema modelo e podem consultar todos os dados.|  
  
5.  Para inserir uma descrição para a função, clique no campo **Descrição** e digite uma descrição.  
  
6.  Se a função que você está criando tem permissão de Leitura ou Leitura e Processamento, você pode adicionar filtros de linha usando uma fórmula DAX. Para adicionar filtros de linha, clique na guia **Filtros de Linha** , selecione uma tabela, clique no campo **Filtro DAX** e digite uma fórmula DAX.  
  
7.  Para adicionar membros à função, clique na guia **Membros** e clique em **Adicionar**.  
  
    > [!NOTE]  
    >  Os membros de função também podem ser adicionados a um modelo implantado usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [gerenciar funções usando SSMS](../../analysis-services/tabular-models/manage-roles-by-using-ssms-ssas-tabular.md).  
  
8.  Na caixa de diálogo **Selecionar Usuários ou Grupos** , insira os objetos usuário do Windows ou grupo do Windows como membros.  
  
9. Clique em **OK**.  
  
## <a name="see-also"></a>Confira também  
 [Funções](../../analysis-services/tabular-models/roles-ssas-tabular.md)   
 [Perspectivas](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Analisar no Excel](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)   
 [Função USERNAME (DAX)](http://msdn.microsoft.com/en-us/22dddc4b-1648-4c89-8c93-f1151162b93f)   
 [Função CUSTOMDATA (DAX)](http://msdn.microsoft.com/en-us/58235ad8-226c-43cc-8a69-5a52ac19dd4e)  
  
  
