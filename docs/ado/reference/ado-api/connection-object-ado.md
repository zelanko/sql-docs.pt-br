---
title: O objeto de Conexão (ADO) | Microsoft Docs
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
apitype: COM
f1_keywords:
- Connection
helpviewer_keywords:
- Connection object [ADO]
ms.assetid: ef6b1824-5b12-43db-89d7-8f3d13896d4d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba405d7993c5f9c327d5789cfa3bf3c9ccfba2b7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="connection-object-ado"></a>Objeto de Conexão (ADO)
Representa uma conexão aberta com uma fonte de dados.  
  
## <a name="remarks"></a>Remarks  
 Um **Conexão** objeto representa uma sessão exclusiva com uma fonte de dados. Em um sistema de banco de dados cliente/servidor, é equivalente a uma conexão de rede reais para o servidor. Dependendo da funcionalidade com suporte do provedor, algumas coleções, métodos ou propriedades de um **Conexão** objeto pode não estar disponível.  
  
 Com as coleções, métodos e propriedades de um **Conexão** do objeto, você pode fazer o seguinte:  
  
-   Configurar a conexão antes de abri-lo com o [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md), [ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md), e [modo](../../../ado/reference/ado-api/mode-property-ado.md) propriedades. **ConnectionString** é a propriedade padrão do **Conexão** objeto.  
  
-   Definir o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade ao cliente para chamar o [do serviço Microsoft Cursor do OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md), que oferece suporte a atualizações do lote.  
  
-   Definir o banco de dados padrão para a conexão com o [DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md) propriedade.  
  
-   Definir o nível de isolamento para as transações aberto na conexão com o [IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md) propriedade.  
  
-   Especifique um provedor OLE DB com o [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade.  
  
-   Estabelecer e dividir posteriormente, a conexão física à fonte de dados com o [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) e [fechar](../../../ado/reference/ado-api/close-method-ado.md) métodos.  
  
-   Executar um comando em conexão com o [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) método e configurar a execução com o [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md) propriedade.  
  
    > [!NOTE]
    >  Para executar uma consulta sem usar um objeto de comando, passar uma cadeia de caracteres de consulta para o **Execute** método de um **Conexão** objeto. No entanto, um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto é necessário quando você deseja manter o texto de comando e execute novamente ou use parâmetros de consulta.  
  
-   Gerenciar transações em que a conexão aberta, inclusive transações aninhadas, se o provedor oferece suporte a eles, com o [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md), [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md), e [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) métodos e [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propriedade.  
  
-   Examine os erros retornados da fonte de dados com o [erros](../../../ado/reference/ado-api/errors-collection-ado.md) coleção.  
  
-   Ler a versão da implementação do ADO usada com o [versão](../../../ado/reference/ado-api/version-property-ado.md) propriedade.  
  
-   Obter informações de esquema sobre seu banco de dados com o [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) método.  
  
 Você pode criar **Conexão** objetos independentemente de qualquer outro objeto definido anteriormente.  
  
 Você pode executar comandos nomeados ou procedimentos armazenados, como se fossem métodos nativos em uma **Conexão** do objeto, como mostrado na próxima seção. Quando um comando nomeado tem o mesmo nome de um procedimento armazenado, invoque "chamada do método nativo" em um **Conexão** objeto sempre execute o comando nomeado em vez do procedimento armazenado.  
  
> [!NOTE]
>  Não use esse recurso (chamando um procedimento armazenado ou um comando nomeado como se fosse um método nativo no **Conexão** objeto) em um aplicativo do Microsoft® .NET Framework, porque a implementação subjacente dos conflitos de recurso com a maneira como o .NET Framework interopera com COM.  
  
## <a name="execute-a-command-as-a-native-method-of-a-connection-object"></a>Executar um comando como um método nativo de um objeto de Conexão  
 Para executar um comando, nomeie o comando usando o **comando** objeto [nome](../../../ado/reference/ado-api/name-property-ado.md) propriedade. Definir o **ActiveConnection** propriedade o **comando** objeto para a conexão. Em seguida, emita uma instrução em que o nome do comando é usado como se fosse um método no **Conexão** objeto, seguido por quaisquer parâmetros e um **registros** se todas as linhas são retornadas do objeto. Definir o **registros** propriedades para personalizar resultante **registros**. Por exemplo:  
  
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
  
## <a name="execute-a-stored-procedure-as-a-native-method-of-a-connection-object"></a>Executar um procedimento armazenado como um método nativo de um objeto de Conexão  
 Para executar um procedimento armazenado, emita uma instrução em que o nome do procedimento armazenado é usado como se fosse um método no **Conexão** objeto, seguido por todos os parâmetros. ADO tornará "melhor estimativa" dos tipos de parâmetro. Por exemplo:  
  
```  
Dim cnn As New ADODB.Connection  
...  
'Your stored procedure name and any parameters.  
cnn. "parameter"  
```  
  
 O **Conexão** objeto é seguro para script.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Eventos, métodos e propriedades do objeto de Conexão](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de comando (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Coleção de erros (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Coleção de propriedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
