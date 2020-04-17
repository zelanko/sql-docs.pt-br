---
title: 'Tarefa 2 (Opcional): Criar uma exibição de assinatura do MDS usando o Master Data Manager | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f3da8219-e0cb-4848-95ca-285a76ec1ba9
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: cc923792adc3fefb5ebaab9e225169648394c71f
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484706"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>Tarefa 2 (opcional): Criando uma exibição de assinatura do MDS usando o Master Data Manager
  Nesta tarefa, você cria uma exibição de assinatura para expor a entidade **Fornecedora** no modelo **Fornecedores** a outras aplicações. Você não utiliza essa exibição na versão atual do tutorial.  
  
1.  Mude para a página principal`http://localhost/MDS`do Master Data **Manager** ( ) clicando em **Serviços de Dados Mestres do SQL Server 2012** no topo.  
  
2.  Clique **em Gestão de integração**.  
  
3.  Clique **em Criar visualizações** na barra de menus.  
  
     ![Botão Adicionar uma Nova Exibição de Assinatura](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "Botão Adicionar uma Nova Exibição de Assinatura")  
  
4.  Clique no ícone **+ (Mais)** na barra de ferramentas para criar uma exibição de assinatura.  
  
5.  No **painel Criar exibição de assinatura,** digite **Fornecedores** para **nome de exibição de assinatura**.  
  
6.  Selecione **Fornecedores** como **Modelo**.  
  
7.  Selecione **VERSION_1** como **Versão**.  
  
8.  Selecione **Fornecedor** para **Entidade**.  
  
9. Selecione **membros do Leaf** para **formato**.  
  
     ![Botão Salvar Exibição de Assinatura](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "Botão Salvar Exibição de Assinatura")  
  
10. Clique em **Salvar** na barra de ferramentas para salvar a exibição da assinatura. Essa ação cria uma visualização no SQL Server chamado **Suppliers**. Você pode verificar isso usando o SQL Server Management Studio (SSMS).  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 3 &#40;&#41; opcional: Revisão das visualizações da assinatura](task-3-optional-reviewing-the-subscription-views.md)  
  
  
