---
title: 'Tarefa 16: Verificar com master data manager | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 57ad9d3e-8f95-4df6-af01-c291ccf49164
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d9828c02625ae2bc5a85859577a237b4c4fa99c5
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484676"
---
# <a name="task-16-verifying-with-master-data-manager"></a>Tarefa 16: Verificando com o Master Data Manager
  Nesta tarefa, você verificará o status do trabalho em lotes enviado pelo pacote SSIS e verificará se os dados foram carregados no servidor MDS usando o Master Data Manager.  
  
1.  Inicie o Master`http://localhost/MDS`Data **Manager** (). Se ele já estiver aberto, clique em **Microsoft SQL Server Master Data Services** na parte superior para mudar para a página **inicial**.  
  
2.  Clique **em Gestão de integração**.  
  
3.  Observe que há um lote com o nome **EIMBatch** que você enviou na lista. Clique **em Importar Dados** na barra de menu sustais se você não ver a seguinte tela.  
  
     ![Lote EIM](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "Lote EIM")  
  
4.  Volte para a página inicial clicando em **Serviços de Dados Mestres do SQL Server 2012** na parte superior.  
  
5.  Certifique-se de que o modelo **Fornecedores** está selecionado para **Modelo** e **VERSION_1** está selecionado para **Versão**e clique em **Explorador**.  
  
6.  Você pode consultar o pacote SSIS de dados importado para o MDS. Os dados devem ser limpos e não possuem duplicatas Valores de **código** (Nota: A coluna **SupplierID** no Excel corresponde ao atributo **Código** da entidade fornecedora em MDS).  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 17: Examinando o projeto de limpeza do DQS criado pelo pacote SSIS](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  
