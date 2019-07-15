---
title: Adicionar snippets de Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 901c7995-8eb5-4d12-8bb0-de0a922b48f8
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ea9fe53e39a6b00b1446b35c33f78dff10c9227b
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67683886"
---
# <a name="add-transact-sql-snippets"></a>Adicionar snippets de Transact-SQL
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Você pode adicionar seus próprios snippets de código Transact-SQL ao conjunto de snippets predefinidos incluídos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="creating-a-transact-sql-snippet-file"></a>Criando um arquivo de snippet Transact-SQL  
 A primeira parte da criação de um snippet de código do [!INCLUDE[tsql](../../includes/tsql-md.md)] é criar um arquivo XML com o texto do seu snippet de código. O arquivo deve ter uma extensão .snippet e atender as requisitos do [Esquema de trechos de código](https://go.microsoft.com/fwlink/?LinkId=207504). Defina a linguagem do snippet como SQL.  
  
 Você pode usar os snippets predefinidos fornecidos com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como exemplos. Para encontrar os snippets predefinidos, abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selecione o menu **Ferramentas** e clique em **Gerenciador de Snippets de Código**. Selecione **SQL** na caixa de listagem **Linguagem** ; o caminho para os snippets do [!INCLUDE[tsql](../../includes/tsql-md.md)] será exibido na caixa **Local** .  
  
## <a name="registering-the-code-snippet"></a>Registrando o snippet de código  
 Após criar o arquivo de snippet, use o Gerenciador de Snippets de Código para registrar o snippet com o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você pode adicionar uma pasta que contém vários snippets ou importar snippets individuais para a pasta **Meus Snippets de Código** .  
  
## <a name="procedures"></a>Procedimentos  
  
#### <a name="adding-a-snippet-folder"></a>Adicionando uma pasta de snippets  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Selecione o menu **Ferramentas** e clique em **Gerenciador de Snippets de Código**.  
  
3.  Clique no botão **Adicionar** .  
  
4.  Navegue até a pasta que contém seus snippets de código e clique no botão **Selecionar Pasta** .  
  
#### <a name="importing-a-snippet"></a>Importando um snippet  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Selecione o menu **Ferramentas** e clique em **Gerenciador de Snippets de Código**.  
  
3.  Clique no botão **Importar** .  
  
4.  Navegue até a pasta que contém seu trecho, clique no arquivo .snippet e clique em **Abrir** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um snippet surround-with **TRY-CATCH** e o importa para o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
1.  Cole o código a seguir no bloco de notas e salve como um arquivo chamado TryCatch.snippet.  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <CodeSnippets  xmlns="https://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">  
    <_locDefinition xmlns="urn:locstudio">  
        <_locDefault _loc="locNone" />  
        <_locTag _loc="locData">Title</_locTag>  
        <_locTag _loc="locData">Description</_locTag>  
        <_locTag _loc="locData">Author</_locTag>  
        <_locTag _loc="locData">ToolTip</_locTag>  
       <_locTag _loc="locData">Default</_locTag>  
    </_locDefinition>  
    <CodeSnippet Format="1.0.0">  
    <Header>  
    <Title>TryCatch</Title>  
                            <Shortcut></Shortcut>  
    <Description>Example Snippet for Try-Catch.</Description>  
    <Author>SQL Server Books Online Example</Author>  
    <SnippetTypes>  
                                    <SnippetType>SurroundsWith</SnippetType>  
    </SnippetTypes>  
    </Header>  
    <Snippet>  
    <Declarations>  
                                    <Literal>  
                                    <ID>CatchCode</ID>  
                                    <ToolTip>Code to handle the caught error</ToolTip>  
                                    <Default>CatchCode</Default>  
                                    </Literal>  
    </Declarations>  
    <Code Language="SQL"><![CDATA[  
    BEGIN TRY  
  
    $selected$ $end$  
  
    END TRY  
    BEGIN CATCH  
  
    $CatchCode$  
  
    END CATCH;  
    ]]>  
    </Code>  
    </Snippet>  
    </CodeSnippet>  
    </CodeSnippets>  
    ```  
  
2.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
3.  Selecione o menu **Ferramentas** e clique em **Gerenciador de Snippets de Código**.  
  
4.  Clique no botão **Importar** .  
  
5.  Navegue até a pasta que contém TryCatch.snippet, clique no arquivo TryCatch.snippet e clique em **Abrir** . Você não deve ter um snippet TryCatch na pasta **Meus Snippets de Código** .  
  
## <a name="see-also"></a>Consulte Também  
 [Inserir snippets Transact-SQL com Surround](../../relational-databases/scripting/insert-surround-with-transact-sql-snippets.md)  
  
  
