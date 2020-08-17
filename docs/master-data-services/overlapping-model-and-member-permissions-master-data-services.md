---
description: Sobrepondo permissões de modelo e membro (Serviços de Dados Mestre)
title: Sobrepondo permissões de modelo e membro
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], effective permissions
- permissions [Master Data Services], model and member overlaps
- members [Master Data Services], effective permissions
ms.assetid: 9fd7a555-43bf-4796-a8b6-1ca63a291216
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d3de498043b5be0e6ad71a9e32b5abbc6db7ab21
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88343222"
---
# <a name="overlapping-model-and-member-permissions-master-data-services"></a>Sobrepondo permissões de modelo e membro (Serviços de Dados Mestre)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

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
  
  
