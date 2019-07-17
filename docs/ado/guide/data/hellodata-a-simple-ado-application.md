---
title: 'HelloData: Um aplicativo ADO simples | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e666f479d95e3915703dc539ba2731e95175488b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925134"
---
# <a name="hellodata-a-simple-ado-application"></a>HelloData: Um aplicativo ADO simples
Este aplicativo simples percorre cada uma das quatro principais operações ADO: Introdução, o exame, edição e atualização de dados. Essas operações são executadas em relação a dados de exemplo Northwind incluído com o Microsoft® SQL Server. Para se concentrar nos conceitos básicos do ADO e evitar a desordem de código, no exemplo de tratamento de erro é mínimo.  
  
### <a name="to-run-hellodata"></a>Para executar o HelloData  
  
1.  Crie um novo projeto Standard EXE Visual Basic que faz referência a biblioteca do ADO. Para obter mais informações, consulte [referenciando as bibliotecas ADO](../../../ado/guide/referencing-the-ado-libraries.md).  
  
2.  Criar quatro botões de comando na parte superior do formulário, definindo a **nome** e **legenda** propriedades com os valores mostrados na tabela no final deste tópico.  
  
3.  Abaixo dos botões, adicione uma **Microsoft controle DataGrid** (Msdatgrd.ocx). O arquivo Msdatgrd.ocx está incluído no Visual Basic e está localizado no diretório \windows\system32 ou \Winnt\System32. Para adicionar o controle DataGrid ao seu painel de caixa de ferramentas do Visual Basic, selecione **componentes...**  do **projeto** menu. Em seguida, marque a caixa ao lado de "Microsoft controle DataGrid 6.0 (SP3) (OLEDB)" e, em seguida, clique em **Okey**. Para adicionar o controle ao projeto, arraste o controle DataGrid da caixa de ferramentas para o formulário do Visual Basic.  
  
4.  Criar uma **caixa de texto** no formulário abaixo da grade e defina suas propriedades, conforme mostrado na tabela. O formulário deve ser semelhante a figura a seguir, quando tiver terminado.  
  
5.  Por fim, copie o código listado na [código do HelloData](../../../ado/guide/data/hellodata-code.md)e cole-o na janela do editor de código do formulário. Pressione **F5** para executar o código.  
  
> [!NOTE]
>  No exemplo a seguir e neste guia, a id de usuário "MyId" com uma senha de "123aBc" é usada para autenticar no servidor. Você deve substituir esses valores com credenciais de logon válidas para o servidor. Além disso, substitua o valor de "MySQLServer" com o nome do seu servidor.  
  
 Para obter uma descrição detalhada do código, consulte [comentários sobre o HelloData](../../../ado/guide/data/comments-on-hellodata.md).  
  
 ![Mostra Form1 para o aplicativo HelloData VB](../../../ado/guide/data/media/hellodata.gif "HelloData")  
  
|Tipo de controle|Propriedade|Valor|  
|------------------|--------------|-----------|  
|Formulário|Name|Form1|  
||Altura|6500|  
||Largura|6500|  
|DataGrid MS|Name|grdDisplay1|  
|TextBox|Nome|txtDisplay1|  
||Várias linhas|true|  
|Botão de comando|Name|cmdGetData|  
||Legenda|Get Data|  
|Botão de comando|Nome|cmdExamineData|  
||Legenda|Examinar dados|  
|Botão de comando|Name|cmdEditData|  
||Legenda|Editar dados|  
|Botão de comando|Nome|cmdUpdateData|  
||Legenda|Atualizar dados|
