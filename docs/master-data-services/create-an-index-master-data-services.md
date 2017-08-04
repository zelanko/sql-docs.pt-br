---
title: "Criar um índice (Master Data Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d694a105-69b1-4ff6-99d3-1f408b916b81
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a4d03606ab8a45d6c7b326fd64b6900ac7e67356
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="create-an-index-master-data-services"></a>Criar um índice (Master Data Services)
  Crie um índice personalizado em uma lista de atributos que você consulta com frequência para melhorar o desempenho da consulta.  
  
## <a name="prerequisites"></a>Pré-requisitos  
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
|Status|O status do índice.<br /><br /> Quando você clica em **salvar**, o ![ícone de status de atualização](../master-data-services/media/mds-statusicon-updating.png "ícone de status de atualização") imagem exibida indicando que o índice está sendo atualizado.<br /><br /> Se houver erros ao criar ou editar um índice, o ![ícone de status de erro](../master-data-services/media/mds-statusicon-error.png "ícone de status de erro") imagem é exibida.<br /><br /> Caso contrário, o status é Okey e o ![ícone de status Okey](../master-data-services/media/mds-statusicon-ok.png "ícone de status Okey") imagem é exibida.|  
|Nome|O nome do índice.|  
|É Exclusivo|Especifica se o índice é exclusivo.|  
|Sobre atributos|Mostra os nomes de exibição de atributos nos quais o índice é definido.|  
  
 Quando você clica em um índice, as informações a seguir são exibidas.  
  
-   **Criado por**: o nome do usuário que criou o índice.  
  
-   **Em**: a data e a hora em que o índice foi criado.  
  
-   **Atualizado por**: o nome do usuário que atualizou o índice pela última vez.  
  
-   **Em**: a data e a hora em que o índice foi atualizado pela última vez.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Editar e excluir um índice &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-index-master-data-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Índice personalizado &#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md)  
  
  
