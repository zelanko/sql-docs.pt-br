---
description: Provedor de comunicação remota do Microsoft OLE DB (provedor de serviços ADO)
title: Provedor de comunicação remota do Microsoft OLE DB (provedor de serviços ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB remoting provider [ADO]
- providers [ADO], OLE DB remoting provider
- remoting provider [ADO]
ms.assetid: a4360ed4-b70f-4734-9041-4025d033346b
author: rothja
ms.author: jroth
ms.openlocfilehash: 2e8520dc35b7a6d913736637cabaf34a2bd60651
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806541"
---
# <a name="microsoft-ole-db-remoting-provider-overview"></a>Visão geral do provedor de comunicação remota do Microsoft OLE DB
O provedor de comunicação remota do Microsoft OLE DB permite que um usuário local em um computador cliente invoque provedores de dados em um computador remoto. Especifique os parâmetros do provedor de dados para o computador remoto como você faria se fosse um usuário local no computador remoto. Em seguida, especifique os parâmetros usados pelo provedor de comunicação remota para acessar o computador remoto. Em seguida, você pode acessar o computador remoto como se você fosse um usuário local.

> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o  [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).

## <a name="provider-keyword"></a>Palavra-chave Provider
 Para invocar o provedor de comunicação remota OLE DB, especifique a palavra-chave e o valor a seguir na cadeia de conexão. (Observe o espaço em branco no nome do provedor.)

```vb
"Provider=MS Remote"
```

## <a name="additional-keywords"></a>Palavras-chave adicionais
 Quando esse provedor de serviços é invocado, as palavras-chave adicionais a seguir são relevantes.

|Palavra-chave|Descrição|
|-------------|-----------------|
|**Fonte de Dados**|Especifica o nome da fonte de dados remota. Ele é passado para o provedor de comunicação remota OLE DB para processamento.<br /><br /> Essa palavra-chave é equivalente ao [RDS. ](../../reference/rds-api/datacontrol-object-rds.md) Propriedade [Connect](../../reference/rds-api/connect-property-rds.md) do objeto DataControl.|

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 Quando esse provedor de serviços é invocado, as propriedades dinâmicas a seguir são adicionadas à coleção de [Propriedades](../../reference/ado-api/properties-collection-ado.md) do objeto de [conexão](../../reference/ado-api/connection-object-ado.md).

|Nome da propriedade dinâmica|Descrição|
|---------------------------|-----------------|
|**DFMode**|Indica o modo datafactory. Uma cadeia de caracteres que especifica a versão desejada do objeto [DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md) no servidor. Defina essa propriedade antes de abrir uma conexão para solicitar uma versão específica do **DataFactory**. Se a versão solicitada não estiver disponível, será feita uma tentativa de usar a versão anterior. Se não houver nenhuma versão anterior, ocorrerá um erro. Se **DFMode** for menor que a versão disponível, ocorrerá um erro. Essa propriedade é somente leitura depois que uma conexão é estabelecida.<br /><br /> Pode ser um dos seguintes valores de cadeia de caracteres válidos:<br /><br /> -"25"-versão 2,5 (padrão)<br />-"21"-versão 2,1<br />-"20"-versão 2,0<br />-"15"-versão 1,5|
|**Propriedades do comando**|Indica os valores que serão adicionados à cadeia de caracteres de propriedades de comando (conjunto de linhas) enviadas ao servidor pelo provedor remoto MS. O valor padrão dessa cadeia de caracteres é vt_empty.|
|**DFMode atual**|Indica o número de versão real do **DataFactory** no servidor. Verifique essa propriedade para ver se a versão solicitada na propriedade **DFMode** foi respeitada.<br /><br /> Pode ser um dos seguintes valores inteiros longos válidos:<br /><br /> -25-versão 2,5 (padrão)<br />-21-versão 2,1<br />-20-versão 2,0<br />-15-versão 1,5<br /><br /> Adicionar "DFMode = 20;" à sua cadeia de conexão ao usar o provedor **MSRemote** pode melhorar o desempenho do servidor ao atualizar dados. Com essa configuração, o objeto **RDSServer. datafactory** no servidor usa um modo menos intensivo de recursos. No entanto, os seguintes recursos não estão disponíveis nesta configuração:<br /><br /> -Usando consultas parametrizadas.<br />-Obtendo informações de parâmetro ou coluna antes de chamar o método **Execute** .<br />-Definindo **as atualizações do Transact** como **true**.<br />-Obtendo status de linha.<br />-Chamando o método de **ressincronização** .<br />-Atualizando (explicitamente ou automaticamente) por meio da propriedade **Atualizar ressincronização** .<br />-Definindo propriedades de **comando** ou **conjunto de registros** .<br />-Usando **adCmdTableDirect**.|
|**Manipulador**|Indica o nome de um programa de personalização do lado do servidor (ou manipulador) que estende a funcionalidade do [RDSServer. datafactory](../../reference/rds-api/datafactory-object-rdsserver.md)e quaisquer parâmetros usados pelo manipulador, todos separados por vírgulas (","). Um valor de **cadeia de caracteres** .|
|**Tempo limite da Internet**|Indica o número máximo de milissegundos para aguardar uma solicitação de viagem de e para o servidor. (O padrão é 5 minutos.)|
|**Provedor remoto**|Indica o nome do provedor de dados a ser usado no servidor remoto.|
|**Servidor remoto**|Indica o nome do servidor e o protocolo de comunicação a ser usado por essa conexão. Essa propriedade é equivalente ao [RDS. ](../../reference/rds-api/datacontrol-object-rds.md) Propriedade [do servidor](../../reference/rds-api/server-property-rds.md) de objetos DataContro.|
|**Atualizações do Transact**|Quando definido como **true**, esse valor indica que quando [UpdateBatch](../../reference/ado-api/updatebatch-method.md) é executado no servidor, ele será feito dentro de uma transação. O valor padrão para essa propriedade dinâmica booliana é **false**.|

 Você também pode definir propriedades dinâmicas graváveis especificando seus nomes como palavras-chave na cadeia de conexão. Por exemplo, defina a propriedade dinâmica **tempo limite da Internet** como cinco segundos, especificando:

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MS Remote;Internet Timeout=5000"
```

 Você também pode definir ou recuperar uma propriedade dinâmica especificando seu nome como o índice para a propriedade **Properties** . O exemplo a seguir mostra como obter e imprimir o valor atual da propriedade dinâmica de **tempo limite da Internet** e, em seguida, definir um novo valor:

```vb
Debug.Print cn.Properties("Internet Timeout")
cn.Properties("Internet Timeout") = 5000
```

## <a name="remarks"></a>Comentários
 No ADO 2,0, o provedor de comunicação remota OLE DB só podia ser especificado no parâmetro *ActiveConnection* do método **Open** do objeto [Recordset](../../reference/ado-api/recordset-object-ado.md) . A partir do ADO 2,1, o provedor também pode ser especificado no parâmetro *ConnectionString* do método **Open** do objeto [Connection](../../reference/ado-api/connection-object-ado.md) .

 O equivalente do **RDS. ** A propriedade [SQL](../../reference/rds-api/sql-property.md) do objeto DataControl não está disponível. Em vez disso, o argumento de *origem* do método **Open** do objeto [Recordset](../../reference/ado-api/recordset-object-ado.md) é usado.

 **Observação** Especificando "...; Provedor remoto = MS remoto;... " criaria um cenário de quatro camadas. Os cenários além de três camadas não foram testados e não devem ser necessários.

## <a name="example"></a>Exemplo
 Este exemplo executa uma consulta na tabela **autores** do banco de dados **pubs** em um servidor chamado *YourServer*. Os nomes da fonte de dados remota e do servidor remoto são fornecidos no método [Open](../../reference/ado-api/open-method-ado-connection.md) do objeto[Connection](../../reference/ado-api/connection-object-ado.md) , e a consulta SQL é especificada no método[Open](../../reference/ado-api/open-method-ado-recordset.md) do objeto [Recordset](../../reference/ado-api/recordset-object-ado.md) . Um objeto **Recordset** é retornado, editado e usado para atualizar a fonte de dados.

```vb
Dim rs as New ADODB.Recordset
Dim cn as New ADODB.Connection
cn.Open  "Provider=MS Remote;Data Source=pubs;" & _
         "Remote Server=https://YourServer"
rs.Open "SELECT * FROM authors", cn
...                'Edit the recordset
rs.UpdateBatch     'Equivalent of RDS SubmitChanges
...
```

## <a name="see-also"></a>Consulte Também
 [Visão geral do provedor de comunicação remota OLE DB](/previous-versions/windows/desktop/ms713673(v=vs.85))