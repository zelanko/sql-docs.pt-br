---
title: Criar um destino ODBC com o componente Script | Microsoft Docs
ms.custom: ''
ms.date: 10/10/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], destination components
- ODBC destination [Integration Services]
- destinations [Integration Services], components
- Script component [Integration Services], examples
ms.assetid: d198c866-78f4-4a50-ae15-333160645815
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 812915337b03927af5b23a66a0452d0d6a875112
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65724484"
---
# <a name="creating-an-odbc-destination-with-the-script-component"></a>Criando um destino ODBC com o componente Script

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você normalmente salva os dados em um destino ODBC usando um destino [!INCLUDE[vstecado](../../includes/vstecado-md.md)] e o Provedor de Dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para ODBC. Porém, você também pode criar um destino ODBC ad hoc para uso em um único pacote. Para criar esse destino ODBC ad hoc, use o componente Script conforme demonstrado no exemplo seguinte.  
  
> [!NOTE]  
>  Se desejar criar um componente que possa ser reutilizado mais facilmente em várias tarefas de fluxo de dados e em vários pacotes, procure utilizar o código deste exemplo de componente Script como o ponto inicial de um componente de fluxo de dados personalizado. Para obter mais informações, consulte [Desenvolvendo um componente de fluxo de dados personalizado](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como criar um componente de destino que usa um gerenciador de conexões ODBC existente para salvar dados do fluxo de dados em uma tabela do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esse exemplo é uma versão modificada do destino [!INCLUDE[vstecado](../../includes/vstecado-md.md)] personalizado que foi demonstrado no tópico [Criar um destino com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). Contudo, nesse exemplo, o destino [!INCLUDE[vstecado](../../includes/vstecado-md.md)] personalizado foi modificado para funcionar com um gerenciador de conexões ODBC e salvar dados em um destino ODBC. Essas modificações também incluem as alterações seguintes:  
  
-   Você não pode chamar o método **AcquireConnection** do gerenciador de conexões ODBC do código gerenciado, porque ele retorna um objeto nativo. Portanto, esse exemplo usa a cadeia de conexão do gerenciador de conexões para se conectar à fonte de dados diretamente, usando o Provedor de Dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ODBC gerenciado.  
  
-   O **OdbcCommand** espera parâmetros posicionais. As posições dos parâmetros são indicadas pelos pontos de interrogação (?) no texto do comando. (Por outro lado, um **SqlCommand** espera parâmetros nomeados.)  
  
 Essa amostra usa a tabela **Person.Address** no banco de dados de exemplo **AdventureWorks**. O exemplo transmite a primeira e a quarta colunas, e as colunas **int _AddressID_** e **nvarchar(30) _City_** dessa tabela pelo fluxo de dados. Esses mesmos dados são usados nas amostras de origem, transformação e destino no tópico [Desenvolvendo tipos específicos de componentes Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md).  
  
#### <a name="to-configure-this-script-component-example"></a>Para configurar esse exemplo de componente Script  
  
1.  Crie um gerenciador de conexões ODBC que se conecte ao banco de dados **AdventureWorks**.  
  
2.  Crie uma tabela de destino executando o comando Transact-SQL seguinte no banco de dados **AdventureWorks**:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  Adicione um novo componente Script à superfície do designer de Fluxo de Dados e configure-o como um destino.  
  
4.  Conecte a saída de uma origem ou transformação upstream para o componente de destino no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)]. (Você pode conectar uma origem diretamente a um destino, sem transformações.) Para que essa amostra funcione, a saída do componente upstream deve incluir pelo menos as colunas **AddressID** e **City** da tabela **Person.Address** do banco de dados de exemplo **AdventureWorks**.  
  
5.  Abra o **Editor de Transformação Scripts**. Na página **Colunas de Entrada**, selecione as colunas **AddressID** e **City**.  
  
6.  Na página **Entradas e Saídas**, renomeie a entrada com um nome mais descritivo, como **MyAddressInput**.  
  
7.  Na página **Gerenciadores de Conexões**, adicione ou crie o gerenciador de conexões ODBC com um nome descritivo, como **MyODBCConnectionManager**.  
  
8.  Na página **Script**, clique em **Editar Script** e digite o script mostrado abaixo na classe **ScriptMain**.  
  
9. Feche o ambiente de desenvolvimento de script e o **Editor de Transformação Scripts**, então execute a amostra.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Criar um destino com o componente de Script](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
  
  
