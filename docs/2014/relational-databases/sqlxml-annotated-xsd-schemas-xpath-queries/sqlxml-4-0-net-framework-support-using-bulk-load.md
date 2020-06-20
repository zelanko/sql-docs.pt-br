---
title: Usando o carregamento em massa do SQLXML no ambiente .NET | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, XML Bulk Load
- XML Bulk Load [SQLXML], .NET environment
- .NET Framework [SQLXML], XML Bulk Load
- bulk load [SQLXML], .NET environment
ms.assetid: b85df83b-ba56-43bf-bcdf-b2a6fca43276
author: rothja
ms.author: jroth
ms.openlocfilehash: 1ef1bec93a1e0ce04c40f4333fa3450118da08df
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060105"
---
# <a name="using-sqlxml-bulk-load-in-the-net-environment"></a>Usando o Carregamento em Massa de SQLXML no ambiente .NET
  Este tópico explica como a funcionalidade de Carregamento em Massa de XML pode ser usada no ambiente .NET. Para obter informações detalhadas sobre o carregamento em massa de XML, consulte [executando o carregamento em massa de dados XML &#40;SQLXML 4,0&#41;](bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md).  
  
 Para usar o objeto COM do Carregamento em Massa de SQLXML de um ambiente gerenciado, você precisa adicionar uma referência de projeto a esse objeto. Isso gera uma interface de wrapper gerenciado em torno do objeto COM do Carregamento em Massa.  
  
> [!NOTE]  
>  O Carregamento em Massa de XML gerenciado não funciona com fluxos gerenciados e exige um wrapper em torno dos fluxos nativos. O componente de Carregamento em Massa de SQLXML não será executado em um ambiente multithread (atributo '[MTAThread]'). Se você tentar executar o componente de carregamento em massa em um ambiente de vários threads, obterá uma exceção InvalidCastException com as seguintes informações adicionais: "QueryInterface para a interface SQLXMLBULKLOADLib. ISQLXMLBulkLoad falhou." A solução alternativa é tornar o objeto que contém o objeto de carregamento em massa acessível por thread único (por exemplo, usando o atributo **[STAThread]** , como mostrado no exemplo).  
  
 Este tópico fornece um exemplo de aplicativo C# funcional para carregamento em massa de dados XML no banco de dados. Para criar um exemplo funcional, siga estas etapas:  
  
1.  Crie as tabelas a seguir:  
  
    ```  
    CREATE TABLE Ord (  
             OrderID     int identity(1,1)  PRIMARY KEY,  
             CustomerID  varchar(5))  
    GO  
    CREATE TABLE Product (  
             ProductID   int identity(1,1) PRIMARY KEY,  
             ProductName varchar(20))  
    GO  
    CREATE TABLE OrderDetail (  
           OrderID     int FOREIGN KEY REFERENCES Ord(OrderID),  
           ProductID   int FOREIGN KEY REFERENCES Product(ProductID),  
                       CONSTRAINT OD_key PRIMARY KEY (OrderID, ProductID))  
    GO  
    ```  
  
2.  Salve o seguinte esquema em um arquivo (schema.xml):  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
    <xsd:annotation>  
      <xsd:appinfo>  
        <sql:relationship name="OrderOD"  
              parent="Ord"  
              parent-key="OrderID"  
              child="OrderDetail"  
              child-key="OrderID" />  
  
        <sql:relationship name="ODProduct"  
              parent="OrderDetail"  
              parent-key="ProductID"  
              child="Product"  
              child-key="ProductID"   
              inverse="true"/>  
      </xsd:appinfo>  
    </xsd:annotation>  
  
      <xsd:element name="Order" sql:relation="Ord"   
                                sql:key-fields="OrderID" >  
       <xsd:complexType>  
         <xsd:sequence>  
            <xsd:element name="Product" sql:relation="Product"   
                         sql:key-fields="ProductID"  
                         sql:relationship="OrderOD ODProduct">  
              <xsd:complexType>  
                 <xsd:attribute name="ProductID" type="xsd:int" />  
                 <xsd:attribute name="ProductName" type="xsd:string" />  
              </xsd:complexType>  
            </xsd:element>  
         </xsd:sequence>  
            <xsd:attribute name="OrderID"   type="xsd:integer" />   
            <xsd:attribute name="CustomerID"   type="xsd:string" />  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  Salve o seguinte exemplo de documento XML em um arquivo (data.xml):  
  
    ```  
    <ROOT>    
      <Order OrderID="11" CustomerID="ALFKI">  
        <Product ProductID="11" ProductName="Chai" />  
        <Product ProductID="22" ProductName="Chang" />  
      </Order>  
      <Order OrderID="22" CustomerID="ANATR">  
         <Product ProductID="33" ProductName="Aniseed Syrup" />  
        <Product ProductID="44" ProductName="Gumbo Mix" />  
      </Order>  
    </ROOT>  
    ```  
  
4.  Inicie o Visual Studio.  
  
5.  Crie um aplicativo de console C#.  
  
6.  No menu **projeto** , selecione **Adicionar referência**.  
  
7.  Na guia **com** , selecione **biblioteca de tipos do Microsoft SQLXML carregamento em massa 4,0** (xblkld4.dll) e clique em **OK**. Você verá o assembly **Interop. SQLXMLBULKLOADLib** criado no projeto.  
  
8.  Substitua o método Main() pelo código a seguir. Atualize a propriedade **ConnectionString** e o caminho do arquivo para o esquema e os arquivos de dados.  
  
    ```  
    [STAThread]  
       static void Main(string[] args)  
       {     
             try  
             {  
                SQLXMLBULKLOADLib.SQLXMLBulkLoad4Class objBL = new SQLXMLBULKLOADLib.SQLXMLBulkLoad4Class();  
                objBL.ConnectionString = "Provider=sqloledb;server=server;database=databaseName;integrated security=SSPI";  
                objBL.ErrorLogFile = "error.xml";  
                objBL.KeepIdentity = false;  
                objBL.Execute ("schema.xml","data.xml");  
             }  
             catch(Exception e)  
             {  
             Console.WriteLine(e.ToString());  
             }  
       }  
    ```  
  
9. Para carregar o XML na tabela que você criou, compile e execute o projeto.  
  
    > [!NOTE]  
    >  A referência para o componente de Carregamento em Massa (xblkld4.dll) também pode ser acionada usando a ferramenta tlbimp.exe, que está disponível como parte da estrutura .NET. Essa ferramenta cria um wrapper gerenciado para a DLL nativa (xblkld4.dll) que pode ser usada em qualquer projeto do .NET. Por exemplo:  
  
    ```  
    c:\>tlbimp xblkld4.dll  
    ```  
  
     Isso cria a DLL do wrapper gerenciado (SQLXMLBULKLOADLib.dll) que você pode usar no projeto do .NET Framework. No .NET Framework, você adiciona referência de projeto à DLL recém-criada.  
  
## <a name="see-also"></a>Consulte Também  
 [Como executar o carregamento em massa de dados XML &#40;SQLXML 4.0&#41;](bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)  
  
  
