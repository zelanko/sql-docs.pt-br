---
title: "Criar uma exibi&#231;&#227;o de assinatura para exportar dados (Master Data Services) | Microsoft Docs"
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
  - "exibições de assinatura [Master Data Services], criando"
  - "criando exibições de assinatura [Master Data Services]"
ms.assetid: a5e28961-af16-414a-9845-d2e06aac5214
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 10
---
# Criar uma exibi&#231;&#227;o de assinatura para exportar dados (Master Data Services)
  Crie uma exibição de assinatura para exportar dados do Master Data Services para sistemas de assinatura. Você está criando um modo de exibição de seus dados no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] banco de dados.  
  
## Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Gerenciamento de Integração** . Para obter mais informações, consulte [permissões de área funcional e 40; Master Data Services & 41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [Administradores e 40; Master Data Services & 41;](../master-data-services/administrators-master-data-services.md).  
  
### Para criar e editar uma exibição de assinatura  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Gerenciamento de Integração**.  
  
2.  Da barra de menus, clique em **Criar Exibições**.  
  
3.  Sobre o **exibições de assinatura** clique em **Adicionar** para criar um modo de exibição ou clique em **Editar** para editar um modo de exibição. Um painel é exibido no lado direito.  
  
4.  No **Criar exibição de assinatura** painel, no **nome** digite um nome para o modo de exibição.  
  
     No **Editar modo de exibição de assinatura** painel, no **nome** digite o nome do modo de exibição atualizado.  
  
5.  Do **modelo** selecione um modelo.  
  
6.  Selecione **incluir membros excluído**, para incluir membros excluído no modo de exibição.  
  
7.  Selecione **versão** ou **sinalizador de versão** em **Opções de versão**, e, em seguida, selecione na lista correspondente.  
  
    > [!TIP]  
    >  Crie uma exibição de assinatura com base em um sinalizador de versão. Quando você bloqueia uma versão, pode reatribuir o sinalizador a uma versão aberta sem atualizar a exibição de assinatura.  
  
8.  Selecione **entidade** ou **hierarquia derivada** no **fontes de dados** opção e, em seguida, selecione na lista correspondente.  
  
9. Do **formato** selecione um formato de exibição de assinatura.  
  
10. Se você escolheu **níveis explícitos** ou **níveis derivados** do **formato** lista, digite o número de níveis na hierarquia para incluir na exibição.  
  
11. Clique em **Salvar**.  
  
## Informações de Exibição  
 Para cada exibição criada, uma linha com dez colunas é adicionada à grade. A tabela a seguir descreve as colunas.  
  
|Coluna|Descrição|  
|------------|-----------------|  
|Status|O status da exibição.<br /><br /> Quando você clica em **Salvar**, o ![Icon for updating status](../master-data-services/media/mds-statusicon-updating.png "Icon for updating status") será exibida, indicando que a exibição está atualizando a imagem.<br /><br /> Se houver erros ao criar ou editar uma exibição, o ![Icon for error status](../master-data-services/media/mds-statusicon-error.png "Icon for error status") exibe a imagem.<br /><br /> Caso contrário, o status está OK e ![Icon for OK status](../master-data-services/media/mds-statusicon-ok.png "Icon for OK status") exibe a imagem.|  
|Nome|O nome da exibição de assinatura.|  
|Modelo|O nome do modelo.|  
|Versão|O nome da versão.|  
|Sinalizador de Versão|O nome do sinalizador de versão.|  
|Hierarquia Derivada|O nome da hierarquia derivada.|  
|Entidade|O nome da entidade.|  
|Formato|Especifica o tipo dos dados na exibição.|  
|Nível|Especifica o número de níveis na exibição, que é usado apenas para os formatos de Nível explícito ou Nível derivado|  
|Incluir membros excluídos|Indica se membros excluídos de forma reversível são incluídos na exibição.|  
  
 Quando você clica em uma exibição, as informações a seguir são exibidas.  
  
-   **Criado por**: O nome do usuário que criou a exibição.  
  
-   **Em**: A data e hora em que o modo de exibição foi criado.  
  
-   **Atualizado por**: O nome do usuário que fez a última atualizado o modo de exibição.  
  
-   **Em**: A data e hora em que o modo de exibição foi atualizado pela última.  
  
## Consulte também  
 [Visão geral: Exportando dados & #40. Master Data Services & 41;](../master-data-services/overview-exporting-data-master-data-services.md)   
 [Excluir uma exibição de assinatura & #40. Master Data Services & 41;](../master-data-services/delete-a-subscription-view-master-data-services.md)   
 [Criar um sinalizador de versão & #40. Master Data Services & 41;](../master-data-services/create-a-version-flag-master-data-services.md)  
  
  