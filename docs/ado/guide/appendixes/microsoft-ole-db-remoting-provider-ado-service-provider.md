---
title: Comunicação remota do Microsoft OLE DB Provider (provedor de serviços do ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 99fe38d78ff146503995a3e28dbe186b04be870d
ms.sourcegitcommit: d9c5b9ab3c282775ed61712892eeb3e150ccc808
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67597489"
---
# <a name="microsoft-ole-db-remoting-provider-overview"></a>Visão geral do provedor Microsoft OLE DB remotamente
O Microsoft OLE DB provedor remoto permite que um usuário local em um computador cliente invocar os provedores de dados em um computador remoto. Especifique os parâmetros de provedor de dados para o computador remoto, como você faria se fosse um usuário local no computador remoto. Em seguida, especifique os parâmetros usados pelo provedor de comunicação remota para acessar o computador remoto. Em seguida, você pode acessar o computador remoto como se fosse um usuário local.

> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).

## <a name="provider-keyword"></a>Palavra-chave do provedor
 Para invocar o provedor OLE DB comunicação remota, especifique a seguinte palavra-chave e valor na cadeia de conexão. (Observe o espaço em branco no nome do provedor).

```vb
"Provider=MS Remote"
```

## <a name="additional-keywords"></a>Palavras-chave adicionais
 Quando esse provedor de serviço é chamado, as palavras-chave adicionais a seguir são relevantes.

|Palavra-chave|Descrição|
|-------------|-----------------|
|**Fonte de dados**|Especifica o nome da fonte de dados remota. Ele é passado para o provedor OLE DB comunicação remota para processamento.<br /><br /> Essa palavra-chave é equivalente ao [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) do objeto [Connect](../../../ado/reference/rds-api/connect-property-rds.md) propriedade.|

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 Quando esse provedor de serviço é chamado, as seguintes propriedades dinâmicas são adicionadas para o [Conexão](../../../ado/reference/ado-api/connection-object-ado.md)do objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.

|Nome da propriedade dinâmica|Descrição|
|---------------------------|-----------------|
|**DFMode**|Indica o modo do DataFactory. Uma cadeia de caracteres que especifica a versão desejada do [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto no servidor. Defina essa propriedade antes de abrir uma conexão para solicitar uma versão específica do **DataFactory**. Se a versão solicitada não estiver disponível, será feita uma tentativa para usar a versão anterior. Se não houver nenhuma versão anterior, ocorrerá um erro. Se **DFMode** é menor que a versão disponível, ocorrerá um erro. Essa propriedade é somente leitura depois que uma conexão é feita.<br /><br /> Pode ser um dos seguintes valores de cadeia de caracteres válida:<br /><br /> -"25"-versão 2.5 (padrão)<br />-   "21"-Version 2.1<br />-   "20"-Version 2.0<br />-"15"-versão 1.5|
|**Propriedades de comando**|Indica os valores que serão adicionados à cadeia de caracteres de propriedades de comando (conjunto de linhas) enviada ao servidor pelo provedor Remote MS. O valor padrão para essa cadeia de caracteres é vt_empty.|
|**DFMode atual**|Indica o número de versão real a **DataFactory** no servidor. Verifique se a propriedade para ver se a versão solicitada na **DFMode** propriedade tiver sido cumprida.<br /><br /> Pode ser um dos seguintes valores de inteiro longo válido:<br /><br /> -25-versão 2.5 (padrão)<br />-21-versão 2.1<br />-20-versão 2.0<br />-15-versão 1.5<br /><br /> Adicionando "DFMode = 20;" à cadeia de conexão ao usar o **MSRemote** provedor pode melhorar o desempenho do servidor quando a atualização de dados. Com essa configuração, o **RDSServer.DataFactory** objeto no servidor usa um modo menos intensivo de recursos. No entanto, os seguintes recursos não estão disponíveis nesta configuração:<br /><br /> -Usando consultas parametrizadas.<br />– Obtendo informações de parâmetro ou coluna antes de chamar o **Execute** método.<br />-Configuração **Transact atualizações** à **verdadeiro**.<br />-Ao obter o status de linha.<br />-O chamando o **ressincronizar** método.<br />-Atualizando (explícita ou automaticamente) por meio de **atualização ressincronizar** propriedade.<br />-Configuração **comando** ou **Recordset** propriedades.<br />-Usando **adCmdTableDirect**.|
|**Manipulador**|Indica o nome de um programa de personalização do lado do servidor (ou manipulador) que estende a funcionalidade dos [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), e os parâmetros usados pelo manipulador, todos separados por vírgulas (","). Um valor de **String**.|
|**Tempo limite da Internet**|Indica o número máximo de milissegundos de espera de uma solicitação para viajar para e do servidor. (O padrão é 5 minutos.)|
|**Provedor remoto**|Indica o nome do provedor de dados a ser usado no servidor remoto.|
|**Servidor remoto**|Indica o protocolo de comunicação e o nome do servidor a ser usado por esta conexão. Essa propriedade é equivalente ao [RDS. DataContro](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto [Server](../../../ado/reference/rds-api/server-property-rds.md) propriedade.|
|**Transact atualizações**|Quando definido como **verdadeira**, esse valor indica que, quando [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) é executada no servidor, ele será feito dentro de uma transação. É o valor padrão para essa propriedade dinâmica de booliana **falsos**.|

 Você também pode definir propriedades dinâmicas graváveis, especificando seus nomes como palavras-chave na cadeia de conexão. Por exemplo, defina as **tempo limite de Internet** propriedade dinâmica para cinco segundos, especificando:

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MS Remote;Internet Timeout=5000"
```

 Você também pode definir ou recuperar uma propriedade dinâmica especificando seu nome como o índice para o **propriedades** propriedade. O exemplo a seguir mostra como obter e imprimir o valor atual do **tempo limite de Internet** propriedade dinâmica e defina um novo valor:

```vb
Debug.Print cn.Properties("Internet Timeout")
cn.Properties("Internet Timeout") = 5000
```

## <a name="remarks"></a>Comentários
 No ADO 2.0, o provedor OLE DB comunicação remota pode ser especificado somente na *ActiveConnection* parâmetro do [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto **abrir** método. Começando com o ADO 2.1, o provedor também pode ser especificado na *ConnectionString* parâmetro do [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto **abrir** método.

 O equivalente a **RDS. DataControl** objeto [SQL](../../../ado/reference/rds-api/sql-property.md) propriedade não está disponível. O [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto **abra** método *origem* argumento é usado em vez disso.

 **Observação** especificando "...; Provedor remoto = MS Remote;... "criaria um cenário de quatro camadas. Cenários além de três camadas não foram testados e não devem ser necessário.

## <a name="example"></a>Exemplo
 Este exemplo executa uma consulta na **autores** tabela da **Pubs** banco de dados em um servidor denominado *Seu_servidor*. Os nomes da fonte de dados remota e servidor remoto são fornecidos no [aberto](../../../ado/reference/ado-api/open-method-ado-connection.md) método da[Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto e a consulta SQL é especificada no[abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) método da [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Um **Recordset** objeto é retornado, editado e usado para atualizar a fonte de dados.

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

## <a name="see-also"></a>Consulte também
 [Visão geral do provedor OLE DB remotamente](https://msdn.microsoft.com/4083b72f-68c4-4252-b366-abb70db5ca2b)
