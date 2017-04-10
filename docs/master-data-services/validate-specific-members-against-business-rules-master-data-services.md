---
title: "Validar membros espec&#237;ficos em rela&#231;&#227;o a regras de neg&#243;cio (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "aplicando regras de negócio [Master Data Services]"
  - "regras de negócios [Master Data Services], aplicando a membros selecionados"
ms.assetid: 2288ef43-5392-47ea-b651-ec25e5692a14
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# Validar membros espec&#237;ficos em rela&#231;&#227;o a regras de neg&#243;cio (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], aplique regras de negócio seletivamente quando desejar atualizar ou validar subconjuntos de membros com base em regras de negócio.  
  
> [!NOTE]  
>  Se você deseja aplicar regras de negócio a todos os membros em uma versão de um modelo, consulte [Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md).  
  
## Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
-   Você deve ter, no mínimo, a permissão **Atualizar** para o objeto de modelo ao qual está aplicando regras de negócio.  
  
### Para aplicar regras de negócio seletivamente.  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], na lista suspensa **Modelo**, selecione um modelo.  
  
2.  Na lista suspensa **Versão**, selecione uma versão.  
  
3.  Clique na guia **Gerenciador** .  
  
4.  Na barra de menus, aponte para **Entidades** e clique no nome da entidade que contém os membros aos quais você deseja aplicar regras.  
  
5.  Clique em **Aplicar Regras**. As regras de negócio são aplicadas apenas aos membros exibidos na grade.  
  
## Consulte também  
 [Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)   
 [Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  