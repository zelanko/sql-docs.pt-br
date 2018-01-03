---
title: "Sobrepondo permissões de modelo e membro (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- models [Master Data Services], effective permissions
- permissions [Master Data Services], model and member overlaps
- members [Master Data Services], effective permissions
ms.assetid: 9fd7a555-43bf-4796-a8b6-1ca63a291216
caps.latest.revision: "7"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 02dfdc1e784696c5df1185867a435cc14693b4b2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="overlapping-model-and-member-permissions-master-data-services"></a>Sobrepondo permissões de modelo e membro (Serviços de Dados Mestre)
  A permissão atribuída a um membro pode sobrepor a permissão atribuída a um objeto de modelo. Quando ocorrem sobreposições, a permissão mais restritiva tem efeito.  
  
 Se um membro tiver uma permissão que seja diferente daquela correspondente ao objeto de modelo, as seguintes regras se aplicarão:  
  
-   **Negar** substitui todas as outras permissões.  
  
-   A permissão**Admin** no nível do Modelo substitui todas as outras permissões e é alterada para a permissão de acesso Todos (CRUD) nos subníveis.  
  
-   A permissão de acesso efetiva cruza as permissões dos membros e dos atributos.  
  
     Por exemplo, se as permissões do membro incluírem **Criar** e **Atualizar**, a permissão dos atributos será **Atualizar**. A permissão efetiva será **Atualizar**.  
  
 A imagem a seguir mostra quais permissões entram em vigor em um valor de atributo individual quando as permissões de atributo são diferentes das permissões de membro.  
  
 ![mds_conc_security_member_overlap_table](../master-data-services/media/mds-conc-security-member-overlap-table.gif "mds_conc_security_member_overlap_table")  
  
## <a name="example-1"></a>Exemplo 1  
 ![mds_conc_overlap_model_1](../master-data-services/media/mds-conc-overlap-model-1.gif "mds_conc_overlap_model_1")  
  
 Na guia **Modelos** , a entidade Produto tem a permissão **Atualizar** atribuída. Todos os atributos da entidade herdam essa permissão.  
  
 Na guia **Membros da Hierarquia** , o nó da subcategoria Mountain Bikes em uma hierarquia derivada tem a permissão **Atualizar** atribuída.  
  
 Resultado: no **Explorer**, o usuário tem a permissão **Atualizar** para todos os valores do atributo para todos os membros do nó Mountain Bikes. Todos os outros membros e atributos estão ocultados.  
  
 ![mds_conc_overlap_model_example_1](../master-data-services/media/mds-conc-overlap-model-example-1.gif "mds_conc_overlap_model_example_1")  
  
## <a name="example-2"></a>Exemplo 2  
 ![mds_conc_overlap_model_2](../master-data-services/media/mds-conc-overlap-model-2.gif "mds_conc_overlap_model_2")  
  
 Na guia **Modelos** , o atributo Subcategory tem a permissão **Atualizar** atribuída.  
  
 Na guia **Membros da Hierarquia** , o nó da subcategoria Mountain Bikes em uma hierarquia derivada recebe explicitamente a permissão **Leitura** .  
  
 Resultado: No **Explorer**, o usuário tem a permissão **Leitura** para os valores do atributo Subcategory para os membros no nó Mountain Bikes. Todos os outros membros e atributos estão ocultados.  
  
 ![mds_conc_overlap_model_example_2](../master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## <a name="example-3"></a>Exemplo 3  
 ![mds_conc_overlap_model_3](../master-data-services/media/mds-conc-overlap-model-3.gif "mds_conc_overlap_model_3")  
  
 Na guia **Modelos** , o atributo Subcategory tem a permissão **Leitura** atribuída.  
  
 Na guia **Membros da Hierarquia** , o nó da subcategoria Mountain Bikes em uma hierarquia derivada recebe explicitamente a permissão **Atualizar** .  
  
 Resultado: No **Explorer**, o usuário tem a permissão **Leitura** para os valores do atributo. Todos os outros membros e atributos estão ocultados.  
  
 ![mds_conc_overlap_model_example_2](../master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## <a name="see-also"></a>Consulte Também  
 [Como as permissões são determinadas &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)   
 [Sobrepondo permissões de usuário e grupo &#40;Master Data Services&#41;](../master-data-services/overlapping-user-and-group-permissions-master-data-services.md)  
  
  
