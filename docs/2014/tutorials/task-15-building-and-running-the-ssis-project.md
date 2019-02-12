---
title: 'Tarefa 15: Compilar e executar o projeto do SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 13adf4e0-216a-4992-b13d-b7b1e1629e77
ms.openlocfilehash: 1dc31f9b3df500e862236d4125fb1de99bc93eda
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56022798"
---
# <a name="task-15-building-and-running-the-ssis-project"></a>Tarefa 15: Compilando e executando o projeto SSIS
  Nesta tarefa, você criará e executará o projeto SSIS. Se você tiver a versão de 64 bits do Excel 2010 instalado no seu computador, você deve definir o valor de **Run64BitRuntime** à **falso** para a origem do Excel trabalhar.  
  
1.  No **Gerenciador de soluções** janela, clique em **Project** no menu e clique em **propriedades de CleanseAndCurateSuppliers**.  
  
2.  No **propriedades** diálogo caixa, expanda **propriedades de configuração** na esquerda, clique em **depuração**.  
  
3.  Definir **Run64BitRuntime** à **falso**.  
  
     ![Propriedades do projeto CleanseAndCurateSuppliers](../../2014/tutorials/media/et-buildingandrunningthessisproject-01.jpg "propriedades do projeto CleanseAndCurateSuppliers")  
  
4.  Clique em **Okey** para fechar o **propriedades** caixa de diálogo.  
  
5.  Clique em **construir** na barra de menus e clique em **compilar CleanseAndCurateSuppliers**. Verifique se não há erros de compilação.  
  
6.  Clique em **Debug** na barra de menus, clique em **iniciar depuração**.  
  
7.  Examine as mensagens na **andamento** janela e verifique se o pacote foi executado e terminado com êxito.  
  
     ![Os resultados da janela de progresso](../../2014/tutorials/media/et-buildingandrunningthessisproject-02.jpg "resulta da janela de progresso")  
  
     ![Status final da janela de progresso](../../2014/tutorials/media/et-buildingandrunningthessisproject-03.jpg "Status Final da janela de progresso")  
  
8.  Clique em **Debug** na barra de menus e clique em **parar depuração** para parar a sessão de depuração. Se o pacote falhar, você deverá habilitar visualizadores de dados e verificar como os dados fluem entre os componentes.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 16: Verificando com o Master Data Manager](../../2014/tutorials/task-16-verifying-with-master-data-manager.md)  
  
  
