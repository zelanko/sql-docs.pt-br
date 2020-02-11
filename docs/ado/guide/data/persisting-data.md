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
ms.openlocfilehash: 63323fd8ed18f57a68633dce0525d1d37e4978ae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924703"
---
# <a name="persisting-data"></a>Persistência de dados
A computação portátil (por exemplo, usando laptops) gerou a necessidade de aplicativos que podem ser executados em um estado conectado e desconectado. O ADO adicionou suporte para isso fornecendo ao desenvolvedor a capacidade de salvar um **conjunto de registros** de cursor do cliente em disco e recarregá-lo mais tarde.  
  
 Há vários cenários em que você pode usar esse tipo de recurso, incluindo o seguinte:  
  
-   **Viajando:** Ao colocar o aplicativo em trânsito, é vital fornecer a capacidade de fazer alterações e adicionar novos registros que podem ser reconectados posteriormente ao banco de dados e confirmados.  
  
-   **Pesquisas atualizadas com pouca frequência:** Geralmente, em um aplicativo, as tabelas são usadas como pesquisas – por exemplo, tabelas de imposto de estado. Elas são atualizadas com pouca frequência e são somente leitura. Em vez de reler esses dados do servidor cada vez que o aplicativo é iniciado, o aplicativo pode simplesmente carregar os dados de um **conjunto de registros**persistentes localmente.  
  
 No ADO, para salvar e carregar **conjuntos de registros**, use os métodos **Recordset. Save** e **Recordset. Open (,,,, ADCMDFILE)** no objeto **Recordset** ADO.  
  
 Você pode usar o método **Save do conjunto de registros** para manter o conjunto de **registros** ADO em um arquivo em um disco. (Você também pode salvar um **conjunto de registros** em um objeto de **fluxo** ADO. Os objetos **Stream** são discutidos posteriormente no guia.) Posteriormente, você pode usar o método **Open** para reabrir o **conjunto de registros** quando estiver pronto para usá-lo. Por padrão, o ADO salva o **conjunto de registros** no formato proprietário do Microsoft Advanced data TABLEGRAM (ADTG). Esse formato binário é especificado usando o valor de **PersistFormatEnum adPersistADTG** . Como alternativa, você pode optar por salvar o **conjunto de registros** como XML em vez disso usando **adPersistXML**. Para obter mais informações sobre como salvar conjuntos de registros como XML, consulte [persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).  
  
 A sintaxe do método **Save** é a seguinte:  
  
```  
  
recordset.  
Save  
Destination, PersistFormat  
  
```  
  
 Na primeira vez que você salvar o **conjunto de registros**, é opcional especificar *destino*. Se você omitir o *destino*, um novo arquivo será criado com um nome definido como o valor da propriedade [Source](../../../ado/reference/ado-api/source-property-ado-recordset.md) do **conjunto de registros**.  
  
 Omita o *destino* quando você chamar o **salvamento** posteriormente após o primeiro salvamento ou se ocorrer um erro de tempo de execução. Se, posteriormente, você chamar **Save** com um novo *destino*, o **conjunto de registros** será salvo no novo destino. No entanto, o novo destino e o destino original serão abertos.  
  
 **Salvar** não fecha o **conjunto de registros** ou *destino*, para que você possa continuar a trabalhar com o **conjunto de registros** e salvar suas alterações mais recentes. O *destino* permanece aberto até que o **conjunto de registros** seja fechado, durante o qual outros aplicativos podem ler, mas não gravar no *destino*.  
  
 Por motivos de segurança, o método **Save** permite apenas o uso de configurações de segurança baixas e personalizadas de um script executado pelo Microsoft Internet Explorer.  
  
 Se o método **Save** for chamado enquanto uma operação de busca, execução ou atualização do **conjunto de registros** assíncrono estiver em andamento, **salve** aguarda até que a operação assíncrona seja concluída.  
  
 Os registros são salvos a partir da primeira linha do **conjunto de registros**. Quando o método **Save** é concluído, a posição da linha atual é movida para a primeira linha do **conjunto de registros**.  
  
 Para obter melhores resultados, defina a propriedade [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) como **adUseClient** com **salvar**. Se seu provedor não oferecer suporte a toda a funcionalidade necessária para salvar objetos do **conjunto de registros** , o serviço de cursor fornecerá essa funcionalidade.  
  
 Quando um **conjunto de registros** é persistido com a propriedade **CursorLocation** definida como **adUseServer**, o recurso de atualização para o **conjunto de registros** é limitado. Normalmente, apenas atualizações de tabela única, inserções e exclusões são permitidas (dependentes da funcionalidade do provedor). O método [Ressync](../../../ado/reference/ado-api/resync-method.md) também não está disponível nessa configuração.  
  
 Como o parâmetro de *destino* pode aceitar qualquer objeto que dê suporte à interface OLE DB **IStream** , você pode salvar um **conjunto de registros** diretamente no objeto de **resposta** ASP.  
  
 No exemplo a seguir, os métodos **Save** e **Open** são usados para persistir um **conjunto de registros** e, posteriormente, reabri-lo:  
  
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
 Esta seção contém os seguintes tópicos:  
  
-   [Mais informações sobre a persistência do conjunto de registros](../../../ado/guide/data/more-about-recordset-persistence.md)  
  
-   [Persistência de conjunto de registros filtrados e hierárquicos](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)  
  
-   [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
