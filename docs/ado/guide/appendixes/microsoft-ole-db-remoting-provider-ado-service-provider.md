---
title: Comunicação remota do Microsoft OLE DB Provider (provedor de serviços de ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB remoting provider [ADO]
- providers [ADO], OLE DB remoting provider
- remoting provider [ADO]
ms.assetid: a4360ed4-b70f-4734-9041-4025d033346b
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b69c6f64de019aadf71476958c26f99a46dabac2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-ole-db-remoting-provider-overview"></a>Visão geral do provedor Microsoft OLE DB remotamente
O Microsoft OLE DB provedor remoto permite que um usuário local em um computador cliente invocar os provedores de dados em um computador remoto. Especifique os parâmetros de provedor de dados para o computador remoto como se fosse um usuário local no computador remoto. Em seguida, especifique os parâmetros usados pelo provedor de comunicação remota para acessar o computador remoto. Em seguida, você pode acessar o computador remoto como se fosse um usuário local.

> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).

## <a name="provider-keyword"></a>Palavra-chave do provedor
 Para chamar o provedor OLE DB comunicação remota, especifique a seguinte palavra-chave e valor na cadeia de conexão. (Observe o espaço em branco no nome do provedor).

```
"Provider=MS Remote"
```

## <a name="additional-keywords"></a>Palavras-chave adicionais
 Quando esse provedor de serviços é chamado, as palavras-chave adicionais a seguir são relevantes.

|Palavra-chave|Description|
|-------------|-----------------|
|**Fonte de dados**|Especifica o nome da fonte de dados remoto. Ele é passado para o provedor OLE DB Remoting para processamento.<br /><br /> Esta palavra-chave é equivalente a [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) do objeto [conectar](../../../ado/reference/rds-api/connect-property-rds.md) propriedade.|

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 Quando esse provedor de serviços é chamado, as propriedades dinâmicas a seguir são adicionadas para o [Conexão](../../../ado/reference/ado-api/connection-object-ado.md)do objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.

