---
title: 'HelloData: Um aplicativo ADO simples | Microsoft Docs'
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- HelloData sample application [ADO]
- ADO, samples
ms.assetid: de4bcd56-dac2-45e6-95ab-9fd7f25878fc
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a1c7d61c6349945274febc92e4e6b5acfcc379b9
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="hellodata-a-simple-ado-application"></a>HelloData: Um aplicativo ADO simples
Este aplicativo simples percorre cada uma das quatro principais operações ADO: obtendo, examinando, editar e atualizar dados. Essas operações são executadas no banco de dados de exemplo Northwind incluído com o Microsoft® SQL Server. Para focalizar os conceitos básicos do ADO e evitar desordem de código, no exemplo de tratamento de erro é mínimo.  
  
### <a name="to-run-hellodata"></a>Para executar HelloData  
  
1.  Crie um novo projeto Standard EXE Visual Basic que faz referência a biblioteca do ADO. Para obter mais informações, consulte [fazer referência às bibliotecas do ADO](../../../ado/guide/referencing-the-ado-libraries.md).  
  
2.  Criar quatro botões de comando na parte superior do formulário, definindo a **nome** e **legenda** propriedades com os valores mostrados na tabela no final deste tópico.  
  
3.  Abaixo os botões, adicione um **Microsoft controle DataGrid** (Msdatgrd.ocx). O arquivo Msdatgrd.ocx está incluído com o Visual Basic e está localizado na pasta \windows\system32 ou \Winnt\System32. Para adicionar o controle DataGrid ao painel de ferramentas do Visual Basic, selecione **componentes...**  do **projeto** menu. Em seguida, marque a caixa ao lado de "Microsoft controle DataGrid 6.0 (SP3) (OLEDB)" e, em seguida, clique em **Okey**. Para adicionar o controle ao projeto, arraste o controle DataGrid da caixa de ferramentas para o formulário do Visual Basic.  
  
4.  Criar um **TextBox** no formulário abaixo da grade e defina suas propriedades conforme mostrado na tabela. O formulário deve se parecer com a figura a seguir, quando tiver terminado.  
  
5.  Por fim, copie o código listado na [HelloData código](../../../ado/guide/data/hellodata-code.md)e cole-o na janela do editor de código do formulário. Pressione **F5** para executar o código.  
  
> [!NOTE]
>  No exemplo a seguir e em todo este guia, a id de usuário "MyId" com uma senha de "123aBc" é usada para autenticar no servidor. Você deve substituir esses valores com credenciais de logon válido para o servidor. Além disso, substitua o valor de "MySQLServer" com o nome do seu servidor.  
  
 Para obter uma descrição detalhada do código, consulte [comentários em HelloData](../../../ado/guide/data/comments-on-hellodata.md).  
  
 ![Mostra Form1 para o aplicativo HelloData VB](../../../ado/guide/data/media/hellodata.gif "HelloData")  
  
|Tipo de controle|Propriedade|Valor|  
|------------------|--------------|-----------|  
|formulário|Nome|Form1|  
||Altura|6500|  
||Largura|6500|  
|DataGrid MS|Nome|grdDisplay1|  
|TextBox|Nome|txtDisplay1|  
||Várias linhas|true|  
|Botão de comando|Nome|cmdGetData|  
||Caption|Get Data|  
|Botão de comando|Nome|cmdExamineData|  
||Caption|Examinar os dados|  
|Botão de comando|Nome|cmdEditData|  
||Caption|Editar dados|  
|Botão de comando|Nome|cmdUpdateData|  
||Caption|Atualizar dados|

