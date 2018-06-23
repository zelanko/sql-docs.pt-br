---
title: 'Tarefa 15: Criando e executando o projeto SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 13adf4e0-216a-4992-b13d-b7b1e1629e77
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9a63fcf03591626d5b4c1351d5ce868ef7a9fb65
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012808"
---
# <a name="task-15-building-and-running-the-ssis-project"></a>Tarefa 15: Criando e executando o projeto SSIS
  Nesta tarefa, você criará e executará o projeto SSIS. Se você tiver a versão de 64 bits do Excel 2010 instalado no computador, você deve definir o valor de **Run64BitRuntime** para **False** para a origem do Excel trabalhar.  
  
1.  No **Solution Explorer** janela, clique em **projeto** no menu e clique em **propriedades de CleanseAndCurateSuppliers**.  
  
2.  No **propriedades** caixa de diálogo caixa, expanda **propriedades de configuração** na esquerda, clique em **depuração**.  
  
3.  Definir **Run64BitRuntime** para **False**.  
  
     ![Propriedades do projeto CleanseAndCurateSuppliers](../../2014/tutorials/media/et-buildingandrunningthessisproject-01.jpg "propriedades do projeto CleanseAndCurateSuppliers")  
  
4.  Clique em **Okey** para fechar o **propriedades** caixa de diálogo.  
  
5.  Clique em **criar** na barra de menus e clique em **compilar CleanseAndCurateSuppliers**. Verifique se não há erros de compilação.  
  
6.  Clique em **depurar** na barra de menus, clique em **iniciar depuração**.  
  
7.  Examine as mensagens no **andamento** janela e verifique se o pacote foi executado e terminado com êxito.  
  
     ![Os resultados da janela de progresso](../../2014/tutorials/media/et-buildingandrunningthessisproject-02.jpg "resulta da janela de progresso")  
  
     ![Status final da janela de progresso](../../2014/tutorials/media/et-buildingandrunningthessisproject-03.jpg "Status Final da janela de progresso")  
  
8.  Clique em **depurar** na barra de menus e clique em **parar depuração** para parar a sessão de depuração. Se o pacote falhar, você deverá habilitar visualizadores de dados e verificar como os dados fluem entre os componentes.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 16: Verificando com o Master Data Manager](../../2014/tutorials/task-16-verifying-with-master-data-manager.md)  
  
  