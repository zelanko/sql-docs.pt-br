---
title: Introdução ao provedor SQLXMLOLEDB (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, properties
- adExecuteStream flag
- SQLXMLOLEDB Provider, about SQLXMLOLEDB Provider
ms.assetid: 2e3f3817-4209-4bf4-9f46-248c95bc6f1b
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 06bd27e4151adf3e30cacd32bf27b4547e1e3bc3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649524"
---
# <a name="introduction-to-the-sqlxmloledb-provider-sqlxml-40"></a>Introdução ao provedor SQLXMLOLEDB (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  O provedor SQLXMLOLEDB é um provedor OLE DB que expõe a funcionalidade SQLXML [!INCLUDE[msCoName](../../../includes/msconame-md.md)] através do ADO (ActiveX Data Objects). No entanto, o provedor só pode executar comandos no modo "write to an output stream" do ADO. SQLXMLOLEDB não é um provedor de conjunto de linhas. Quando você executar um comando, você deve especificar o sinalizador adExecuteStream, que direciona o ADO para usar o fluxo de saída que você especificou.  
  
 O exemplo a seguir mostra a sintaxe para o comando executar no qual o sinalizador adExecuteStream é especificado:  
  
```  
Dim oTestCommand As New ADODB.Command  
...  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Execute , , adExecuteStream  
...  
```  
  
## <a name="sqlxmloledb-provider-specific-properties"></a>Propriedades específicas do provedor SQLXMLOLEDB  
 O provedor SQLXMLOLEDB expõe a seguinte propriedade de conexão específica do provedor:  
  
|Conexão<br /><br /> propriedade|Padrão<br /><br /> (se houver)|Description|  
|-----------------------------|----------------------------|-----------------|  
|Provedor de Dados||Fornece o PROGID do provedor OLE DB através do qual o SQLXMLOLEDB executa os comandos. A partir do SQLXML 4.0 e do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], este provedor passou a fazer parte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, portanto, o valor dessa propriedade se restringe a "SQLNCLI11". Para obter mais informações, veja [Programação do SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md).|  
  
 O provedor SQLXMLOLEDB expõe as seguintes propriedades de comando específicas do provedor:  
  
