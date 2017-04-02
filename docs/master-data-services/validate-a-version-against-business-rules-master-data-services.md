---
title: "Validar uma vers&#227;o em rela&#231;&#227;o a regras de neg&#243;cio (Master Data Services) | Microsoft Docs"
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
  - "validando versões [Master Data Services]"
  - "validando versões [Master Data Services], sobre a validação de versões"
  - "versões [Master Data Services], validando"
  - "regras de negócios [Master Data Services], aplicando a todos os membros"
ms.assetid: 5aee7901-6d05-41d4-8bbb-c6f26791d1df
caps.latest.revision: 8
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 8
---
# Validar uma vers&#227;o em rela&#231;&#227;o a regras de neg&#243;cio (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], valide uma versão para aplicar regras de negócio a todos os membros da versão do modelo.  
  
 Este procedimento explica como usar o aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para validar dados. Se você tiver permissão no banco de dados MDS, poderá usar um procedimento armazenado no lugar. Para obter mais informações, consulte [Procedimento armazenado de validação &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md).  
  
> [!NOTE]  
>  Todos os membros deverão ser validados antes que uma versão possa ser confirmada.  
  
## Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Gerenciamento de Versões** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   O status da versão deve ser **Aberto** ou **Bloqueado**.  
  
-   Na página **Validar Versões**, os membros devem existir com um status diferente de **Validação bem-sucedida**.  
  
### Para validar uma versão  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Gerenciamento de Versões**.  
  
2.  Na página **Gerenciar Versões**, na barra de menus, clique em **Validar Versão**.  
  
3.  Na página **Validar Versões**, selecione o modelo e a versão que você deseja validar.  
  
4.  Clique em **Validar**.  
  
5.  Na caixa de diálogo de confirmação, clique em **OK**.  
  
    > [!NOTE]  
    >  Quando o indicador de progresso já não for exibido, isso significará que a versão concluiu a validação.  
  
## Próximas etapas  
  
-   [Bloquear uma versão &#40;Master Data Services&#41;](../master-data-services/lock-a-version-master-data-services.md)  
  
## Consulte também  
 [Status da validação &#40;Master Data Services&#41;](../master-data-services/validation-statuses-master-data-services.md)   
 [Procedimento armazenado de validação &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)   
 [Versões &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [Validar membros específicos em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
  