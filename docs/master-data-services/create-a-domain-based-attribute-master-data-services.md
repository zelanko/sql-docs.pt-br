---
title: "Criar um atributo baseado em dom&#237;nio (Master Data Services) | Microsoft Docs"
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
  - "atributos baseados em domínio [Master Data Services], criando"
  - "criando atributos baseados em domínio [Master Data Services]"
  - "atributos [Master Data Services], criando atributos baseados em domínio"
ms.assetid: 11c31c9f-e6cc-47b7-b76a-d691f84c93c6
caps.latest.revision: 12
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 12
---
# Criar um atributo baseado em dom&#237;nio (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie um atributo baseado em domínio para popular os valores de um atributo com membros de uma entidade.  
  
## Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Uma entidade deve existir para ser usada como a origem dos valores de atributo. Por exemplo, para criar um atributo baseado em domínio com base na entidade Color, você deve primeiro criar a entidade Color. Para obter mais informações, consulte [Criar uma entidade &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
-   Uma entidade deve existir para que se possa criar o atributo para ela. Para obter mais informações, consulte [Criar uma entidade &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
## Informações de Atributo  
 Para cada atributo criado, uma linha com sete colunas é adicionada à grade. A tabela a seguir descreve as colunas.  
  
|Coluna|Description|  
|------------|-----------------|  
|Status|O status do atributo.<br /><br /> Quando você clica em Salvar, a imagem ![Icon for updating status](../master-data-services/media/mds-statusicon-updating.png "Icon for updating status") é exibida, indicando que o atributo está sendo atualizado.<br /><br /> Se houver erros ao criar ou editar um atributo, a imagem ![Icon for error status](../master-data-services/media/mds-statusicon-error.png "Icon for error status") será exibida.<br /><br /> Caso contrário, o status será OK e a imagem ![Icon for OK status](../master-data-services/media/mds-statusicon-ok.png "Icon for OK status") será exibida.|  
|Nome|O nome do atributo.|  
|Nome de Exibição|O nome de exibição do atributo.|  
|Description|A descrição do atributo.|  
|Exibir Largura em Pixels|A largura do atributo.|  
|Tipo e Propriedades|As informações de tipo e de tipo de dados do atributo.|  
|Habilitar Controle de Alterações|Especifica se o atributo está habilitado para o controle de alterações e mostra o número do grupo entre parênteses.|  
  
 Quando você clica em um atributo, as seguintes informações são exibidas.  
  
-   **Criado Por**: o nome do usuário que criou o atributo.  
  
-   **Em**: a data e hora em que o atributo foi criado.  
  
-   **Atualizado Por**: o nome do usuário que atualizou o atributo pela última vez.  
  
-   **Em**: a data e hora em que o atributo foi atualizado pela última vez.  
  
### Para criar um atributo baseado em domínio  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Gerenciar Modelos** , clique em um modelo e, em seguida, clique em **Entidades**.  
  
3.  Na página **Gerenciar Entidades** , selecione a linha da entidade para a qual deseja criar um atributo.  
  
4.  Clique em **Atributos**.  
  
5.  Na página **Gerenciar Atributos** , execute um dos procedimentos a seguir e clique em **Adicionar**.  
  
    -   Se o atributo for para membros folha, selecione **Folha** na caixa de listagem **Tipos de Membro** .  
  
    -   Se o atributo for para membros consolidados, selecione **Consolidado** na caixa de listagem **Tipos de Membro** .  
  
    -   Se o atributo for para coleções, selecione **Coleção** na caixa de listagem **Tipos de Membro** .  
  
6.  Na caixa **Nome** , digite um nome para o atributo. Para obter uma lista de palavras que não devem ser usadas como nomes de atributo, consulte [Palavras reservadas &#40;Master Data Services&#41;](../master-data-services/reserved-words-master-data-services.md)  
  
7.  Opcionalmente, digite um nome de exibição e digite uma descrição na caixa **Descrição** .  
  
8.  Na caixa **Exibir largura em pixels** , digite a largura da coluna de atributo a ser exibida na grade do **Gerenciador** .  
  
9. Na lista **Tipo de atributo**, selecione **Baseado em domínio**.  
  
10. Na lista **Entidade de Domínio** , escolha a entidade a ser usada para popular os valores de atributo.  
  
11. **Opcional, para atributos baseados em domínio para membros folha.** Selecione um atributo pai de filtro que é usado para restringir os valores permitidos para o atributo baseado em domínio.  
  
     O atributo pai de filtro deve ser outro atributo baseado em domínio para um membro folha, dentro da mesma entidade. Uma hierarquia derivada deve existir com um nível que define a relação pai-filho entre as entidades de domínio dos dois atributos.  
  
     Para obter informações sobre como restringir os valores permitidos, consulte [como filtrar listas suspensas de atributos com base em domínio](https://blogs.msdn.microsoft.com/mds/2015/12/03/in-sql-server-2016-master-data-services-how-to-filter-domain-based-attribute-drop-down-lists/), no blog do Master Data Services.  
  
12. **Opcional.** Selecione **Enable change tracking** para acompanhar as alterações feitas em grupos de atributos. Para obter mais informações, consulte [Adicionar atributos a um grupo de controle de alterações &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).  
  
13. Clique em **Salvar**.  
  
## Consulte também  
 [Atributos baseados em domínio &#40;Master Data Services&#41;](../master-data-services/domain-based-attributes-master-data-services.md)   
 [Criar uma hierarquia derivada &#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)   
 [Alterar um nome de atributo e um tipo de dados &#40;Master Data Services&#41;](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)   
 [Excluir um atributo &#40;Master Data Services&#41;](../master-data-services/delete-an-attribute-master-data-services.md)  
  
  