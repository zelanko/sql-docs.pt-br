---
title: 'Tarefa 15: Compilando e executando o projeto do SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 13adf4e0-216a-4992-b13d-b7b1e1629e77
ms.author: lle
author: lrtoyou1223
ms.openlocfilehash: 50b313f63ae434a96d6c0e38f3c8b600914c806d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66822998"
---
# <a name="task-15-building-and-running-the-ssis-project"></a>Tarefa 15: Criando e executando o projeto SSIS

  Nesta tarefa, você criará e executará o projeto SSIS. Se você tiver a versão de 64 bits do Excel 2010 instalada em seu computador, defina o valor de **Run64BitRuntime** como **false** para que a origem do Excel funcione.  
  
1.  Na janela **Gerenciador de soluções** , clique em **projeto** no menu e clique em **Propriedades de CleanseAndCurateSuppliers**.  
  
2.  Na caixa de diálogo **Propriedades** , expanda **Propriedades de configuração** à esquerda e clique em **depuração**.  
  
3.  Defina **Run64BitRuntime** como **false**.  
  
     ![Propriedades do Projeto CleanseAndCurateSuppliers](../../2014/tutorials/media/et-buildingandrunningthessisproject-01.jpg "Propriedades do Projeto CleanseAndCurateSuppliers")  
  
4.  Clique em **OK** para fechar a caixa de diálogo **Propriedades**.  
  
5.  Clique em **criar** na barra de menus e clique em **criar CleanseAndCurateSuppliers**. Verifique se não há erros de compilação.  
  
6.  Clique em **depurar** na barra de menus e clique em **Iniciar Depuração**.  
  
7.  Examine as mensagens na janela de **progresso** e verifique se o pacote foi executado e foi concluído com êxito.  
  
     ![Resultados da janela de progresso](../../2014/tutorials/media/et-buildingandrunningthessisproject-02.jpg "Resultados da janela de progresso")  
  
     ![Status final da janela de progresso](../../2014/tutorials/media/et-buildingandrunningthessisproject-03.jpg "Status final da janela de progresso")  
  
8.  Clique em **depurar** na barra de menus e clique em **parar depuração** para interromper a sessão de depuração. Se o pacote falhar, você deverá habilitar visualizadores de dados e verificar como os dados fluem entre os componentes.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 16: Verificando com o Master Data Manager](../../2014/tutorials/task-16-verifying-with-master-data-manager.md)  
  
  
