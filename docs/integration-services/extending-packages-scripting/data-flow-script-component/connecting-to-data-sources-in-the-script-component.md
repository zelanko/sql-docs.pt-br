---
title: Conectando-se a fontes de dados no componente Script | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], connecting to data sources
ms.assetid: 96de63ab-ff48-4e7e-89e0-ffd6a89c63b6
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e2accca553f1bd9c536076fd0bbcebbff0ff2c42
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="connecting-to-data-sources-in-the-script-component"></a>Conectando-se a fontes de dados no componente de Script
  Um gerenciador de conexões é uma unidade conveniente que encapsula e armazena as informações necessárias para conexão com uma fonte de dados de um tipo específico. Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Conexões](../../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
 Você pode tornar os gerenciadores de conexão existentes disponíveis para acesso de script personalizado no componente de origem ou destino clicando o **adicionar** e **remover** botões o **gerenciadores de Conexão** página do **Editor de transformação scripts**. Entretanto, você deverá gravar seu próprio código personalizado para carregar ou salvar seus dados e, possivelmente, abrir e fechar a conexão com a fonte de dados. Para obter mais informações sobre o **gerenciadores de Conexão** página do **Editor de transformação scripts**, consulte [Configurando o componente Script no Editor de componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md) e [Editor de transformação scripts &#40; Página gerenciadores de Conexão &#41; ](../../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
 O componente Script cria uma **conexões** classe de coleção no **ComponentWrapper** item de projeto que contém um acessador fortemente tipado para cada Gerenciador de conexão que tem o mesmo nome que o próprio Gerenciador de conexão. Essa coleção é exposta por meio de **conexões** propriedade do **ScriptMain** classe. A propriedade de acessador retorna uma referência ao gerenciador de conexões como uma instância de <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100>. Por exemplo, se você adicionou um gerenciador de conexões nomeado `MyADONETConnection` na página Gerenciadores de Conexões da caixa de diálogo, poderá obter uma referência a ele em seu script adicionando o seguinte código:  
  
 `Dim myADONETConnectionManager As IDTSConnectionManager100 = _`  
  
 `Me.Connections.MyADONETConnection`  
  
> [!NOTE]  
>  Você deve saber o tipo de conexão que é retornado pelo Gerenciador de conexão antes de chamar **AcquireConnection**. Como a tarefa de Script foi **Option Strict** habilitado, você deve converter a conexão, o que é retornado como tipo **objeto**, para o tipo de conexão apropriado antes de você pode usá-lo.  
  
 Em seguida, você chama o **AcquireConnection** método do Gerenciador de conexão específica para obter a conexão subjacente ou as informações necessárias para se conectar à fonte de dados. Por exemplo, você pode obter uma referência para o **System.Data.SqlConnection** encapsulada por um Gerenciador de conexão ADO.NET usando o código a seguir:  
  
 `Dim myADOConnection As SqlConnection = _`  
  
 `CType(MyADONETConnectionManager.AcquireConnection(Nothing), SqlConnection)`  
  
 Em contraste, a mesma chamada para um gerenciador de conexões de arquivo simples retorna somente o caminho e nome de arquivo da fonte de dados de arquivo.  
  
 `Dim myFlatFile As String = _`  
  
 `CType(MyFlatFileConnectionManager.AcquireConnection(Nothing), String)`  
  
 Em seguida, você deve fornecer esse nome de arquivo e caminho para um **System.IO.StreamReader** ou **Streamwriter** para ler ou gravar os dados no arquivo simples.  
  
> [!IMPORTANT]  
>  Quando você escreve o código gerenciado em um componente de Script, você não pode chamar o método AcquireConnection de conexão gerenciadores que retornam objetos não gerenciados, como o Gerenciador de conexão OLE DB e o Gerenciador de conexão do Excel. No entanto, você pode ler a propriedade ConnectionString desses gerenciadores de conexão e se conectar à fonte de dados diretamente em seu código usando a cadeia de caracteres de conexão de um banco de dados OLE **conexão** do **OLEDB** namespace.  
>   
>  Se você precisar chamar o método AcquireConnection de um Gerenciador de conexão que retorna um objeto não gerenciado, use um Gerenciador de conexão ADO.NET. Quando você configurar o gerenciador de conexões ADO.NET para usar um provedor OLE DB, ele se conectará usando o provedor de dados .NET Framework para OLE DB. Nesse caso, o método AcquireConnection retorna um **OleDbConnection** em vez de um objeto não gerenciado. Para configurar um Gerenciador de conexão ADO.NET para uso com uma fonte de dados do Excel, selecione o Microsoft OLE DB Provider for Jet, especifique uma pasta de trabalho do Excel e, em seguida, digite `Excel 8.0` (para o Excel 97 e posterior) como o valor de **propriedades estendidas** no **todos os** página do **Gerenciador de Conexão** caixa de diálogo.  
  
 Para obter mais informações sobre como usar gerenciadores de conexão com o componente script, consulte [criando uma fonte com o componente Script](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md) e [criando um destino com o componente Script](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md).  
  
## <a name="see-also"></a>Consulte também  
 [Integration Services &#40; SSIS &#41; Conexões](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Criar gerenciadores de Conexão](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  
