---
title: Objeto SqlXmlCommand (Classes gerenciadas SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- void ExecuteNonQuery() method
- namespaces property
- Stream ExecuteStream() method
- CommandType property
- RootTag property
- OutputEncoding property
- XmlReader ExecuteXmlReader() method
- Managed Classes [SQLXML], SqlXmlCommand object
- SQLXML Managed Classes, SqlXmlCommand object
- Base Path property
- void ClearParameters() method
- public void ExecuteToStream(Stream outputStream) method
- SqlXmlCommand object
- CommandText property
- XslPath property
- SchemaPath property
- SqlXmlParameter CreateParameter() method
- ClientSideXML property
- CommandStream property
ms.assetid: c1f9e0bb-a89d-4d6a-a96e-289ef516a3a6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 736345b7ee5b9c3e40f0ae34fe139cb911cad42f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740509"
---
# <a name="sqlxmlcommand-object-sqlxml-managed-classes"></a>Objeto SqlXmlCommand (classes gerenciadas SQLXML)
  Este é o construtor para o objeto SqlXmlCommand:  
  
```  
public SqlXmlCommand(string cnString)  
```  
  
 Em que `cnString` é a cadeia de conexão OLEDB ou ADO que identifica o servidor, banco de dados e as informações de logon – por exemplo, `Provider=SQLOLEDB; Server=(local); database=AdventureWorks; Integrated Security=SSPI"`.  
  
 Na cadeia de conexão, o `Provider` precisa ser SQLOLEDB e o `Data Provider` não deve ser incluído na cadeia de caracteres do provedor.  
  
 Para obter um exemplo funcional, consulte [executar consultas de SQL &#40;Classes gerenciadas SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md).  
  
## <a name="methods"></a>Métodos  
 Objeto TheSqlXmlCommand dá suporte a vários métodos, incluindo os seguintes métodos para executar um comando:  
  
 void ExecuteNonQuery)  
 Executa o comando, mas não retorna nada. Este método será útil se você quiser executar um comando nonquery (ou seja, um comando que não retorna nada). Um exemplo é a execução de um diagrama de atualização ou um DiffGram que atualiza registros mas não retorna nada.  
  
 Stream ExecuteStream()  
 Retorna um novo objeto Stream. Este método será útil quando você quiser os resultados de consulta retornados em um novo fluxo. Para obter um exemplo funcional, consulte [executar consultas de SQL &#40;Classes gerenciadas SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md).  
  
 ExecuteToStream public void (Stream outputStream)  
 Escreve os resultados da consulta para um fluxo existente. Esse método é útil quando você tiver um fluxo ao qual você precisa anexar (por exemplo, para que os resultados da consulta escritos para o System.Web.HttpResponse.OutputStream) os resultados. Para obter um exemplo funcional, consulte [executar consultas de SQL &#40;Classes gerenciadas SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md).  
  
 XmlReader ExecuteXmlReader()  
 Retorna um objeto de XmlReader. Você pode usar esse método para manipular diretamente os dados no objeto XmlReader ou plug-in a arquitetura encadeável de System. XML. Para obter mais informações, consulte a documentação do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework. Para obter um exemplo funcional, consulte [executar consultas de SQL usando o método ExecuteXMLReader](executing-sql-queries-by-using-the-executexmlreader-method.md).  
  
 Objeto TheSqlXmlCommand também dá suporte a esses métodos adicionais:  
  
 SqlXmlParameter CreateParameter()  
 Cria um objeto SqlXmlParameter. Você pode definir valores para o *nome* e *valor* parâmetros deste objeto. Este método será útil se você quiser passar parâmetros para um comando. Para obter um exemplo funcional, consulte [executar consultas de SQL &#40;Classes gerenciadas SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md).  
  
 void clearparameters)  
 Desmarca o(s) parâmetro(s) que foi(ram) criado(s) para um determinado objeto de comando. Este método será útil se você quiser executar várias consultas no mesmo objeto de comando.  
  
## <a name="properties"></a>Propriedades  
 O objeto SqlXmlCommand também suporta estas propriedades:  
  
 ClientSideXml  
 Quando definida como True, especifica que a conversão do conjunto de linhas em XML ocorrerá no cliente, e não no servidor. Esta propriedade será útil quando você quiser mover a carga de desempenho para a camada intermediária. A propriedade também permite envolver os procedimentos armazenados existentes com FOR XML para obter saída de XML.  
  
 SchemaPath  
 O nome do esquema de mapeamento juntamente com o caminho de diretório (por exemplo, C:\x\y\MySchema.xml). Esta propriedade será útil para especificar um esquema de mapeamento para consultas XPath. O caminho especificado pode ser absoluto ou relativo. Se o caminho for relativo, o caminho base que é especificado no caminho Base é usado para resolver o caminho relativo. Se nenhum caminho base for especificado, o caminho relativo será relativo ao diretório atual. Para obter um exemplo funcional, consulte [acessando a funcionalidade SQLXML no ambiente .NET](accessing-sqlxml-functionality-in-the-net-environment.md).  
  
 XslPath  
 O nome do arquivo XSL juntamente com o caminho de diretório. O caminho especificado pode ser absoluto ou relativo. Se o caminho for relativo, o caminho base que é especificado no caminho Base é usado para resolver o caminho relativo. Se nenhum caminho base for especificado, o caminho relativo será relativo ao diretório atual. Para obter um exemplo funcional, consulte [aplicando uma transformação XSL &#40;Classes gerenciadas SQLXML&#41;](applying-an-xsl-transformation-sqlxml-managed-classes.md).  
  
 Caminho base  
 O caminho base (um caminho de diretório). Essa propriedade é útil para resolver um caminho relativo que é especificado para um arquivo XSL (usando a propriedade XslPath), um arquivo de esquema de mapeamento (usando a propriedade SchemaPath) ou uma referência de esquema externa em um modelo XML (especificado usando o `mapping-schema` atributo).  
  
 OutputEncoding  
 Especifica a codificação para o fluxo retornado quando o comando é executado. Esta propriedade será útil para solicitar uma codificação específica para o fluxo que é retornado. Algumas codificações geralmente usadas são UTF-8, ANSI e Unicode. UTF-8 é a codificação padrão.  
  
 Namespaces  
 Habilita a execução de consultas XPath que usam namespaces. Para obter mais informações sobre consultas XPath com namespaces, consulte [executar consultas do XPath com Namespaces &#40;Classes gerenciadas SQLXML&#41;](executing-xpath-queries-with-namespaces-sqlxml-managed-classes.md). Para obter um exemplo funcional, consulte [executar consultas de XPath &#40;Classes gerenciadas SQLXML&#41;](executing-xpath-queries-sqlxml-managed-classes.md).  
  
 RootTag  
 Fornece o único elemento raiz para XML gerado pela execução do comando. Um documento XML válido exige uma única marca de nível raiz. Se o comando executado gerar um fragmento XML (sem um único elemento de nível superior), você poderá especificar um elemento raiz para o XML de retorno. Para obter um exemplo funcional, consulte [aplicando uma transformação XSL &#40;Classes gerenciadas SQLXML&#41;](applying-an-xsl-transformation-sqlxml-managed-classes.md).  
  
 CommandText  
 O texto do comando. Esta propriedade será usada para especificar o texto do comando que você quer executar. Para obter um exemplo funcional, consulte [executar consultas de SQL &#40;Classes gerenciadas SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md).  
  
 CommandStream  
 O fluxo de comando. Esta propriedade será útil se você quiser executar um comando de um arquivo (por exemplo, um modelo XML). Quando você estiver usando CommandStream, apenas **"Modelo"**, **"UpdateGram"** e **"DiffGram" CommandType** valores têm suporte. Para obter um exemplo funcional, consulte [executando os arquivos de modelo usando a propriedade CommandStream](executing-template-files-by-using-the-commandstream-property.md).  
  
 CommandType  
 Identifica o tipo de comando. Esta propriedade será usada para especificar o tipo de comando que você quer executar. Os valores da tabela a seguir determinam o tipo do comando. Para obter um exemplo funcional, consulte [acessando a funcionalidade SQLXML no ambiente .NET](accessing-sqlxml-functionality-in-the-net-environment.md).  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SqlXmlCommandType.Sql|Executa um comando SQL (por exemplo, `SELECT * FROM Employees FOR XML AUTO`).|  
|SqlXmlCommandType.XPath|Executa um comando XPath (por exemplo, `Employees[@EmployeeID=1]`).|  
|SqlXmlCommandType.Template|Executa um modelo XML.|  
|SqlXmlCommandType.TemplateFile|Executa um arquivo de modelo no caminho especificado.|  
|SqlXmlCommandType.UpdateGram|Executa um diagrama de atualização.|  
|SqlXmlCommandType.Diffgram|Executa um DiffGram.|  
  
## <a name="see-also"></a>Consulte também  
 [Objeto SqlXmlParameter &#40;Classes gerenciadas SQLXML&#41;](sqlxml-managed-classes-sqlxmlparameter-object.md)   
 [Objeto SqlXmlAdapter &#40;Classes gerenciadas SQLXML&#41;](sqlxml-managed-classes-sqlxmladapter-object.md)  
  
  
