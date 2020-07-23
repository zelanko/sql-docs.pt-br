---
title: Simulando uma saída de erro para o componente Script | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], error output
- error outputs [Integration Services], Script component
ms.assetid: f8b6ecff-ac99-4231-a0e7-7ce4ad76bad0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: db88defad5962fb6a71b6705d7055abfb93c52c5
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914922"
---
# <a name="simulating-an-error-output-for-the-script-component"></a>Simulando uma saída de erro para o componente Script

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Embora não seja possível configurar uma saída como uma saída de erro no componente Script para manipular automaticamente as linhas de erro, você pode reproduzir a funcionalidade de uma saída de erro interna criando uma saída adicional e usando lógica condicional em seu script para direcionar linhas a essa saída quando apropriado. Talvez você queira imitar o comportamento de uma saída de erro interna adicionando duas colunas de saída para receber o número de erro e a ID da coluna em que um erro ocorreu.  
  
 Se você quiser adicionar a descrição de erro que corresponde a um código de erro específico e predefinido do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você pode usar o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> da interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>, disponível na propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> do componente Script.  
  
## <a name="example"></a>Exemplo  
 O exemplo mostrado aqui usa um componente Script configurado como uma transformação que tem duas saídas síncronas. O propósito do componente Script é filtrar linhas de erro de dados de endereço no banco de dados de exemplo AdventureWorks. Esse exemplo fictício presume que nós estamos preparando uma promoção para clientes norte-americanos e precisamos filtrar endereços que não estão localizados na América do Norte.  
  
#### <a name="to-configure-the-example"></a>Para configurar o exemplo  
  
1.  Antes de criar o novo componente Script, crie um gerenciador de conexões e configure uma origem de fluxo de dados que selecione dados de endereço do banco de dados de exemplo AdventureWorks. Para esse exemplo, que olha apenas para a coluna CountryRegionName, você pode simplesmente usar a exibição Person.vStateCountryProvinceRegion ou selecionar dados unindo as tabelas Person.Address, Person.StateProvince e Person.CountryRegion.  
  
2.  Adicione um novo componente Script à superfície de designer Fluxo de Dados e configure-o como uma transformação. Abra o **Editor de Transformação Scripts**.  
  
3.  Na página **Script**, defina a propriedade **ScriptLanguage** para a linguagem de script que você quer usar para codificar o script.  
  
4.  Clique em **Editar Script** para abrir o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSTA (Tools for Applications).  
  
5.  No método **Input0_ProcessInputRow**, digite ou cole o código de exemplo a seguir.  
  
6.  Feche o VSTA.  
  
7.  Na página **Colunas de Entrada**, selecione as colunas que você quer processar na transformação Scripts. Esse exemplo usa somente a coluna CountryRegionName. As colunas de entrada disponíveis que você não selecionar, simplesmente permanecerão inalteradas no fluxo de dados.  
  
8.  Na página **Entradas e Saídas**, adicione uma saída nova e secundária e defina seu valor **SynchronousInputID** para a ID da entrada, que também é o valor da propriedade **SynchronousInputID** da saída padrão. Defina a propriedade **ExclusionGroup** das duas saídas para o mesmo valor diferente de zero (por exemplo, 1) para indicar que cada linha será direcionada a somente uma das duas saídas. Dê à nova saída de erro um nome diferente, como "MyErrorOutput".  
  
9. Adicione colunas de saída à nova saída de erro para capturar as informações de erro desejadas, que podem incluir o código de erro, a ID da coluna em que o erro ocorreu e, possivelmente, a descrição do erro. Esse exemplo cria as colunas novas, ErrorColumn e ErrorMessage. Se você estiver capturando erros predefinidos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em sua própria implementação, adicione uma coluna ErrorCode para registrar o número do erro.  
  
10. Anote o valor de ID da(s) coluna(s) de entrada em que o componente Script verificará se há condições de erro. Esse exemplo usa esse identificador de coluna para preencher o valor da ErrorColumn.  
  
11. Feche o **Editor de Transformação Scripts**.  
  
12. Anexe as saídas do componente Script a um destino satisfatório. Destinos de arquivo simples são os mais fáceis de configurar para testar ad hoc.  
  
13. Execute o pacote.  
  
```vb  
Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
  If Row.CountryRegionName <> "Canada" _  
      And Row.CountryRegionName <> "United States" Then  
  
    Row.ErrorColumn = 68 ' ID of CountryRegionName column  
    Row.ErrorMessage = "Address is not in North America."  
    Row.DirectRowToMyErrorOutput()  
  
  Else  
  
    Row.DirectRowToOutput0()  
  
  End If  
  
End Sub  
```  
  
```csharp  
public override void Input0_ProcessInputRow(Input0Buffer Row)  
{  
  
  if (Row.CountryRegionName!="Canada"&&Row.CountryRegionName!="United States")  
  
  {  
    Row.ErrorColumn = 68; // ID of CountryRegionName column  
    Row.ErrorMessage = "Address is not in North America.";  
    Row.DirectRowToMyErrorOutput();  
  
  }  
  else  
  {  
  
    Row.DirectRowToOutput0();  
  
  }  
  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Tratamento de erro em dados](../../integration-services/data-flow/error-handling-in-data.md)   
 [Usando saídas de erro em um componente de fluxo de dados](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [Criar uma transformação síncrona com o componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)  
  
  
