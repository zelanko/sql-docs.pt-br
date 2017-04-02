---
title: "Exibir erros que ocorrem durante o preparo (Master Data Services) | Microsoft Docs"
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
  - "processo de preparo [Master Data Services], exibindo erros"
ms.assetid: 6d2bff84-624b-47fc-a4a5-d9ea01d13412
caps.latest.revision: 8
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 8
---
# Exibir erros que ocorrem durante o preparo (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode exibir os erros ocorridos durante o processo de preparo. No banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , há duas exibições que mostram erros:  
  
-   stg.viw_name_MemberErrorDetails para atualizações de membro folha ou consolidado.  
  
-   stg.viw_name_RelationshipErrorDetails para atualizações de relação de hierarquia.  
  
## Pré-requisitos  
 Para executar esse procedimento:  
  
-   No banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você deve ter permissões SELECT para a exibição stg.viw_name_MemberErrorDetails ou stg.viw_name_RelationshipErrorDetails.  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### Para exibir erros de preparo  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e conecte-se à instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] de seu banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
2.  Abra uma nova consulta.  
  
3.  Digite o texto a seguir, substituindo name pelo nome de sua tabela de preparo, por exemplo, viw_Product_MemberErrorDetails.  
  
     `SELECT * FROM stg.viw_name_MemberErrorDetails`  
  
4.  Execute a consulta. Os detalhes do erro são exibidos no campo **ErrorDescription** .  
  
## Próximas etapas  
 Para obter mais detalhes sobre mensagens de erro, consulte [Erros de processo de preparo &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md).  
  
## Consulte também  
 [Visão geral: Importando dados de tabelas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [Solucionando problemas do processo de preparo (Master Data Services)](http://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-the-staging-process-master-data-services.aspx)  
  
  