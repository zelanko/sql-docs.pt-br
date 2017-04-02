---
title: "Sobrepondo permiss&#245;es de modelo e membro (Servi&#231;os de Dados Mestre) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modelos [Master Data Services], permissões efetivas"
  - "permissões [Master Data Services], sobreposições do modelo e do membro"
  - "membros [Master Data Services], permissões efetivas"
ms.assetid: 9fd7a555-43bf-4796-a8b6-1ca63a291216
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# Sobrepondo permiss&#245;es de modelo e membro (Servi&#231;os de Dados Mestre)
  A permissão atribuída a um membro pode sobrepor a permissão atribuída a um objeto de modelo. Quando ocorrem sobreposições, a permissão mais restritiva tem efeito.  
  
 Se um membro tiver uma permissão que seja diferente daquela correspondente ao objeto de modelo, as seguintes regras se aplicarão:  
  
-   **Negar** substitui todas as outras permissões.  
  
-   **Admin** permissão no nível do modelo substitui todas as outras permissões e é alterado para permissão de acesso de todos os (CRUD) nos níveis de sub.  
  
-   A permissão de acesso efetiva cruza as permissões dos membros e dos atributos.  
  
     Por exemplo, se as permissões do membro incluírem **Criar** e **Atualizar**, a permissão dos atributos será **Atualizar**. A permissão efetiva será **Atualizar**.  
  
 A imagem a seguir mostra quais permissões entram em vigor em um valor de atributo individual quando as permissões de atributo são diferentes das permissões de membro.  
  
 ![mds_conc_security_member_overlap_table](../master-data-services/media/mds-conc-security-member-overlap-table.gif "mds_conc_security_member_overlap_table")  
  
## Exemplo 1  
 ![mds_conc_overlap_model_1](../master-data-services/media/mds-conc-overlap-model-1.gif "mds_conc_overlap_model_1")  
  
 Na guia **Modelos** , a entidade Produto tem a permissão **Atualizar** atribuída. Todos os atributos da entidade herdam essa permissão.  
  
 Na guia **Membros da Hierarquia** , o nó da subcategoria Mountain Bikes em uma hierarquia derivada tem a permissão **Atualizar** atribuída.  
  
 Resultado: no **Explorer**, o usuário tem a permissão **Atualizar** para todos os valores do atributo para todos os membros do nó Mountain Bikes. Todos os outros membros e atributos estão ocultados.  
  
 ![mds_conc_overlap_model_example_1](../master-data-services/media/mds-conc-overlap-model-example-1.gif "mds_conc_overlap_model_example_1")  
  
## Exemplo 2  
 ![mds_conc_overlap_model_2](../master-data-services/media/mds-conc-overlap-model-2.gif "mds_conc_overlap_model_2")  
  
 Na guia **Modelos** , o atributo Subcategory tem a permissão **Atualizar** atribuída.  
  
 Na guia **Membros da Hierarquia** , o nó da subcategoria Mountain Bikes em uma hierarquia derivada recebe explicitamente a permissão **Leitura** .  
  
 Resultado: No **Explorer**, o usuário tem a permissão **Leitura** para os valores do atributo Subcategory para os membros no nó Mountain Bikes. Todos os outros membros e atributos estão ocultados.  
  
 ![mds_conc_overlap_model_example_2](../master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## Exemplo 3  
 ![mds_conc_overlap_model_3](../master-data-services/media/mds-conc-overlap-model-3.gif "mds_conc_overlap_model_3")  
  
 Na guia **Modelos** , o atributo Subcategory tem a permissão **Leitura** atribuída.  
  
 Na guia **Membros da Hierarquia** , o nó da subcategoria Mountain Bikes em uma hierarquia derivada recebe explicitamente a permissão **Atualizar** .  
  
 Resultado: No **Explorer**, o usuário tem a permissão **Leitura** para os valores do atributo. Todos os outros membros e atributos estão ocultados.  
  
 ![mds_conc_overlap_model_example_2](../master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## Consulte também  
 [Como as permissões são determinadas & #40. Master Data Services & 41;](../master-data-services/how-permissions-are-determined-master-data-services.md)   
 [Sobreposição de usuário e permissões de grupo e 40; Master Data Services & 41;](../master-data-services/overlapping-user-and-group-permissions-master-data-services.md)  
  
  