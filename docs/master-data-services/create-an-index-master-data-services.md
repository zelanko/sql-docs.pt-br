---
title: "Criar um &#237;ndice (Master Data Services) | Microsoft Docs"
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
ms.assetid: d694a105-69b1-4ff6-99d3-1f408b916b81
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# Criar um &#237;ndice (Master Data Services)
  Crie um índice personalizado em uma lista de atributos que você consulta com frequência para melhorar o desempenho da consulta.  
  
## Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional Administração do Sistema. Para obter mais informações, consulte [Permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
 **Para criar um índice**  
  
1.  No Master Data Manager, clique em **Administração do Sistema**.  
  
2.  Na página **Gerenciar Modelo** , selecione um modelo na grade e clique em **Entidades**.  
  
3.  Na página **Gerenciar Entidade** , na **grade** , selecione a linha para a entidade para a qual você deseja criar o índice.  
  
4.  Clique em **Índices**.  
  
5.  Na caixa **Nome** , digite um nome para o índice.  
  
6.  Escolha **É Exclusivo** se quiser criar um índice exclusivo. Para obter mais informações sobre tipos de índice, consulte [Índice personalizado &#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md).  
  
7.  Clique nos atributos na caixa **Atributos Disponíveis** e clique na seta **Adicionar** . Para adicionar todos os atributos, clique na seta **Adicionar Tudo** .  
  
8.  Clique em **Salvar**.  
  
 Para cada índice criada, uma linha com quatro colunas é adicionada à grade. A tabela a seguir descreve as colunas.  
  
|Nome da coluna|Description|  
|-----------------|-----------------|  
|Status|O status do índice.<br /><br /> Quando você clica em **Salvar**, a imagem ![Icon for updating status](../master-data-services/media/mds-statusicon-updating.png "Icon for updating status") é exibida, indicando que o índice está sendo atualizado.<br /><br /> Se houver erros ao criar ou editar um índice, a imagem ![Icon for error status](../master-data-services/media/mds-statusicon-error.png "Icon for error status") será exibida.<br /><br /> Caso contrário, o status será OK e a imagem ![Icon for OK status](../master-data-services/media/mds-statusicon-ok.png "Icon for OK status") será exibida.|  
|Nome|O nome do índice.|  
|É Exclusivo|Especifica se o índice é exclusivo.|  
|Sobre atributos|Mostra os nomes de exibição de atributos nos quais o índice é definido.|  
  
 Quando você clica em um índice, as informações a seguir são exibidas.  
  
-   **Criado por**: o nome do usuário que criou o índice.  
  
-   **Em**: a data e a hora em que o índice foi criado.  
  
-   **Atualizado por**: o nome do usuário que atualizou o índice pela última vez.  
  
-   **Em**: a data e a hora em que o índice foi atualizado pela última vez.  
  
## Próximas etapas  
 [Editar e excluir um índice &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-index-master-data-services.md)  
  
## Consulte também  
 [Índice personalizado &#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md)  
  
  