---
title: "Método Save | Microsoft Docs"
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
apitype: COM
f1_keywords:
- _Recordset::Save
- _Recordset::raw_Save
helpviewer_keywords:
- Save method [ADO]
ms.assetid: ed3d9678-5c28-4e61-8bb3-7dfb66d99cf5
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ca1aa95841be1331ad1b214b2a8b377622883d3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="save-method"></a>Método Save
Salva o [registros](../../../ado/reference/ado-api/recordset-object-ado.md) em um arquivo ou [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Save Destination, PersistFormat  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Destino*  
 Opcional. Um **Variant** que representa o nome de caminho completo do arquivo onde o **registros** deve ser salvo, ou uma referência a um **fluxo** objeto.  
  
 *PersistFormat*  
 Opcional. Um [PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md) valor que especifica o formato no qual o **registros** deve ser salvo (XML ou ADTG). O valor padrão é **adPersistADTG**.  
  
## <a name="remarks"></a>Remarks  
 O [método Save](../../../ado/reference/ado-api/save-method.md) método só pode ser chamado em um aberto **registros**. Use o [método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) método para restauração posterior a **registros** de *destino*.  
  
 Se o [propriedade filtro](../../../ado/reference/ado-api/filter-property.md) propriedade está em vigor para o **Recordset**, em seguida, somente as linhas acessíveis com o filtro serão salvas. Se o **Recordset** é hierárquico, em seguida, o filho atual **Recordset** e seus filhos são salvos, incluindo o pai **Recordset**. Se o método de gravação de um filho **registros** é chamado, o filho e todos os seus filhos são salvas, mas o pai não é.  
  
 Na primeira vez que você salvar o **registros**, é opcional especificar *destino*. Se você omitir *destino*, um novo arquivo será criado com um nome definido para o valor da propriedade de origem a **registros**.  
  
 Omitir *destino* quando você chamar subsequentemente **salvar** após a primeira gravação ou um erro de tempo de execução ocorrerá. Se você chamar subsequentemente **salvar** com um novo *destino*, o **registros** é salvo para o novo destino. No entanto, o novo destino e o destino original ambos será abertas.  
  
 **Salvar** não fecha o **registros** ou *destino*, portanto, você pode continuar a trabalhar com o **registros** e salve as alterações mais recentes. *Destino* permanece aberto até que o **registros** está fechado.  
  
 Por razões de segurança, o **salvar** método permite apenas o uso de configurações de segurança personalizados e baixa de um script executado pelo Microsoft Internet Explorer.  
  
 Se o **salvar** método é chamado durante assíncrona **registros** buscar, executar ou atualizar a operação está em andamento, em seguida, **salvar** aguarda até que a operação assíncrona foi concluída.  
  
 Registros são salvos, começando com a primeira linha do **registros**. Quando o **salvar** método é concluído, a posição da linha atual é movida para a primeira linha do **registros**.  
  
 Para obter melhores resultados, defina o [CursorLocation Property (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade **adUseClient** com **salvar**. Se o provedor não dá suporte toda a funcionalidade necessária para salvar **registros** objetos, o serviço de Cursor fornecem essa funcionalidade.  
  
 Quando um **Recordset** são mantidas com o **CursorLocation** propriedade definida como **adUseServer**, a capacidade de atualização para o **Recordset**é limitado. Normalmente, somente tabela única atualizações, inserções e exclusões são permitidas (dependente de funcionalidade de provedor). O [método Resync](../../../ado/reference/ado-api/resync-method.md) método também está disponível nessa configuração.  
  
> [!NOTE]
>  Salvando uma **registros** com **campos** do tipo **adVariant**, **adIDispatch**, ou **adIUnknown** é não têm suporte pelo ADO e pode causar resultados imprevisíveis.  
  
 Somente filtros na forma de cadeias de caracteres de critérios (OrderDate, por exemplo, > ' 12/31/1999 ') afeta o conteúdo de um persistente **registros**. Filtros criados com uma matriz de **indicadores** ou usando um valor da [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) não afeta o conteúdo de persistente **registros**. Essas regras se aplicam a **registros**s criados com cursores do lado do cliente ou do servidor.  
  
 Porque o *destino* parâmetro pode aceitar qualquer objeto que ofereça suporte à interface IStream do OLE DB, você pode salvar uma **registros** diretamente para o objeto de resposta do ASP. Para obter mais detalhes, consulte o **cenário de persistência do conjunto de registros de XML**.  
  
 Você também pode salvar uma **registros** em formato XML a uma instância de um objeto DOM MSXML, como é mostrado no seguinte código do Visual Basic:  
  
```  
Dim xDOM As New MSXML.DOMDocument  
Dim rsXML As New ADODB.Recordset  
Dim sSQL As String, sConn As String  
  
sSQL = "SELECT customerid, companyname, contactname FROM customers"  
sConn="Provider=Microsoft.Jet.OLEDB.4.0;Data Source=Northwind.mdb"  
rsXML.Open sSQL, sConn  
rsXML.Save xDOM, adPersistXML   'Save Recordset directly into a DOM tree.  
...  
```  
  
> [!NOTE]
>  Duas limitações se aplicam ao salvar o conjunto de registros hierárquico (formas de dados) em formato XML. Não é possível salvar em XML se o hierárquica **registros** contém as atualizações pendentes, e não é possível salvar um parametrizadas hierárquica **registros**.  
  
 Um **registros** salvo no XML de formato é salvo usando o formato UTF-8. Quando esse arquivo é carregado em um fluxo de ADO, o objeto de fluxo não tentará abrir um **registros** do fluxo, a menos que a propriedade de conjunto de caracteres do fluxo é definida como o valor apropriado para o formato UTF-8.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Salve e abra o exemplo de métodos (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Salve e abra o exemplo de métodos (VC + +)](../../../ado/reference/ado-api/save-and-open-methods-example-vc.md)   
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método Open (fluxo de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)
