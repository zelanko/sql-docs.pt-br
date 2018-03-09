---
title: Dados persistentes | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: 21c162ca-2845-4dd8-a49d-e715aba8c461
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 533801c5f6717ec32a821a79acadce3f953c8d71
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="persisting-data"></a>Dados persistentes
Computação portátil (por exemplo, usando laptops) gerou a necessidade de aplicativos que podem ser executados em um estado conectado ou desconectado. ADO adicionou suporte para isso fornecendo a capacidade de salvar um cursor do cliente para o desenvolvedor **registros** em disco e recarregá-lo mais tarde.  
  
 Há várias situações em que você pode usar esse tipo de recurso, incluindo o seguinte:  
  
-   **Viajando:** quando o aplicativo em trânsito, é essencial para fornecer a capacidade de fazer alterações e adicionar novos registros que podem ser reconectados posteriormente ao banco de dados e confirmados.  
  
-   **Raramente atualizados pesquisas:** geralmente em um aplicativo, as tabelas são usadas como pesquisas — por exemplo, tabelas de imposto de estado. Elas raramente são atualizadas e são somente leitura. Em vez de reler esses dados do servidor de cada vez que o aplicativo é iniciado, o aplicativo pode simplesmente carregar os dados de um localmente persistente **registros**.  
  
 No ADO, salvar e carregar **conjuntos de registros**, use o **Recordset.Save** e **Recordset.Open(,,,adCmdFile)** métodos em ADO **registros**objeto.  
  
 Você pode usar o **Salvar conjunto de registros** método para manter o ADO **registros** em um arquivo em um disco. (Você também pode salvar uma **registros** para ADO **fluxo** objeto. **Fluxo** objetos são discutidos posteriormente no guia.) Posteriormente, você pode usar o **abrir** método para reabrir o **registros** quando estiver pronto para usá-lo. Por padrão, o ADO salva o **registros** no formato proprietário TableGram de dados avançado (ADTG) da Microsoft. Esse formato binário é especificado usando o **adPersistADTG PersistFormatEnum** valor. Como alternativa, você pode optar por salvar seu **registros** fora como XML em vez de usar **adPersistXML**. Para obter mais informações sobre como salvar o conjunto de registros como XML, consulte [manter registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).  
  
 A sintaxe do **salvar** método é o seguinte:  
  
```  
  
recordset.  
Save  
Destination, PersistFormat  
  
```  
  
 Na primeira vez que você salvar o **registros**, é opcional especificar *destino*. Se você omitir *destino*, um novo arquivo será criado com um nome definido como o valor da [fonte](../../../ado/reference/ado-api/source-property-ado-recordset.md) propriedade o **conjunto de registros**.  
  
 Omitir *destino* quando você chamar subsequentemente **salvar** após a primeira gravação ou um erro de tempo de execução ocorrerá. Se você chamar subsequentemente **salvar** com um novo *destino*, o **registros** é salvo para o novo destino. No entanto, o novo destino e o destino original ambos será abertas.  
  
 **Salvar** não fecha o **registros** ou *destino*, portanto, você pode continuar a trabalhar com o **registros** e salve as alterações mais recentes. *Destino* permanece aberto até que o **registros** for fechada, durante o tempo de quais outros aplicativos podem ler, mas não gravar *destino*.  
  
 Por razões de segurança, o **salvar** método permite apenas o uso de configurações de segurança personalizados e baixa de um script executado pelo Microsoft Internet Explorer.  
  
 Se o **salvar** método é chamado durante assíncrona **registros** buscar, executar ou atualizar a operação está em andamento, **salvar** aguarda até que a operação assíncrona é Conclua.  
  
 Registros são salvos, começando com a primeira linha do **registros**. Quando o **salvar** método é concluído, a posição da linha atual é movida para a primeira linha do **registros**.  
  
 Para obter melhores resultados, defina o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade **adUseClient** com **salvar**. Se o provedor não dá suporte toda a funcionalidade necessária para salvar **registros** objetos, o serviço de Cursor fornecem essa funcionalidade.  
  
 Quando um **Recordset** são mantidas com o **CursorLocation** propriedade definida como **adUseServer**, a capacidade de atualização para o **Recordset**é limitado. Normalmente, somente tabela única atualizações, inserções e exclusões são permitidas (dependentes da funcionalidade de provedor). O [Resync](../../../ado/reference/ado-api/resync-method.md) método também está disponível nessa configuração.  
  
 Porque o *destino* parâmetro pode aceitar qualquer objeto que dá suporte a OLE DB **IStream** interface, você pode salvar uma **registros** diretamente para o ASP  **Resposta** objeto.  
  
 No exemplo a seguir, o **salvar** e **abrir** métodos são usados para manter um **registros** e abri-lo posteriormente:  
  
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
  
## <a name="remarks"></a>Remarks  
 Esta seção contém os tópicos a seguir.  
  
-   [Mais informações sobre a persistência do conjunto de registros](../../../ado/guide/data/more-about-recordset-persistence.md)  
  
-   [Persistência de conjunto de registros filtrados e hierárquicos](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)  
  
-   [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