|Comando<br /><br /> propriedade|Padrão<br /><br /> (se houver)|Description|  
|--------------------------|----------------------------|-----------------|  
|Caminho base|""|Especifica o caminho do arquivo de base. O caminho do arquivo de base é usado para indicar o local dos arquivos de esquema de mapeamento ou XSL (Stylesheet Language) XML. O caminho do arquivo de base também é usado para resolver os caminhos relativos de arquivos de esquema que foram especificados nas propriedades do esquema de mapeamento ou XSL de mapeamento ou XSL.<br /><br /> Para obter um exemplo no qual essa propriedade é usada, consulte [executar consultas de XPath &#40;provedor SQLXMLOLEDB&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-sqlxmloledb-provider.md).|  
|ClientSideXML|Falso|Defina esta propriedade como True se quiser que o processo de conversão do conjunto de linhas em XML ocorra no cliente, e não no servidor. Isso é útil quando você deseja mover a carga de desempenho para a camada intermediária.<br /><br /> Para obter um exemplo no qual essa propriedade é usada, consulte [executar consultas de SQL &#40;provedor SQLXMLOLEDB&#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-sql-queries-sqlxmloledb-provider.md) ou [executando modelos que contêm consultas SQL &#40;provedor SQLXMLOLEDB&#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-templates-that-contain-sql-queries-sqlxmloledb-provider.md).|  
|Tipo de Conteúdo||Retorna o tipo de conteúdo de saída. Esta é uma propriedade SOMENTE LEITURA.<br /><br /> Esta propriedade fornece informações ao navegador sobre o tipo de conteúdo (como TEXT/XML, TEXT/HTML, imagem/jpeg, e assim por diante). O valor dessa propriedade se torna a **tipo de conteúdo** campo que é enviado ao navegador como parte do cabeçalho HTTP, que contém o-tipo MIME (Multipurpose Internet Mail Extensions) do documento que está sendo enviado como o corpo.|  
|Esquema de mapeamento|NULL|Se um aplicativo cliente executar uma consulta XPath em um esquema de mapeamento (XDR ou XSD), esta propriedade será usada para especificar o nome do esquema de mapeamento.<br /><br /> O caminho especificado pode ser relativo (xyz/abc/MySchema.xml) ou absoluto (C:\MyFolder\abc\MySchema.xml).<br /><br /> Se um caminho relativo for especificado, o caminho base que é especificado pela propriedade caminho Base é usado para resolver o caminho relativo. Se nenhum caminho foi especificado na propriedade do caminho de Base, o caminho relativo é relativo ao diretório atual.<br /><br /> Especificar um valor para a propriedade do esquema de mapeamento, você pode especificar um caminho de diretório local ou uma URL (http://...). Se você especificar uma URL, deverá configurar WinHTTP para acessar os servidores HTTP e HTTPS por meio de um servidor proxy. Para isso, use o utilitário Proxycfg.exe. Para obter mais informações, consulte "Usando o Utilitário de Configuração do WinHTTP Proxy" na Biblioteca MSDN.<br /><br /> Para obter um exemplo no qual essa propriedade é usada, consulte [executar consultas de XPath &#40;provedor SQLXMLOLEDB&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-sqlxmloledb-provider.md).|  
|namespaces||Esta propriedade permite a execução de consultas XPath que usam namespaces. Para obter um exemplo no qual essa propriedade é usada, consulte [executar consultas do XPath com Namespaces &#40;provedor SQLXMLOLEDB&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-with-namespaces-sqlxmloledb-provider.md).|  
|ss Stream Flags||Esta propriedade é usada para definir tipos específicos de restrições de segurança. Por exemplo, talvez você não queira permitir referências URL a arquivos ou caminhos absolutos para arquivos (como sites externos). Ou você pode optar por não permitir consultas nos modelos.<br /><br /> É possível atribuir estes valores à propriedade:<br /><br /> 1 = STREAM_FLAGS_DISALLOW_URL 2 = STREAM_FLAGS_DISALLOW_ABSOLUTE_PATH 4 = STREAM_FLAGS_DISALLOW_QUERY 8 = STREAM_FLAGS_       DONTCACHEMAPPINGSCHEMA 16 = STREAM_FLAGS_DONTCACHETEMPLATE 32 = STREAM_FLAGS_DONTCACHEXSL<br /><br /> Informações adicionais sobre esses valores são fornecidas na próxima tabela.|  
|xml root||Esta propriedade é usada para definir uma marca raiz para o XML resultante. Por exemplo, se você executar consultas SQL no banco de dados e o documento XML resultante não tiver um elemento raiz, o valor da propriedade será usado para adicionar um elemento raiz ao documento.<br /><br /> Para obter um exemplo no qual essa propriedade é usada, consulte [executar consultas de SQL &#40;provedor SQLXMLOLEDB&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-sql-queries-sqlxmloledb-provider.md).|  
|xsl||Esta propriedade é usada para especificar o nome do arquivo XSL quando você deseja aplicar a transformação XSL ao documento XML retornado pela consulta.<br /><br /> O caminho especificado pode ser relativo (xyz/abc/MyXSL.xsl) ou absoluto (C:\MyFolder\abc\MyXSL.xsl).<br /><br /> Se um caminho relativo for especificado, o caminho base que é especificado pela propriedade caminho Base é usado para resolver o caminho relativo. Se nenhum caminho foi especificado na propriedade do caminho de Base, o caminho relativo é relativo ao diretório atual.<br /><br /> Veja um exemplo no qual essa propriedade é usada, aplicando uma transformação XSL (provedor SQLXMLOLEDB).|  
  
 A tabela a seguir contém descrições do ss valores de propriedade de sinalizadores de Stream.  
  
|Valor da propriedade|Description|  
|--------------------|-----------------|  
|STREAM_FLAGS_DISALLOW_URL|Não são aceitas URLs para esquemas de mapeamento ou XSL.|  
|STREAM_FLAGS_DISALLOW_ABSOLTE_PATH|Um caminho especificado para um esquema de mapeamento ou para XSL deve ser relativo ao caminho de base do próprio modelo.|  
|STREAM_FLAGS_DISALLOW_QUERY|Não são permitidas consultas em um modelo.|  
|STREAM_FLAGS_DONTCACHEMAPPINGSCHEMA|O esquema de mapeamento não é armazenado em cache. Este valor de propriedade é útil durante a fase de desenvolvimento do banco de dados, quando esquemas de banco de dados estão sujeitos a alteração.|  
|STREAM_FLAGS_DONTCACHETEMPLATE|Os modelos não são armazenados em cache.|  
|STREAM_FLAGS_DONTCACHEXSL|XSL não é armazenada em cache.|  
  
  
