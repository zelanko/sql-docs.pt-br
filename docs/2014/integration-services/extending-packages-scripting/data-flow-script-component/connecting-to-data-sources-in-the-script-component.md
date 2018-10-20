---
title: Conectar-se a fontes de dados no componente Script | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], connecting to data sources
ms.assetid: 96de63ab-ff48-4e7e-89e0-ffd6a89c63b6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2943855784fccd869124a3dad1bc2dc72f6a8cf6
ms.sourcegitcommit: ef78cc196329a10fc5c731556afceaac5fd4cb13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49460641"
---
# <a name="connecting-to-data-sources-in-the-script-component"></a>Conectando-se a fontes de dados no componente de Script
  Um gerenciador de conexões é uma unidade conveniente que encapsula e armazena as informações necessárias para conexão com uma fonte de dados de um tipo específico. Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Conexões](../../connection-manager/integration-services-ssis-connections.md).  
  
 Você pode tornar os gerenciadores de conexões existentes disponíveis para acesso por meio de script personalizado no componente de origem ou destino, clicando nos botões **Adicionar** e **Remover** na página **Gerenciadores de Conexões** do **Editor de Transformação Scripts**. Entretanto, você deverá gravar seu próprio código personalizado para carregar ou salvar seus dados e, possivelmente, abrir e fechar a conexão com a fonte de dados. Para obter mais informações sobre a página **Gerenciador de Conexões** do **Editor de Transformação Scripts**, consulte [Configurando o componente Script no Editor de Componente Script](configuring-the-script-component-in-the-script-component-editor.md) e [Editor de Transformação Scripts &#40;Página Gerenciadores de Conexões&#41;](../../script-transformation-editor-connection-managers-page.md).  
  
 O componente de Script cria uma classe de coleção `Connections` no item do projeto `ComponentWrapper` que contém um acessador com rigidez de tipos para cada gerenciador de conexões que tem o mesmo nome que o gerenciador de conexões em si. Esta coleção é exposta pela propriedade `Connections` da classe `ScriptMain`. A propriedade de acessador retorna uma referência ao gerenciador de conexões como uma instância de <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100>. Por exemplo, se você adicionou um gerenciador de conexões nomeado `MyADONETConnection` na página Gerenciadores de Conexões da caixa de diálogo, poderá obter uma referência a ele em seu script adicionando o seguinte código:  
  
 `Dim myADONETConnectionManager As IDTSConnectionManager100 = _`  
  
 `Me.Connections.MyADONETConnection`  
  
> [!NOTE]  
>  Você deve saber o tipo de conexão retornado pelo gerenciador de conexões antes de chamar `AcquireConnection`. Como a tarefa Script tem `Option Strict` habilitada, você deve converter a conexão, que é retornada como tipo `Object`, para o tipo de conexão adequado antes de poder usá-lo.  
  
 Em seguida, chame o método `AcquireConnection` do gerenciador de conexões específico para obter a conexão subjacente ou as informações necessárias para se conectar à fonte de dados. Por exemplo, você obtém uma referência ao **System.Data.SqlConnection** encapsulada por um gerenciador de conexões do ADO.NET com o uso do código a seguir:  
  
 `Dim myADOConnection As SqlConnection = _`  
  
 `CType(MyADONETConnectionManager.AcquireConnection(Nothing), SqlConnection)`  
  
 Em contraste, a mesma chamada para um gerenciador de conexões de arquivo simples retorna somente o caminho e nome de arquivo da fonte de dados de arquivo.  
  
 `Dim myFlatFile As String = _`  
  
 `CType(MyFlatFileConnectionManager.AcquireConnection(Nothing), String)`  
  
 Em seguida, forneça esse caminho e nome de arquivo a um `System.IO.StreamReader` ou `Streamwriter` para ler ou gravar os dados no arquivo simples.  
  
> [!IMPORTANT]  
>  Quando você grava um código gerenciado em um componente Script, você não pode chamar o método AcquireConnection de gerenciadores de conexões que retornam objetos não gerenciados, tais como o gerenciador de conexões OLE DB e o gerenciador de conexões do Excel. Entretanto, você pode gravar a propriedade ConnectionString desses gerenciadores de conexões e conectar-se à fonte de dados diretamente em seu código por meio da cadeia de conexão de uma **conexão** OLE DB do namespace **System.Data.OleDb**.  
>   
>  Se você precisar chamar o método AcquireConnection de um gerenciador de conexões que retorna um objeto não gerenciado, use um gerenciador de conexões ADO.NET. Quando você configurar o gerenciador de conexões ADO.NET para usar um provedor OLE DB, ele se conectará usando o provedor de dados .NET Framework para OLE DB. Nesse caso, o método AcquireConnection retorna um `System.Data.OleDb.OleDbConnection` em vez de um objeto não gerenciado. Para configurar um gerenciador de conexões ADO.NET para uso com uma fonte de dados Excel, selecione o Microsoft OLE DB Provider for Jet, especifique uma pasta de trabalho do Excel e, em seguida, insira `Excel 8.0` (para o Excel 97 e versões posteriores) como o valor de **Propriedades Estendidas** na página **Todos** da caixa de diálogo **Gerenciador de Conexões**.  
  
 Para obter mais informações sobre como usar gerenciadores de conexões com o componente Script, consulte [Criar uma origem com o componente de Script](../../extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md) e [Criar um destino com o componente Script](../../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md).  
  
![Ícone do Integration Services (pequeno)](../../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Conexões do SSIS &#40;Integration Services&#41;](../../connection-manager/integration-services-ssis-connections.md)   
 [Criar Gerenciadores de Conexões](../../create-connection-managers.md)  
  
  
