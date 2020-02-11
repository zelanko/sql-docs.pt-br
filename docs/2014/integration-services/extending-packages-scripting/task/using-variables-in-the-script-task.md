---
title: Usar variáveis na tarefa Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Foreach Loop containers
- Script task [Integration Services], variables
- scripts [Integration Services], variables
- Variables property
- Variable object
- SSIS Script task, variables
- variables [Integration Services], Script task
ms.assetid: 593b5961-4bfa-4ce1-9531-a251c34e89d3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a15edc663d5f855a5aa217400e1c38376e292f4c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62894587"
---
# <a name="using-variables-in-the-script-task"></a>Usando variáveis na tarefa Script
  Variáveis possibilitam que a tarefa Script troque dados com outros objetos no pacote. Para obter mais informações, consulte [Variáveis do SSIS &#40;Integration Services&#41;](../../integration-services-ssis-variables.md).  
  
 A tarefa Script usa a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> do objeto `Dts` para ler de e escrever em objetos <xref:Microsoft.SqlServer.Dts.Runtime.Variable> no pacote.  
  
> [!NOTE]  
>  A propriedade <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A> da classe <xref:Microsoft.SqlServer.Dts.Runtime.Variable> é do tipo `Object`. Como a tarefa Script tem `Option Strict` habilitado, converta a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A> no tipo apropriado antes de utilizá-la.  
  
 Você adiciona variáveis existentes às listas <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadOnlyVariables%2A> e <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadWriteVariables%2A> no **Editor da Tarefa Script** para disponibilizá-las para o script personalizado. Lembre-se de que os nomes de variáveis diferenciam maiúsculas de minúsculas. No script, você acessa variáveis de ambos os tipos através da propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> do objeto `Dts`. Use a propriedade `Value` para ler e gravar em variáveis individuais. A tarefa Script gerencia de forma transparente o bloqueio à medida que o script lê e modifica os valores de variáveis.  
  
 Você pode usar o método <xref:Microsoft.SqlServer.Dts.Runtime.Variables.Contains%2A> da coleção <xref:Microsoft.SqlServer.Dts.Runtime.Variables> retornada pela propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> para verificar a existência de uma variável antes de usá-la no seu código.  
  
 Você também pode usar a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A> (Dts.VariableDispenser) para trabalhar com variáveis na tarefa Script. Ao usar o <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A>, você deve tratar as semânticas de bloqueio e a conversão de tipos de dados para obter valores variáveis em seu próprio código. Talvez seja necessário usar a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A> em vez da propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> para trabalhar com uma variável que não está disponível no tempo de design mas é criada programaticamente no tempo de execução.  
  
## <a name="using-the-script-task-within-a-foreach-loop-container"></a>Usando a tarefa Script dentro de um contêiner Loop Foreach  
 Quando uma tarefa Script é executada repetidas vezes dentro de um contêiner Loop Foreach, em geral o script precisa trabalhar com o conteúdo do item atual no enumerador. Por exemplo, ao usar o enumerador de Arquivo Foreach, o script precisa saber o nome do arquivo atual; ao usar o enumerador ADO Foreach, o script precisa saber o conteúdo das colunas da linha de dados atual.  
  
 As variáveis possibilitam essa comunicação entre o contêiner Loop Foreach e a tarefa Script. Na página **Mapeamentos de Variáveis** do **Editor de Loop Foreach**, atribua variáveis a cada item de dados retornado por um único item enumerado. Por exemplo, um enumerador de Arquivo Foreach retorna apenas um nome de arquivo no Índice 0 e, portanto, requer apenas um mapeamento de variável, enquanto um enumerador que retorna várias colunas de dados em cada linha requer o mapeamento de uma variável diferente para cada coluna a ser usada na tarefa Script.  
  
 Depois de mapear itens enumerados para variáveis, você deve adicionar as variáveis mapeadas à `ReadOnlyVariables` Propriedade na página **script** do editor da **tarefa Script** para torná-las disponíveis para o script. Para obter um exemplo de uma tarefa Script dentro de um contêiner do Loop Foreach que processa os arquivos de imagem em uma pasta, consulte [Trabalhando com imagens com a Tarefa Script](../../extending-packages-scripting-task-examples/working-with-images-with-the-script-task.md).  
  
## <a name="variables-example"></a>Exemplo de variáveis  
 O exemplo a seguir demonstra como acessar e usar variáveis em uma tarefa Script para determinar o caminho do fluxo de trabalho do pacote. O exemplo supõe que você criou variáveis de inteiro `CustomerCount` nomeadas `MaxRecordCount` e e as `ReadOnlyVariables` adicionou à coleção no editor da **tarefa Script**. A variável `CustomerCount` contém o número de registros de cliente a serem importados. Se seu valor for maior que o valor de `MaxRecordCount`, a tarefa Script reportará uma falha. Quando uma falha ocorre porque o limite de `MaxRecordCount` foi excedido, o caminho de erro do fluxo de trabalho pode implementar qualquer limpeza exigida.  
  
 Para compilar o exemplo com êxito, adicione uma referência ao assembly Microsoft.SqlServer.ScriptTask.  
  
```vb  
Public Sub Main()  
  
    Dim customerCount As Integer  
    Dim maxRecordCount As Integer  
  
    If Dts.Variables.Contains("CustomerCount") = True AndAlso _  
        Dts.Variables.Contains("MaxRecordCount") = True Then  
  
        customerCount = _  
            CType(Dts.Variables("CustomerCount").Value, Integer)  
        maxRecordCount = _  
            CType(Dts.Variables("MaxRecordCount").Value, Integer)  
  
    End If  
  
    If customerCount > maxRecordCount Then  
            Dts.TaskResult = ScriptResults.Failure  
    Else  
            Dts.TaskResult = ScriptResults.Success  
    End If  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class ScriptMain  
{  
  
    public void Main()  
    {  
        int customerCount;  
        int maxRecordCount;  
  
        if (Dts.Variables.Contains("CustomerCount")==true&&Dts.Variables.Contains("MaxRecordCount")==true)  
  
        {  
            customerCount = (int) Dts.Variables["CustomerCount"].Value;  
            maxRecordCount = (int) Dts.Variables["MaxRecordCount"].Value;  
  
        }  
  
        if (customerCount>maxRecordCount)  
        {  
            Dts.TaskResult = (int)ScriptResults.Failure;  
        }  
        else  
        {  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
  
    }  
  
}  
  
```  
  
![Ícone de Integration Services (pequeno)](../../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte Também  
 [Variáveis do SSIS &#40;Integration Services&#41;](../../integration-services-ssis-variables.md)   
 [Usar variáveis em pacotes](../../use-variables-in-packages.md)  
  
  
