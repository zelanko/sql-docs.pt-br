---
title: 'Tarefa 16: verificando com Master Data Manager | Microsoft Docs'
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484697"
---
# <a name="task-16-verifying-with-master-data-manager"></a>Tarefa 16: Verificando com o Master Data Manager
  Nesta tarefa, você verificará o status do trabalho em lotes enviado pelo pacote SSIS e verificará se os dados foram carregados no servidor MDS usando o Master Data Manager.  
  
1.  Iniciar **Master Data Manager** ([http://localhost/MDS](http://localhost/MDS)). Se ele já estiver aberto, clique em **Microsoft SQL Server Master Data Services** na parte superior para alternar para o **Home Page**.  
  
2.  Clique em **Gerenciamento de integração**.  
  
3.  Observe que há um lote com o nome **EIMBatch** que você enviou na lista. Clique em **importar dados** na barra de menus se você não vir a tela a seguir.  
  
     ![Lote EIM](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "Lote EIM")  
  
4.  Volte para a home page clicando em **SQL Server 2012 Master Data Services** na parte superior.  
  
5.  Verifique se modelo de **fornecedores** está selecionado para **modelo** e **VERSION_1** está selecionado para **versão**e clique em **Gerenciador**.  
  
6.  Você pode consultar o pacote SSIS de dados importado para o MDS. Os dados devem ser limpos e não têm valores de **código** de duplicatas (Observação: a coluna **CódigoDoFornecedor** no Excel corresponde ao atributo de **código** da entidade fornecedor no MDS).  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 17: Examinando o projeto de limpeza do DQS criado pelo pacote SSIS](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  
