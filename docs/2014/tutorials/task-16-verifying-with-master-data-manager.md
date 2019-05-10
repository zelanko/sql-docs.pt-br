---
title: 'Tarefa 16: Verificando com o Master Data Manager | Microsoft Docs'
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
ms.openlocfilehash: 35dd2da7f6cf6598918cd9d109b97f3d314556d1
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65484697"
---
# <a name="task-16-verifying-with-master-data-manager"></a>Tarefa 16: Verificar com o Master Data Manager
  Nesta tarefa, você verificará o status do trabalho em lotes enviado pelo pacote SSIS e verificará se os dados foram carregados no servidor MDS usando o Master Data Manager.  
  
1.  Inicie **Master Data Manager** ([http://localhost/MDS](http://localhost/MDS)). Se já estiver aberto, clique em **Microsoft SQL Server Master Data Services** na parte superior para alternar para o **home page do**.  
  
2.  Clique em **gerenciamento de integração**.  
  
3.  Observe que há um lote com denominado **EIMBatch** que você enviou na lista. Clique em **importação de dados** na barra de menus se você não vir a tela a seguir.  
  
     ![Lote EIM](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "lote EIM")  
  
4.  Alternar de volta para a home page por clique **SQL Server 2012 Master Data Services** na parte superior.  
  
5.  Certifique-se de que **fornecedores** modelo é selecionado para **modelo** e **VERSION_1** está selecionado para **versão**e clique em  **Explorer**.  
  
6.  Você pode consultar o pacote SSIS de dados importado para o MDS. Os dados devem ser limpos e não ter nenhuma duplicata **código** valores (Observação: **SupplierID** coluna no Excel corresponde à **código** atributo da entidade Supplier no MDS).  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 17: Revisando a limpeza do DQS projeto criado pelo pacote SSIS](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  
