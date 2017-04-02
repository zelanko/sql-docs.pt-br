---
title: "Criar um membro consolidado (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "04/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "criando membros consolidados [Master Data Services]"
  - "membros [Master Data Services], criando membros consolidados"
  - "membros consolidados [Master Data Services], criando"
ms.assetid: 431ab2d2-5517-4372-9980-142b05427c08
caps.latest.revision: 12
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 11
---
# Criar um membro consolidado (Master Data Services)
  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], crie um membro consolidado quando você desejar um nó pai para uma hierarquia explícita. Se você quiser adicionar dados em massa, use as tabelas de preparo. Para obter mais informações, consulte [Importar dados de tabelas &#40;Master Data Services&#41;](../master-data-services/import-data-from-tables-master-data-services.md).  
  
## Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
-   Você deve ter, no mínimo, a permissão **Atualização** para o objeto de modelo consolidado para a entidade à qual você está adicionando um membro, bem como **Criar permissão** para o Tipo Consolidado na entidade.  
  
### Para criar um membro consolidado  
  
1.  Na página inicial do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , na lista **Modelo** , selecione um modelo.  
  
2.  Na lista **Versão** , selecione uma versão.  
  
3.  Clique em **Gerenciador**.  
  
4.  Na barra de menus, aponte para **Hierarquias** e clique no nome da hierarquia à qual você deseja adicionar um membro consolidado.  
  
5.  Acima da grade, selecione a opção **Membros consolidados** ou **Todos os membros consolidados da hierarquia** .  
  
6.  No painel esquerdo, selecione um nó raiz ou um membro consolidado sob a qual você deseja criar um membro consolidado.  
  
7.  Clique em **Adicionar**.  
  
8.  No painel à direita, preencha os campos.  
  
9. Opcional. Na caixa **Anotações** , digite um comentário sobre por que o membro foi adicionado. Todos os usuários que têm acesso ao membro podem exibir a anotação.  
  
10. Clique em **OK**.  
  
## Próximas etapas  
  
-   [Mover membros em uma hierarquia &#40;Master Data Services&#41;](../Topic/Move%20Members%20within%20a%20Hierarchy%20\(Master%20Data%20Services\).md)  
  
## Consulte também  
 [Criar uma hierarquia explícita &#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [Criar um membro folha &#40;Master Data Services&#41;](../master-data-services/create-a-leaf-member-master-data-services.md)   
 [Membros &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [Hierarquias explícitas &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
  