---
title: Exigir valores de atributos (Master Data Services) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- business rules [Master Data Services], requiring attribute values
- attributes [Master Data Services], requiring values
ms.assetid: a360ef13-0c34-43b8-a87e-2f5d8732d30e
caps.latest.revision: 9
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: c80f990580f849dcee4038ec0ca45ea1c18ffff5
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="require-attribute-values-master-data-services"></a>Exigir valores de atributos (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], solicite valores de atributos quando desejar se certificar de que os dados mestres estejam completos.  
  
> [!NOTE]  
>  Os membros que não possuírem valores de atributos baseados em domínio não serão exibidos em hierarquias derivadas baseadas nessas relações.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-require-attribute-values"></a>Para solicitar valores de atributos  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Regras de Negócios**.  
  
3.  Na página **Regras de Negócio** , na lista suspensa **Modelo** , selecione um modelo.  
  
4.  Na lista suspensa **Entidade** , escolha uma entidade.  
  
5.  Na lista suspensa **Tipo de Membro** , selecione um tipo de membro para aplicar a regra de negócio.  
  
6.  Clique em **Adicionar**.  
  
7.  Na caixa **Nome** , digite um nome para a regra de negócios.  
  
8.  Opcionalmente, no campo **Descrição** , digite a descrição da regra de negócios.  
  
9. Abaixo do bloco **Então** , clique em **Adicionar**. Um painel será exibido.  
  
10. Na lista suspensa **Operador** , selecione **ação necessária**.  
  
11. Na lista suspensa **Atributo** , selecione um atributo.  
  
12. Clique em **Salvar**. A nova linha será adicionada à grade **Então** .  
  
13. Clique em **Salvar**.  
  
14. Clique em **Publicar Tudo**.  
  
15. Na caixa de diálogo de confirmação, clique em **OK**. O valor da coluna **Estado da Regra de Negócios** é **Ativa**.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   Aplique regras de negócio a dados seguindo um destes procedimentos:  
  
    -   [Validar membros específicos em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [Hierarquias derivadas &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  
