---
title: Exigir valores de atributos (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], requiring attribute values
- attributes [Master Data Services], requiring values
ms.assetid: a360ef13-0c34-43b8-a87e-2f5d8732d30e
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c635c6083c42be3d1e3eb84afc8f188b0bdf94a5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52761398"
---
# <a name="require-attribute-values-master-data-services"></a>Exigir valores de atributos (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], solicite valores de atributos quando desejar se certificar de que os dados mestres estejam completos.  
  
> [!NOTE]  
>  Os membros que não possuírem valores de atributos baseados em domínio não serão exibidos em hierarquias derivadas baseadas nessas relações.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-require-attribute-values"></a>Para solicitar valores de atributos  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Regras de Negócios**.  
  
3.  Na página **Manutenção de Regra de Negócio** , na lista **Modelo** , selecione um modelo.  
  
4.  Na lista **Entidade** , selecione uma entidade.  
  
5.  Na lista **Tipo de Membro** , selecione um tipo de membro ao qual a regra de negócio será aplicada.  
  
6.  Na lista **Atributo** , selecione um atributo ou deixe o valor padrão **Todos**.  
  
7.  Clique em **Adicionar regra de negócio**.  
  
8.  Clique em **Editar regra de negócio selecionada**.  
  
9. No painel **Componentes** , expanda o nó **Ações** .  
  
10. Clique em **é necessário** e arraste-o para o **, em seguida,** do painel **ação** rótulo.  
  
11. No painel **Atributos** , clique em um atributo e arraste-o até o rótulo **Selecionar atributo** do painel **Editar Ação** .  
  
12. No painel **Editar Ação** , clique em **Salvar item**.  
  
13. Clique em **Voltar**.  
  
14. Opcionalmente, na página **Manutenção de Regra de Negócio** , na linha que contém sua regra de negócio, clique duas vezes em uma célula da coluna **Nome**, **Descrição**ou **Notificação** para atualizar o valor.  
  
15. Clique em **Publicar regras de negócio**.  
  
16. Na caixa de diálogo de confirmação, clique em **OK**. O status da regra mudará para **Ativo**.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   Aplique regras de negócio a dados seguindo um destes procedimentos:  
  
    -   [Validar membros específicos em relação a regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [Hierarquias derivadas &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)  
  
  
