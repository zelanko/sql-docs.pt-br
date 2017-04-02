---
title: "Excluir uma regra de neg&#243;cio (Master Data Services) | Microsoft Docs"
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
  - "excluindo regras de negócio [Master Data Services]"
  - "regras de negócio [Master Data Services], excluindo"
ms.assetid: b97aa4f9-569f-451d-ad62-65b81f980299
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# Excluir uma regra de neg&#243;cio (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], exclua uma regra de negócio quando ela não for mais necessária.  
  
> [!NOTE]  
>  Você pode evitar a validação de dados em relação a uma regra de negócio excluindo-a. Para obter mais informações, consulte [Excluir uma regra de negócio &#40;Master Data Services&#41;](../master-data-services/exclude-a-business-rule-master-data-services.md).  
  
## Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### Para excluir uma regra de negócio  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Regras de Negócios**.  
  
3.  Na página **Regras de Negócio**, na lista suspensa **Modelo**, selecione um modelo.  
  
4.  Na lista suspensa **Entidade**, escolha uma entidade.  
  
5.  Na lista suspensa **Tipos de Membro**, selecione um tipo de membro ao qual a regra de negócio será aplicada.  
  
6.  Na grade, clique na linha da regra de negócios que você deseja excluir.  
  
7.  Clique em **Excluir**.  
  
8.  Na caixa de diálogo de confirmação, clique em **OK**. O valor da coluna **Estado da Regra de Negócios** é **Exclusão pendente**.  
  
9. Clique em **Publicar Tudo**.  
  
10. Na caixa de diálogo de confirmação, clique em **OK**. A regra de negócio excluída não é mais exibida na grade.  
  
## Consulte também  
 [Excluir uma regra de negócio &#40;Master Data Services&#41;](../master-data-services/exclude-a-business-rule-master-data-services.md)   
 [Criar e publicar uma regra de negócio &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  