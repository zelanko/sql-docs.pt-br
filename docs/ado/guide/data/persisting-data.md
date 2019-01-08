---
title: Persistência de dados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: 21c162ca-2845-4dd8-a49d-e715aba8c461
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b89f05822ee23f5ad62c627b8bc6d67ebe401a2e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527628"
---
# <a name="persisting-data"></a>Persistência de dados
Computação portátil (por exemplo, usando laptops) gerou a necessidade de aplicativos que podem ser executados em um estado conectado e desconectado. ADO adicionou suporte para isso, dando a desenvolvedores a capacidade de salvar um cursor do cliente **Recordset** em disco e recarregá-lo mais tarde.  
  
 Há vários cenários em que você pode usar esse tipo de recurso, incluindo o seguinte:  
  
-   **Uma viagem:** Ao fazer o aplicativo em trânsito, é vital para fornecer a capacidade de fazer alterações e adicionar novos registros que podem ser reconectados ao banco de dados mais tarde e confirmados.  
  
-   **Pesquisas não costumam ser atualizadas:** Muitas vezes em um aplicativo, tabelas são usadas como pesquisas-por exemplo, tabelas de impostos de estado. Eles são atualizados com pouca frequência e são somente leitura. Em vez de reler esses dados do servidor de cada vez que o aplicativo é iniciado, o aplicativo pode simplesmente carregar os dados de um localmente persistente **conjunto de registros**.  
  
 No ADO, salvar e carregar **conjuntos de registros**, use o **Recordset.Save** e **Recordset.Open(,,,adCmdFile)** métodos em ADO **Recordset**objeto.  
  
 Você pode usar o **Salvar conjunto de registros** método para manter seu ADO **conjunto de registros** em um arquivo em um disco. (Você também pode salvar uma **conjunto de registros** ao ADO **Stream** objeto. **Stream** objetos são discutidos posteriormente no guia.) Posteriormente, você pode usar o **aberto** método para reabrir a **Recordset** quando você estiver pronto para usá-lo. Por padrão, o ADO salva o **Recordset** em um formato proprietário TableGram de dados avançado da Microsoft (ADTG). Esse formato binário é especificado usando o **adPersistADTG PersistFormatEnum** valor. Como alternativa, você pode optar por salvar seu **conjunto de registros** horizontalmente conforme a XML em vez de usar **adPersistXML**. Para obter mais informações sobre como salvar os conjuntos de registros como XML, consulte [manter registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).  
  
 A sintaxe do **salvar** é como segue:  
  
```  
  
recordset.  
Save  
Destination, PersistFormat  
  
```  
  
 Na primeira vez que você salvar a **conjunto de registros**, é opcional para especificar *destino*. Se você omitir *destino*, um novo arquivo será criado com um nome definido como o valor da [fonte](../../../ado/reference/ado-api/source-property-ado-recordset.md) propriedade do **conjunto de registros**.  
  
 Omitir *destino* ao chamar subsequentemente **salvar** depois que o primeiro salvar ou um erro de tempo de execução ocorrerá. Se você chamar subsequentemente **salve** com uma nova *destino*, o **Recordset** é salvo para o novo destino. No entanto, o novo destino e o destino original serão ser abertos.  
  
 **Salve** não fecha o **conjunto de registros** ou *destino*, portanto, você pode continuar a trabalhar com o **Recordset** e salve as alterações mais recentes. *Destino* permanece aberta até que o **conjunto de registros** for fechada, período durante o qual outros aplicativos podem ler, mas não gravar *destino*.  
  
 Por motivos de segurança, o **salvar** método permite apenas o uso de configurações de segurança baixa e personalizada de um script executado pelo Microsoft Internet Explorer.  
  
 Se o **salve** método é chamado durante a assíncrona **conjunto de registros** buscar, executar ou atualizar operação está em andamento, **salvar** aguarda até que a operação assíncrona é Conclua.  
  
 Registros são salvos, começando com a primeira linha do **conjunto de registros**. Quando o **salve** método for concluído, a posição da linha atual é movida para a primeira linha das **conjunto de registros**.  
  
 Para obter melhores resultados, defina as [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade **adUseClient** com **salvar**. Se seu provedor não oferece suporte a todas as funcionalidades necessárias para salvar **Recordset** objetos, o serviço de Cursor fornecerá essa funcionalidade.  
  
 Quando um **conjunto de registros** é persistida com o **CursorLocation** propriedade definida como **adUseServer**, o recurso de atualização para o **Recordset**é limitado. Normalmente, somente tabela única de atualizações, inserções e exclusões são permitidas (dependentes da funcionalidade de provedor). O [ressincronizar](../../../ado/reference/ado-api/resync-method.md) método também está disponível nessa configuração.  
  
 Porque o *destino* parâmetro pode aceitar qualquer objeto que dá suporte ao OLE DB **IStream** interface, você pode salvar uma **conjunto de registros** diretamente para o ASP  **Resposta** objeto.  
  
 No exemplo a seguir, o **salve** e **abra** métodos são usados para manter uma **conjunto de registros** e abri-la posteriormente:  
  
```  
'BeginPersist  
   conn.ConnectionString = _  
   "Provider=SQLOLEDB;Data Source=MySQLServer;" _  
      & "Integrated Security=SSPI;Initial Catalog=pubs"  
   conn.Open  
  
   conn.Execute "create table testtable (dbkey int " & _  
      "primary key, field1 char(10))"  
   conn.Execute "insert into testtable values (1, 'string1')"  
  
   Set rst.ActiveConnection = conn  
   rst.CursorLocation = adUseClient  
  
   rst.Open "select * from testtable", conn, adOpenStatic, _  
      adLockBatchOptimistic  
  
   'Change the row on the client  
   rst!field1 = "NewValue"  
  
   'Save to a file--the .dat extension is an example; choose  
   'your own extension. The changes will be saved in the file  
   'as well as the original data.  
   MyFile = Dir("c:\temp\temptbl.dat")  
   If MyFile <> "" Then  
       Kill "c:\temp\temptbl.dat"  
   End If  
  
   rst.Save "c:\temp\temptbl.dat", adPersistADTG  
   Set rst = Nothing  
  
   'Now reload the data from the file  
   Set rst = New ADODB.Recordset  
   rst.Open "c:\temp\temptbl.dat", , adOpenStatic, _  
      adLockBatchOptimistic, adCmdFile  
  
   Debug.Print "After Loading the file from disk"  
   Debug.Print "   Current Edited Value: " & rst!field1.Value  
   Debug.Print "   Value Before Editing: " & rst!field1.OriginalValue  
  
   'Note that you can reconnect to a connection and  
   'submit the changes to the data source  
   Set rst.ActiveConnection = conn  
   rst.UpdateBatch  
'EndPersist  
```  
  
## <a name="remarks"></a>Comentários  
 Esta seção contém os tópicos a seguir.  
  
-   [Mais informações sobre a persistência do conjunto de registros](../../../ado/guide/data/more-about-recordset-persistence.md)  
  
-   [Persistência de conjunto de registros filtrados e hierárquicos](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)  
  
-   [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
