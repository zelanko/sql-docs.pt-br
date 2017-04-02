---
title: "Criar um atributo num&#233;rico (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "atributos [Master Data Services], criando atributos de número"
  - "criando atributos de número [Master Data Services]"
ms.assetid: c0dbb6d8-ba78-485a-a40d-6d5cb7e75d0a
caps.latest.revision: 9
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 9
---
# Criar um atributo num&#233;rico (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie um atributo numérico quando desejar que os usuários insiram um número como valor de atributo.  
  
> [!NOTE]  
>  Os atributos numéricos têm limitações. Para obter mais informações, consulte [Atributos #40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md).  
  
## Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
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
  
### Para criar um atributo numérico  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Gerenciar Modelo** , selecione um modelo na grade e clique em **Entidades**.  
  
3.  Na página **Gerenciar Entidade** , selecione a linha da entidade para a qual deseja criar um atributo.  
  
4.  Clique em **Atributos**.  
  
5.  Na página **Gerenciar Atributos** , execute um dos procedimentos a seguir e clique em **Adicionar**.  
  
    -   Se o atributo for para membros folha, selecione **Folha** na caixa de listagem **Tipos de Membro** .  
  
    -   Se o atributo for para membros consolidados, selecione **Consolidado** na caixa de listagem **Tipos de Membro** .  
  
    -   Se o atributo for para coleções, selecione **Coleção** na caixa de listagem **Tipos de Membro** .  
  
6.  Na caixa **Nome** , digite um nome para o atributo. Para obter uma lista de palavras que não devem ser usadas como nomes de atributo, consulte [Palavras reservadas &#40;Master Data Services&#41;](../master-data-services/reserved-words-master-data-services.md).  
  
7.  Opcionalmente, digite um nome de exibição e digite uma descrição para o atributo na caixa **Descrição** .  
  
8.  Na caixa **Exibir largura em pixels** , digite a largura da coluna de atributo a ser exibida na grade do **Gerenciador** .  
  
9. Na lista **Tipo de atributo**, selecione **Forma livre**.  
  
10. Na lista **Tipo de dados** , selecione **Número**.  
  
11. Na caixa **Decimais** , digite a quantidade de números que podem ser inseridos depois de um decimal.  
  
12. Na caixa de listagem **Máscara de entrada** , selecione um formato para números negativos.  
  
13. Opcionalmente, selecione **Habilitar controle de alterações** para controlar alterações de grupos de atributos. Para obter mais informações, consulte [Adicionar atributos a um grupo de controle de alterações &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).  
  
14. Clique em **Salvar**.  
  
## Consulte também  
 [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)   
 [Alterar um nome de atributo e um tipo de dados &#40;Master Data Services&#41;](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)   
 [Criar um atributo baseado em domínio &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [Criar um atributo de arquivo &#40;Master Data Services&#41;](../master-data-services/create-a-file-attribute-master-data-services.md)  
  
  