---
title: Salvar método | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Recordset::Save
- _Recordset::raw_Save
helpviewer_keywords:
- Save method [ADO]
ms.assetid: ed3d9678-5c28-4e61-8bb3-7dfb66d99cf5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0953b76ff642387679c907e6f0b3364cbac898df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711391"
---
# <a name="save-method"></a>Método Save
Salva o [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) em um arquivo ou [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Save Destination, PersistFormat  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Destino*  
 Opcional. Um **Variant** que representa o nome de caminho completo do arquivo no qual o **conjunto de registros** deve ser salvo, ou uma referência a um **Stream** objeto.  
  
 *PersistFormat*  
 Opcional. Um [PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md) valor que especifica o formato no qual o **Recordset** deve ser salvo (ADTG ou XML). O valor padrão é **adPersistADTG**.  
  
## <a name="remarks"></a>Comentários  
 O [método Save](../../../ado/reference/ado-api/save-method.md) método só pode ser chamado em um aberto **conjunto de registros**. Use o [método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) método para restauração posterior a **conjunto de registros** da *destino*.  
  
 Se o [propriedade Filter](../../../ado/reference/ado-api/filter-property.md) propriedade está em vigor para o **conjunto de registros**, em seguida, somente as linhas acessíveis sob o filtro são salvos. Se o **conjunto de registros** é hierárquico, em seguida, o filho atual **conjunto de registros** e seus filhos são salvas, incluindo o pai **conjunto de registros**. Se o método Save de um filho **Recordset** é chamado, o filho e todos os seus filhos são salvas, mas o pai não é.  
  
 Na primeira vez que você salvar a **conjunto de registros**, é opcional para especificar *destino*. Se você omitir *destino*, um novo arquivo será criado com um nome definido como o valor da propriedade do código-fonte a **conjunto de registros**.  
  
 Omitir *destino* ao chamar subsequentemente **salvar** depois que o primeiro salvar ou um erro de tempo de execução ocorrerá. Se você chamar subsequentemente **salve** com uma nova *destino*, o **Recordset** é salvo para o novo destino. No entanto, o novo destino e o destino original serão ser abertos.  
  
 **Salve** não fecha o **conjunto de registros** ou *destino*, portanto, você pode continuar a trabalhar com o **Recordset** e salve as alterações mais recentes. *Destino* permanece aberta até que o **Recordset** está fechado.  
  
 Por motivos de segurança, o **salvar** método permite apenas o uso de configurações de segurança baixa e personalizada de um script executado pelo Microsoft Internet Explorer.  
  
 Se o **salve** método é chamado durante a assíncrona **conjunto de registros** buscar, executar ou atualizar a operação está em andamento, em seguida, **salvar** aguarda até que a operação assíncrona foi concluída.  
  
 Registros são salvos, começando com a primeira linha do **conjunto de registros**. Quando o **salve** método for concluído, a posição da linha atual é movida para a primeira linha das **conjunto de registros**.  
  
 Para obter melhores resultados, defina as [propriedade CursorLocation (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade **adUseClient** com **salvar**. Se seu provedor não oferece suporte a todas as funcionalidades necessárias para salvar **Recordset** objetos, o serviço de Cursor fornecerá essa funcionalidade.  
  
 Quando um **conjunto de registros** é persistida com o **CursorLocation** propriedade definida como **adUseServer**, o recurso de atualização para o **Recordset**é limitado. Normalmente, somente tabela única de atualizações, inserções e exclusões são permitidas (dependente de funcionalidade de provedor). O [método Resync](../../../ado/reference/ado-api/resync-method.md) método também está disponível nessa configuração.  
  
> [!NOTE]
>  Salvando uma **conjunto de registros** com **campos** do tipo **adVariant**, **adIDispatch**, ou **adIUnknown** é não tem suporte pelo ADO e pode causar resultados imprevisíveis.  
  
 Filtra somente na forma de cadeias de caracteres de critérios (OrderDate, por exemplo, > ' 12/31/1999 ') afeta o conteúdo de um persistente **conjunto de registros**. Filtros criados com uma matriz de **indicadores** ou usando um valor da [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) não afetará o conteúdo de persistido **conjunto de registros**. Essas regras se aplicam a **Recordset**s criados com cursores do lado do cliente ou servidor.  
  
 Porque o *destino* parâmetro pode aceitar qualquer objeto compatível com a interface IStream do OLE DB, você pode salvar uma **Recordset** diretamente para o objeto de resposta do ASP. Para obter mais detalhes, consulte o **cenário de persistência de conjunto de registros XML**.  
  
 Você também pode salvar uma **Recordset** em formato XML a uma instância de um objeto DOM MSXML, conforme é mostrado no código do Visual Basic a seguir:  
  
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
>  Duas limitações se aplicam ao salvar os conjuntos de registros hierárquicos (formas de dados) em formato XML. Não é possível salvar em XML se o hierárquica **conjunto de registros** contém as atualizações pendentes, e não é possível salvar um parametrizada hierárquica **conjunto de registros**.  
  
 Um **Recordset** salvo no XML de formato é salvo usando o formato UTF-8. Quando esse arquivo é carregado em um Stream de ADO, o objeto Stream não tentará abrir um **Recordset** do fluxo, a menos que a propriedade de conjunto de caracteres do fluxo é definida como o valor apropriado para o formato UTF-8.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Salvar e abrir um exemplo dos métodos (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Salvar e abrir um exemplo dos métodos (VC + +)](../../../ado/reference/ado-api/save-and-open-methods-example-vc.md)   
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método Open (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)
