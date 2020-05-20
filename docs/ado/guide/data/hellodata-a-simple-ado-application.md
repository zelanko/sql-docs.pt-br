---
title: 'HelloData: um aplicativo ADO simples | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- HelloData sample application [ADO]
- ADO, samples
ms.assetid: de4bcd56-dac2-45e6-95ab-9fd7f25878fc
author: rothja
ms.author: jroth
ms.openlocfilehash: 18f9f0cd227a258b1d2d9cd2d201527f614bcc49
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758822"
---
# <a name="hellodata-a-simple-ado-application"></a>HelloData: um aplicativo ADO simples
Este aplicativo simples percorre cada uma das quatro principais operações do ADO: obtendo, examinando, editando e atualizando dados. Essas operações são executadas em relação ao banco de dados de exemplo Northwind incluído com o Microsoft® SQL Server. Para se concentrar nos conceitos básicos do ADO e evitar a aglomeração de código, o tratamento de erros no exemplo é mínimo.  
  
### <a name="to-run-hellodata"></a>Para executar o HelloData  
  
1.  Crie um novo projeto de Visual Basic EXE padrão que faça referência à biblioteca do ADO. Para obter mais informações, consulte [referenciando as bibliotecas do ADO](../../../ado/guide/referencing-the-ado-libraries.md).  
  
2.  Crie quatro botões de comando na parte superior do formulário, definindo as propriedades **nome** e **legenda** para os valores mostrados na tabela no final deste tópico.  
  
3.  Abaixo dos botões, adicione um **controle DataGrid da Microsoft** (Msdatgrd. ocx). O arquivo Msdatgrd. ocx está incluído com Visual Basic e está localizado no diretório \Windows\System32 ou \Winnt\System32. Para adicionar o controle DataGrid ao painel da caixa de ferramentas Visual Basic, selecione **componentes...** no menu **projeto** . Em seguida, marque a caixa ao lado de "controle DataGrid da Microsoft 6,0 (SP3) (OLEDB)" e clique em **OK**. Para adicionar o controle ao projeto, arraste o controle DataGrid da caixa de ferramentas para o formulário Visual Basic.  
  
4.  Crie uma **caixa de texto** no formulário abaixo da grade e defina suas propriedades conforme mostrado na tabela. O formulário deve ser semelhante à figura a seguir quando você terminar.  
  
5.  Por fim, copie o código listado no [código HelloData](../../../ado/guide/data/hellodata-code.md)e cole-o na janela Editor de código do formulário. Pressione **F5** para executar o código.  
  
> [!NOTE]
>  No exemplo a seguir, e em todo o guia, a ID de usuário "MyId" com uma senha de "123aBc" é usada para autenticar no servidor. Você deve substituir esses valores por credenciais de logon válidas para seu servidor. Além disso, substitua o valor "MySqlServer" pelo nome do seu servidor.  
  
 Para obter uma descrição detalhada do código, consulte [comentários em HelloData](../../../ado/guide/data/comments-on-hellodata.md).  
  
 ![Mostra Form1 para o aplicativo HelloData VB](../../../ado/guide/data/media/hellodata.gif "HelloData")  
  
|Tipo de controle|Propriedade|Valor|  
|------------------|--------------|-----------|  
|Formulário|Name|Form1|  
||Altura|6500|  
||Largura|6500|  
|DataGrid do MS|Name|grdDisplay1|  
|TextBox|Name|txtDisplay1|  
||Multilinha|true|  
|Botão de comando|Name|cmdGetData|  
||Legenda|Get Data|  
|Botão de comando|Name|cmdExamineData|  
||Legenda|Examinar dados|  
|Botão de comando|Name|cmdEditData|  
||Legenda| Editar dados|  
|Botão de comando|Name|cmdUpdateData|  
||Legenda|Atualizar dados|
