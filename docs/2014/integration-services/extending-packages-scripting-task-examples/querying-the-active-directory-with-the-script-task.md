---
title: Consultar o Active Directory com a tarefa Script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], Active Directory access
- SSIS Script task, Active Directory access
- Script task [Integration Services], examples
- Active Directory [Integration Services]
ms.assetid: a88fefbb-9ea2-4a86-b836-e71315bac68e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bbcea29ad75eb84b9c8099e5998e307ecbd7943c
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58392064"
---
# <a name="querying-the-active-directory-with-the-script-task"></a>Consultando o Active Directory com a tarefa Script
  Aplicativos de processamento de dados corporativos, como pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], em geral, precisam processar dados de forma diferente com base na classificação, no nome do cargo ou em outras características dos funcionários armazenadas no Active Directory. O Active Directory é um serviço de diretório do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows que fornece um repositório centralizado de metadados, não apenas sobre usuários, mas também sobre outros ativos organizacionais como computadores e impressoras. O namespace `System.DirectoryServices` no Microsoft .NET Framework fornece classes para trabalhar com o Active Directory, a fim de ajudar você a direcionar o fluxo de processamento de dados com base nas informações que ele armazena.  
  
> [!NOTE]  
>  Se desejar criar uma tarefa mais fácil de ser reutilizada em vários pacotes, procure utilizar o código desse exemplo de tarefa Script como o ponto inicial de uma tarefa personalizada. Para obter mais informações, consulte [Desenvolvendo uma tarefa personalizada](../extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Descrição  
 O exemplo a seguir recupera nome, cargo e número de telefone de um funcionário no Active Directory, com base no valor da variável `email`, que contém o endereço de email desse funcionário. As restrições de precedência no pacote podem usar as informações recuperadas para determinar, por exemplo, se ele deve enviar uma mensagem de email de baixa prioridade ou uma página de alta prioridade, baseando-se no nome do cargo do funcionário.  
  
#### <a name="to-configure-this-script-task-example"></a>Para configurar esse exemplo de tarefa Script  
  
1.  Crie as três variáveis de cadeia de caracteres `email`, `name` e `title`. Digite um endereço de email corporativo válido como o valor da variável `email`.  
  
2.  No **Script** página do **Editor da tarefa Script**, adicione o `email` variável para o `ReadOnlyVariables` propriedade.  
  
3.  Acrescente as variáveis `name` e `title` à propriedade `ReadWriteVariables`.  
  
4.  No projeto de script, acrescente uma referência ao namespace `System.DirectoryServices`.  
  
5.  para obter informações sobre a ferramenta de configuração e recursos adicionais. Em seu código, use uma instrução `Imports` para importar o namespace `DirectoryServices`.  
  
> [!NOTE]  
>  Para executar esse script com sucesso, sua empresa deve usar o Active Directory em sua rede e armazenar as informações do funcionário que este exemplo usa.  
  
### <a name="code"></a>Código  
  
```vb  
Public Sub Main()  
  
    Dim directory As DirectoryServices.DirectorySearcher  
    Dim result As DirectoryServices.SearchResult  
    Dim email As String  
  
    email = Dts.Variables("email").Value.ToString  
  
    Try  
        directory = New _  
            DirectoryServices.DirectorySearcher("(mail=" & email & ")")  
        result = directory.FindOne  
        Dts.Variables("name").Value = _  
            result.Properties("displayname").ToString  
        Dts.Variables("title").Value = _  
            result.Properties("title").ToString  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, _  
            "Script Task Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
public void Main()  
{  
    //  
    DirectorySearcher directory;  
    SearchResult result;  
    string email;  
  
    email = (string)Dts.Variables["email"].Value;  
  
    try  
    {  
        directory = new DirectorySearcher("(mail=" + email + ")");  
        result = directory.FindOne();  
        Dts.Variables["name"].Value = result.Properties["displayname"].ToString();  
        Dts.Variables["title"].Value = result.Properties["title"].ToString();  
        Dts.TaskResult = (int)ScriptResults.Success;  
    }  
    catch (Exception ex)  
    {  
        Dts.Events.FireError(0, "Script Task Example", ex.Message + "\n" + ex.StackTrace, String.Empty, 0);  
        Dts.TaskResult = (int)ScriptResults.Failure;  
    }  
  
}  
```  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Artigo técnico, [Processing Active Directory Information in SSIS](https://go.microsoft.com/fwlink/?LinkId=199588) (em inglês), em social.technet.microsoft.com  
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
  
