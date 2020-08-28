---
description: Objeto Connection (ADO)
title: Objeto de conexão (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection
helpviewer_keywords:
- Connection object [ADO]
ms.assetid: ef6b1824-5b12-43db-89d7-8f3d13896d4d
author: rothja
ms.author: jroth
ms.openlocfilehash: 38a28bf434998943b07ef6463970c26510195299
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974897"
---
# <a name="connection-object-ado"></a>Objeto Connection (ADO)
Representa uma conexão aberta com uma fonte de dados.  
  
## <a name="remarks"></a>Comentários  
 Um objeto de **conexão** representa uma sessão exclusiva com uma fonte de dados. Em um sistema de banco de dados cliente/servidor, pode ser equivalente a uma conexão de rede real com o servidor. Dependendo da funcionalidade suportada pelo provedor, algumas coleções, métodos ou propriedades de um objeto de **conexão** podem não estar disponíveis.  
  
 Com as coleções, métodos e propriedades de um objeto de **conexão** , você pode fazer o seguinte:  
  
-   Configure a conexão antes de abri-la com as propriedades [ConnectionString](./connectionstring-property-ado.md), [connectionTimeout](./connectiontimeout-property-ado.md)e [Mode](./mode-property-ado.md) . **ConnectionString** é a propriedade padrão do objeto **Connection** .  
  
-   Defina a propriedade [CursorLocation](./cursorlocation-property-ado.md) como Client para invocar o [serviço de cursor da Microsoft para OLE DB](../../guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md), que oferece suporte a atualizações em lotes.  
  
-   Defina o banco de dados padrão para a conexão com a propriedade [DefaultDatabase](./defaultdatabase-property.md) .  
  
-   Defina o nível de isolamento para as transações abertas na conexão com a propriedade [IsolationLevel](./isolationlevel-property.md) .  
  
-   Especifique um provedor de OLE DB com a propriedade do [provedor](./provider-property-ado.md) .  
  
-   Estabelecer, e posteriormente, interromper, a conexão física com a fonte de dados com os métodos [Open](./open-method-ado-connection.md) e [Close](./close-method-ado.md) .  
  
-   Execute um comando na conexão com o método [Execute](./execute-method-ado-connection.md) e configure a execução com a propriedade [CommandTimeout](./commandtimeout-property-ado.md) .  
  
    > [!NOTE]
    >  Para executar uma consulta sem usar um objeto Command, passe uma cadeia de caracteres de consulta para o método **Execute** de um objeto **Connection** . No entanto, um objeto de [comando](./command-object-ado.md) é necessário quando você deseja manter o texto do comando e executá-lo novamente, ou usar parâmetros de consulta.  
  
-   Gerencie transações na conexão aberta, incluindo transações aninhadas, se o provedor oferecer suporte a elas, com os métodos [BeginTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md), [CommitTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md)e [RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) e a propriedade [Attributes](./attributes-property-ado.md) .  
  
-   Examine os erros retornados da fonte de dados com a coleção de [erros](./errors-collection-ado.md) .  
  
-   Leia a versão da implementação do ADO usada com a propriedade [version](./version-property-ado.md) .  
  
-   Obtenha informações de esquema sobre seu banco de dados com o método [OpenSchema](./openschema-method.md) .  
  
 Você pode criar objetos de **conexão** independentemente de qualquer outro objeto definido anteriormente.  
  
 Você pode executar comandos nomeados ou procedimentos armazenados como se fossem métodos nativos em um objeto de **conexão** , como mostrado na próxima seção. Quando um comando nomeado tem o mesmo nome que um procedimento armazenado, invocar a "chamada de método nativo" em um objeto de **conexão** sempre executa o comando nomeado em vez do procedimento Store.  
  
> [!NOTE]
>  Não use esse recurso (chamando um comando nomeado ou um procedimento armazenado como se fosse um método nativo no objeto de **conexão** ) em um aplicativo do Microsoft® .NET Framework, pois a implementação subjacente do recurso está em conflito com a maneira como o .NET Framework interopera com com.  
  
## <a name="execute-a-command-as-a-native-method-of-a-connection-object"></a>Executar um comando como um método nativo de um objeto de conexão  
 Para executar um comando, dê um nome ao comando usando a propriedade [nome](./name-property-ado.md) do objeto de **comando** . Defina a propriedade **ActiveConnection** do objeto de **comando** para a conexão. Em seguida, emita uma instrução em que o nome do comando seja usado como se fosse um método no objeto de **conexão** , seguido por qualquer parâmetro e um objeto **Recordset** se qualquer linha for retornada. Defina as propriedades do **conjunto de registros** para personalizar o **conjunto de registros**resultante. Por exemplo:  
  
```  
Dim cnn As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
...  
cnn.Open "..."  
cmd.Name = "yourCommandName"  
cmd.ActiveConnection = cnn  
...  
'Your command name, any parameters, and an optional Recordset.  
cnn. "parameter", rst  
```  
  
## <a name="execute-a-stored-procedure-as-a-native-method-of-a-connection-object"></a>Executar um procedimento armazenado como um método nativo de um objeto de conexão  
 Para executar um procedimento armazenado, emita uma instrução em que o nome do procedimento armazenado é usado como se fosse um método no objeto de **conexão** , seguido por qualquer parâmetro. O ADO fará uma "melhor adivinhação" dos tipos de parâmetro. Por exemplo:  
  
```  
Dim cnn As New ADODB.Connection  
...  
'Your stored procedure name and any parameters.  
cnn. "parameter"  
```  
  
 O objeto de **conexão** é seguro para scripts.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto Connection](./connection-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Command (ADO)](./command-object-ado.md)   
 [Coleta de erros (ADO)](./errors-collection-ado.md)   
 [Coleção Properties (ADO)](./properties-collection-ado.md)   
 [Objeto Recordset (ADO)](./recordset-object-ado.md)   
 [Apêndice A: Provedores](../../guide/appendixes/appendix-a-providers.md)