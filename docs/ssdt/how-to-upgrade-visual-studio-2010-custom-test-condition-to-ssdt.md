---
title: Atualizar uma condição de teste personalizada do Visual Studio 2010 de uma versão anterior
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 44c895a3-dee0-4032-a60f-812f5fe3c713
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 333ef282fe4e1f9d7af53cd3569371e88018a03f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251070"
---
# <a name="how-to-upgrade-a-visual-studio-2010-custom-test-condition-from-a-previous-release-to-sql-server-data-tools"></a>Como fazer: Atualizar uma condição de teste personalizada do Visual Studio 2010 de uma versão anterior do SQL Server Data Tools

Para usar uma condição de unidade de teste que você criou em uma versão anterior para o SQL Server Data Tools, você deverá atualizá-la:  
  
-   [Atualizar referências](#UpdateReferences)  
  
-   [Atualizar atributos de classe e referências de tipo](#UpdateClassAttributesandTypeReference)  
  
-   [Instalar a condição de teste atualizada](#ApplytheNewRegistrationProcess)  
  
## <a name="UpdateReferences"></a>Atualizar referências  
Para atualizar as referências de projeto:  
  
1.  Apenas no Visual Basic, no **Gerenciador de Soluções**, clique em **Mostrar Todos os Arquivos**.  
  
2.  No **Gerenciador de Soluções**, expanda o nó **Referências**.  
  
3.  Clique com o botão direito do mouse nas seguintes referências de assembly e clique em **Remover**:  
  
    1.  Microsoft.Data.Schema.UnitTesting  
  
    2.  Microsoft.Data.Schema  
  
4.  No menu **Projeto**, clique no botão direito do mouse na pasta do projeto no **Gerenciador de Soluções** e clique em **Adicionar Referência**.  
  
5.  Clique na guia **.NET**.  
  
6.  Na lista **Nome do Componente**, selecione **System.ComponentModel.Composition** e clique em **OK**.  
  
7.  Adicione as referências de assembly necessárias. Clique com o botão direito do mouse no nó do projeto e clique em **Adicionar Referência**. Clique em **Procurar** e navegue até a pasta C:\Arquivos de Programas (x86)\\Microsoft SQL Server\110\DAC\Bin. Escolha Microsoft.Data.Tools.Schema.Sql.dll, clique em Adicionar e depois em OK.  
  
8.  No menu **Projeto**, clique em **Descarregar Projeto**.  
  
9. Clique com o botão direito do mouse no **Projeto** no **Gerenciador de Soluções** e escolha **Editar**`project_name` **.csproj**.  
  
10. Adicione a seguinte Instrução Import depois da importação de `Microsoft.CSharp.targets`:  
  
    ```  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' == ''" />  
  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' != ''" />  
    ```  
  
11. Salve o arquivo e feche-o. Clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e escolha **Recarregar Projeto**.  
  
12. Abra a classe de condição de teste e remova todas as instruções using que começam com **Microsoft.Data.Schema**. A maneira mais fácil de fazer isso é clicar com o botão direito do mouse no arquivo e escolher **Organizar Usings** e, em seguida, **Remover e Classificar**. As instruções using a seguir devem ser removidas:  
  
    ```  
    using Microsoft.Data.Schema.UnitTesting;  
    using Microsoft.Data.Schema.UnitTesting.Conditions;  
    using Microsoft.Data.Schema.Extensibility;  
    using Microsoft.Data.Schema;  
    ```  
  
13. Adicione as instruções using a seguir ao arquivo, se já não houver:  
  
    ```  
    using System.ComponentModel;  
    using Microsoft.Data.Tools.Schema.Sql.UnitTesting;  
    using Microsoft.Data.Tools.Schema.Sql.UnitTesting.Conditions;  
    ```  
  
Sua condição de teste agora usa as referências de assembly do teste de unidade do SQL Server.  
  
## <a name="UpdateClassAttributesandTypeReference"></a>Atualizar atributos de classe e referências de tipo  
Substitua os atributos de classe de teste de unidade mais antigos por um novo atributo. A extensibilidade de teste de unidade do SQL Server baseia-se agora no Managed Extensibility Framework (MEF). Você também deve atualizar algumas referências de tipo.  
  
### <a name="update-class-attributes"></a>Atualizar atributos de classes  
Atualize seu código desta maneira:  
  
1.  Remova os atributos `DatabaseSchemaProviderCompatibility`. Eles eram exigidos pelo recurso de extensibilidade da versão anterior e não têm suporte no teste de unidade do SQL Server.  
  
2.  Remova o atributo `DisplayName`. O nome para exibição está incluído no novo atributo.  
  
3.  Adicionar o novo atributo `ExportTestCondition`. Este atributo deve estar presente para sua condição de teste para ser descoberto e usado no teste de unidade do SQL Server. O `ExportTestCondition` e substitui os atributos `DatabaseSchemaProviderCompatibility`. O `ExportTestCondition` utiliza dois parâmetros:  
  
    -   `DisplayName` é o primeiro parâmetro. Ele substitui o atributo `DisplayName` e é usado para descrever todas as condições de teste deste tipo.  
  
    -   O segundo parâmetro é usado para identificar exclusivamente sua extensão. Você pode simplesmente transmitir o seu tipo usando `typeof(NewTestCondition)`, porque ele deve ser exclusivo. No entanto, uma ID de cadeia de caracteres também pode ser transmitida, se preferir.  
  
4.  Sua definição de classe deve ser alterada da seguinte maneira:  
  
    Antes:  
  
    ```  
    [DatabaseSchemaProviderCompatibility(typeof(DatabaseSchemaProvider))]  
    [DatabaseSchemaProviderCompatibility(null)]  
    [DisplayName("NewTestCondition")]  
    public class NewTestCondition:TestCondition  
    {  
       // Additional implementation to be added here  
    }  
    ```  
  
    Após:  
  
    ```  
    [ExportTestCondition("NewTestCondition ", typeof(NewTestCondition))]  
    public class NewTestCondition:TestCondition  
    {  
       // Additional implementation to be added here  
    }  
    ```  
  
### <a name="update-type-references"></a>Atualizar referências de tipo  
Alguns nomes de tipo foram alterados na estrutura de teste de unidade do SQL Server. Para atualizar seu código para usar os novos nomes de tio, use **Localizar e Substituir** no menu **Editar**. Os nomes de tipo agora começam com **Sql**. Os nomes de classe deve ser atualizados da seguinte maneira:  
  
|Nome do tipo antigo|Nome do tipo novo|  
|-----------------|-----------------|  
|`ExecutionResult`|`SqlExecutionResult`|  
  
## <a name="ApplytheNewRegistrationProcess"></a>Instalar a condição de teste atualizada  
Em versões anteriores de teste de unidade de banco de dados, você pode ser solicitado a instalar sua condição de teste no cache de assembly global ou a criar um arquivo XML contendo suas informações de assembly. Com o teste de unidade do SQL Server, este processo adicional não é mais necessário. (Para saber mais, confira [Compilar o projeto e instalar sua condição de teste](../ssdt/walkthrough-use-custom-test-condition-to-verify-stored-procedure-results.md#xxx).  
  
Depois de atualizar suas referências, verifique se seu assembly está assinado e compilado.  
  
Em seguida, copie o arquivo de assembly do diretório de saída, por padrão, Meus Documentos\Visual Studio 2010\Projetos\\<yoursolutionname>\\<yourprojectname>\bin\Debug\\) para o diretório %Arquivos de Programas%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions. Quando o Visual Studio iniciar, ele identificará as extensões no diretório TestConditions e as tornará disponíveis para uso na sessão:  
  
## <a name="upgrade-existing-tests-that-need-to-use-the-new-test-condition"></a>Atualizar testes existentes que precisem usar a nova condição de teste  
Localize todos os projetos de teste que usam a condição de teste antiga e que são necessárias para usar a nova condição. Verifique se esses projetos de teste estão atualizados. Para saber mais, confira [Atualizar um projeto de teste mais antigo contendo testes de unidade de banco de dados](../ssdt/upgrade-an-older-test-project-containing-database-unit-tests.md).  
  
Remova a referência de assembly para a condição de teste antiga.  
  
Adicione um novo teste de unidade do SQL Server para o projeto para criar uma referência de assembly para a condição de teste atualizada no projeto. Uma classe de teste deve ser adicionada para criar a referência. Você pode excluir a classe de teste depois que a referência for adicionada.  
  
## <a name="see-also"></a>Consulte Também  
[Condições de teste personalizadas para testes de unidade do SQL Server](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)  
  
