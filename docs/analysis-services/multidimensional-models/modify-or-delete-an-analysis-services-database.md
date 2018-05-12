---
title: Modificar ou excluir um banco de dados do Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 44952f477cf16a169ad96f2bfe881b16ee9738da
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="modify-or-delete-an-analysis-services-database"></a>Modificar ou excluir um banco de dados do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  É possível alterar o nome e a descrição de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] antes da implantação no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e depois da implantação no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Também é possível ajustar configurações adicionais de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , dependendo do ambiente.  
  
> [!NOTE]  
>  Não é possível alterar as propriedades do banco de dados usando o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo online.  
  
## <a name="modifying-databases-using-sql-server-management-studio"></a>Modificando banco de dados usando o SQL Server Management Studio  
 Uma vez implantado o banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você pode usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para alterar o modo de representação usado pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ao se conectar com as fontes de dados contidas no banco de dados. O modo de representação permite que você especifique o contexto de segurança usado pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ao tentar conectar-se com uma fonte de dados para fins de processamento, navegação ou detalhamento.  
  
## <a name="modifying-databases-using-sql-server-data-tools"></a>Modificando banco de dados usando as Ferramentas de Dados do SQL Server  
 Use o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo de projeto para modificar as traduções de legenda e a descrição de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usado para definir um banco de dados. Para obter mais informações sobre como usar traduções em um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , consulte [Cenários de globalização para Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md).  
  
 Também é possível definir alises e funções de agregação associados a tipos de contas usados pelos atributos de conta em dimensões contidas no banco de dados. Os aliases permitem a seleção da terminologia específica do ramo usada pela empresa para os tipos de contas do plano de contas. Os tipos de conta são usados pelos membros de um atributo de conta para indicar como agregar medidas em cada membro usando as funções de agregação especificadas para cada tipo de conta existente no banco de dados. Para obter mais informações sobre os atributos de conta, consulte [Atributos e hierarquias de atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md).  
  
## <a name="deleting-databases"></a>excluindo bancos de dados  
 A exclusão de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] exclui o banco de dados e todos os seus cubos, dimensões e modelos de mineração. É possível excluir um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] somente no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-delete-an-analysis-services-database"></a>Para excluir um banco de dados do Analysis Services  
  
1.  Conecte-se a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  No **Pesquisador de Objetos**, expanda o nó da instância conectada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e verifique se o objeto a ser excluído está visível.  
  
3.  Clique com o botão direito do mouse no objeto a ser excluído e selecione **Excluir**.  
  
4.  Na caixa de diálogo **Excluir Objeto** , clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Documentar e gerar scripts de um banco de dados do Analysis Services](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md)  
  
  
