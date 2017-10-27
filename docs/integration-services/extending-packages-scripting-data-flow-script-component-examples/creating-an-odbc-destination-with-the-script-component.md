---
title: Criando um destino ODBC com o componente Script | Microsoft Docs
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
- Script component [Integration Services], destination components
- ODBC destination [Integration Services]
- destinations [Integration Services], components
- Script component [Integration Services], examples
ms.assetid: d198c866-78f4-4a50-ae15-333160645815
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5eb539f0d18f473b10ed8d49bcee9c298292fb41
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="creating-an-odbc-destination-with-the-script-component"></a>Criando um destino ODBC com o componente Script
  Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você normalmente salva os dados em um destino ODBC usando um [!INCLUDE[vstecado](../../includes/vstecado-md.md)] destino e o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider para ODBC. Porém, você também pode criar um destino ODBC ad hoc para uso em um único pacote. Para criar esse destino ODBC ad hoc, use o componente Script conforme demonstrado no exemplo seguinte.  
  
> [!NOTE]  
>  Se desejar criar um componente que possa ser reutilizado mais facilmente em várias tarefas de fluxo de dados e em vários pacotes, procure utilizar o código deste exemplo de componente Script como o ponto inicial de um componente de fluxo de dados personalizado. Para obter mais informações, consulte [Desenvolvendo um componente de fluxo de dados personalizado](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como criar um componente de destino que usa um ODBC existente Gerenciador de conexão para salvar os dados de fluxo de dados em um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela.  
  
 Este exemplo é uma versão modificada do personalizado [!INCLUDE[vstecado](../../includes/vstecado-md.md)] destino que foi demonstrado no tópico [criando um destino com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). Contudo, nesse exemplo, o destino [!INCLUDE[vstecado](../../includes/vstecado-md.md)] personalizado foi modificado para funcionar com um gerenciador de conexões ODBC e salvar dados em um destino ODBC. Essas modificações também incluem as alterações seguintes:  
  
-   Não é possível chamar o **AcquireConnection** método do Gerenciador de conexão ODBC do código gerenciado, porque retorna um objeto nativo. Portanto, esse exemplo usa a cadeia de conexão do gerenciador de conexões para se conectar à fonte de dados diretamente, usando o Provedor de Dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ODBC gerenciado.  
  
-   O **OdbcCommand** espera parâmetros posicionais. As posições dos parâmetros são indicadas pelos pontos de interrogação (?) no texto do comando. (Por outro lado, uma **SqlCommand** espera parâmetros nomeados.)  
  
 Este exemplo usa o **Person. address** tabela o **AdventureWorks** banco de dados de exemplo. O exemplo passa as primeira e a quarta colunas, o  **int*AddressID** * e **nvarchar (30) Cidade** colunas dessa tabela pelo fluxo de dados. Esses mesmos dados são usados na origem, transformação e exemplos de destino no tópico [desenvolvendo específico Types of Script Components](../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md).  
  
#### <a name="to-configure-this-script-component-example"></a>Para configurar esse exemplo de componente Script  
  
1.  Criar uma conexão ODBC que se conecta ao Gerenciador de **AdventureWorks** banco de dados.  
  
2.  Criar uma tabela de destino executando o seguinte comando Transact-SQL no **AdventureWorks** banco de dados:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  Adicione um novo componente Script à superfície do designer de Fluxo de Dados e configure-o como um destino.  
  
4.  Conecte a saída de uma origem ou transformação upstream para o componente de destino no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)]. (Você pode conectar uma origem diretamente a um destino, sem transformações.) Para garantir que esse exemplo funcione, a saída do componente upstream deve incluir pelo menos o **AddressID** e **Cidade** colunas para o **Person. address** tabela do **AdventureWorks** banco de dados de exemplo.  
  
5.  Abra o **Editor de transformação scripts**. Sobre o **colunas de entrada** página, selecione o **AddressID** e **City** colunas.  
  
6.  Sobre o **entradas e saídas** página, renomeie a entrada com um nome mais descritivo, como **MyAddressInput**.  
  
7.  Sobre o **gerenciadores de Conexão** página, adicione ou crie a conexão ODBC manager com um nome descritivo, como **MyODBCConnectionManager**.  
  
8.  Sobre o **Script** , clique em **Editar Script**e, em seguida, digite o script mostrado abaixo no **ScriptMain** classe.  
  
9. Feche o ambiente de desenvolvimento script, feche o **Editor de transformação scripts**, e, em seguida, executar o exemplo.  
  
    ```vb  
    Imports System.Data.Odbc  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Dim odbcConn As OdbcConnection  
        Dim odbcCmd As OdbcCommand  
        Dim odbcParam As OdbcParameter  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            Dim connectionString As String  
            connectionString = Me.Connections.MyODBCConnectionManager.ConnectionString  
            odbcConn = New OdbcConnection(connectionString)  
            odbcConn.Open()  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
  
            odbcCmd = New OdbcCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
                "VALUES(?, ?)", odbcConn)  
            odbcParam = New OdbcParameter("@addressid", OdbcType.Int)  
            odbcCmd.Parameters.Add(odbcParam)  
            odbcParam = New OdbcParameter("@city", OdbcType.NVarChar, 30)  
            odbcCmd.Parameters.Add(odbcParam)  
  
        End Sub  
  
        Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
            With odbcCmd  
                .Parameters("@addressid").Value = Row.AddressID  
                .Parameters("@city").Value = Row.City  
                .ExecuteNonQuery()  
            End With  
  
        End Sub  
  
        Public Overrides Sub ReleaseConnections()  
  
            odbcConn.Close()  
  
        End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System.Data.Odbc;  
    ...  
    public class ScriptMain :  
        UserComponent  
    {  
        OdbcConnection odbcConn;  
        OdbcCommand odbcCmd;  
        OdbcParameter odbcParam;  
  
        public override void AcquireConnections(object Transaction)  
        {  
  
            string connectionString;  
            connectionString = this.Connections.MyODBCConnectionManager.ConnectionString;  
            odbcConn = new OdbcConnection(connectionString);  
            odbcConn.Open();  
  
        }  
  
        public override void PreExecute()  
        {  
  
            odbcCmd = new OdbcCommand("INSERT INTO Person.Address2(AddressID, City) " +  
                "VALUES(?, ?)", odbcConn);  
            odbcParam = new OdbcParameter("@addressid", OdbcType.Int);  
            odbcCmd.Parameters.Add(odbcParam);  
            odbcParam = new OdbcParameter("@city", OdbcType.NVarChar, 30);  
            odbcCmd.Parameters.Add(odbcParam);  
  
        }  
  
        public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
        {  
  
            {  
                odbcCmd.Parameters["@addressid"].Value = Row.AddressID;  
                odbcCmd.Parameters["@city"].Value = Row.City;  
                odbcCmd.ExecuteNonQuery();  
            }  
  
        }  
  
        public override void ReleaseConnections()  
        {  
  
            odbcConn.Close();  
  
        }  
    }  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Criar um destino com o componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
  
  