|Nome de propriedade dinâmica|Description|
|---------------------------|-----------------|
|**DFMode**|Indica o modo DataFactory. Uma cadeia de caracteres que especifica a versão desejada do [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto no servidor. Defina essa propriedade antes de abrir uma conexão para solicitar uma versão específica da **DataFactory**. Se a versão solicitada não estiver disponível, será feita uma tentativa para usar a versão anterior. Se não houver nenhuma versão anterior, ocorrerá um erro. Se **DFMode** é menor do que a versão disponível, ocorrerá um erro. Essa propriedade é somente leitura depois que uma conexão é estabelecida.<br /><br /> Pode ser um dos seguintes valores de cadeia de caracteres válida:<br /><br /> -"25" — versão 2.5 (padrão)<br />-"21", versão 2.1<br />-"20", versão 2.0<br />-"15", versão 1.5|
|**Propriedades de comando**|Indica os valores que serão adicionados à cadeia de caracteres de propriedades de comando (linhas) enviados ao servidor pelo provedor Remote MS. O valor padrão para essa cadeia de caracteres é vt_empty.|
|**DFMode atual**|Indica o número de versão real de **DataFactory** no servidor. Verifique se a propriedade para ver se a versão solicitada no **DFMode** propriedade sido cumprida.<br /><br /> Pode ser um dos seguintes valores de inteiro longo válido:<br /><br /> -25 – versão 2.5 (padrão)<br />-21-versão 2.1<br />-20 – versão 2.0<br />-15 – versão 1.5<br /><br /> Adicionando "DFMode = 20;" para a cadeia de caracteres de conexão ao usar o **MSRemote** provedor pode melhorar o desempenho do servidor quando a atualização de dados. Com essa configuração, o **RDSServer.DataFactory** objeto no servidor usa um modo de uso menos intensivo de recursos. No entanto, os seguintes recursos não estão disponíveis nesta configuração:<br /><br /> -Usar consultas parametrizadas.<br />-Obtendo informações de parâmetro ou coluna antes de chamar o **Execute** método.<br />-Configuração **Transact atualizações** para **True**.<br />-Ao obter o status de linha.<br />-Chamando o **Resync** método.<br />-Atualizando (explicitamente ou automaticamente) por meio de **atualização Resync** propriedade.<br />-Configuração **comando** ou **registros** propriedades.<br />-Usando **adCmdTableDirect**.|
|**Manipulador**|Indica o nome de um programa de personalização do lado do servidor (ou manipulador) que estende a funcionalidade do [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)e os parâmetros usados pelo manipulador de *,* todos separados por vírgulas ( ","). Um **cadeia de caracteres** valor.|
|**Tempo limite de Internet**|Indica o número máximo de milissegundos para aguardar uma solicitação para viajar para e do servidor. (O padrão é 5 minutos.)|
|**Provedor remoto**|Indica o nome do provedor de dados a ser usado no servidor remoto.|
|**Servidor remoto**|Indica o protocolo de comunicação e o nome do servidor a ser usado por esta conexão. Essa propriedade é equivalente a [RDS. DataContro](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto [Server](../../../ado/reference/rds-api/server-property-rds.md) propriedade.|
|**Transact atualizações**|Quando definido como **True**, esse valor indica que, quando [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) é executada no servidor, ele será feito em uma transação. O valor padrão desta propriedade booliana de dinâmico é **False**.|

 Você também pode definir propriedades dinâmicas graváveis especificando seus nomes como palavras-chave na cadeia de conexão. Por exemplo, definir a **tempo limite de Internet** propriedade dinâmica a cinco segundos, especificando:

```
Dim cn as New ADODB.Connection
cn.Open "Provider=MS Remote;Internet Timeout=5000"
```

 Você também pode definir ou recuperar uma propriedade dinâmica especificando seu nome como o índice para o **propriedades** propriedade. O exemplo a seguir mostra como obter e imprimir o valor atual de **tempo limite de Internet** propriedades dinâmicas e em seguida, defina um novo valor:

```
Debug.Print cn.Properties("Internet Timeout")
cn.Properties("Internet Timeout") = 5000
```

## <a name="remarks"></a>Remarks
 No ADO 2.0, o provedor OLE DB comunicação remota pode ser especificado somente no *ActiveConnection* parâmetro do [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto **abrir** método. Começando com o ADO 2.1, o provedor também pode ser especificado no *ConnectionString* parâmetro do [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto **abrir** método.

 O equivalente a **RDS. DataControl** objeto [SQL](../../../ado/reference/rds-api/sql-property.md) propriedade não está disponível. O [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto **abrir** método *fonte* argumento é usado em vez disso.

 **Observação** especificando "...; Provedor remoto = MS Remote;... "criaria um cenário de quatro níveis. Cenários além de três camadas não foram testados e não será necessária.

## <a name="example"></a>Exemplo
 Este exemplo executa uma consulta no **autores** analítico o **Pubs** banco de dados em um servidor chamado *Seu_servidor*. Os nomes da fonte de dados remota e do servidor remoto são fornecidos no [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) método do[Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto e a consulta SQL é especificado no[abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) método do [Registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Um **registros** objeto é retornado, editado e usado para atualizar a fonte de dados.

```
Dim rs as New ADODB.Recordset
Dim cn as New ADODB.Connection
cn.Open  "Provider=MS Remote;Data Source=pubs;" & _
         "Remote Server=http://YourServer"
rs.Open "SELECT * FROM authors", cn
...                'Edit the recordset
rs.UpdateBatch     'Equivalent of RDS SubmitChanges
...
```

## <a name="see-also"></a>Consulte também
 [Visão geral do provedor OLE DB remotamente](http://msdn.microsoft.com/en-us/4083b72f-68c4-4252-b366-abb70db5ca2b)
