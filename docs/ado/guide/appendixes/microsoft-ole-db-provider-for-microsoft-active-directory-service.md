---
title: Provedor do Microsoft OLE DB para Microsoft Active Directory Service | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADSI provider [ADO]
- Active Directory Service Interfaces provider [ADO]
- providers [ADO], OLE DB provider for Active Directory service
- OLE DB provider for Active Directory service [ADO]
ms.assetid: f9e81452-5675-4cfc-9949-cfbd2fe57534
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e204a4f6f7f395ca93198bc560f4a216d5a70673
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926673"
---
# <a name="microsoft-ole-db-provider-for-microsoft-active-directory-service"></a>Provedor do Microsoft OLE DB para Microsoft Active Directory Service
O provedor de interfaces do serviço de Active Directory (ADSI) permite que o ADO se conecte a serviços de diretório heterogêneos por meio de ADSI. Isso fornece aos aplicativos ADO acesso somente leitura aos serviços de diretório do Microsoft Windows NT 4,0 e do Microsoft Windows 2000, além de qualquer serviço de diretório compatível com LDAP e serviços de Diretório Novell. A própria ADSI se baseia em um modelo de provedor, de modo que, se houver um novo provedor que dê acesso a outro diretório, o aplicativo ADO poderá acessá-lo diretamente. O provedor ADSI está livre de threads e Unicode habilitado.  
  
## <a name="connection-string-parameters"></a>Parâmetros de cadeia de conexão  
 Para se conectar a esse provedor, defina o argumento do **provedor** da propriedade [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) para o seguinte:  
  
```vb
ADSDSOObject  
```  
  
 A leitura da propriedade [Provider](../../../ado/reference/ado-api/provider-property-ado.md) retornará essa cadeia de caracteres também.  
  
## <a name="typical-connection-string"></a>Cadeia de conexão típica  
 Uma cadeia de conexão típica para esse provedor é a seguinte:  
  
```vb
"Provider=ADSDSOObject;User ID=MyUserID;Password=MyPassword;"  
```  
  
 A cadeia de caracteres consiste nas seguintes palavras-chave.  
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|**Provedor**|Especifica o provedor de OLE DB para o serviço Active Directory.|  
|**ID de usuário**|Especifica um nome de usuário. Se essa palavra-chave for omitida, o logon atual será usado.|  
|**Senha**|Especifica a senha do usuário. Se essa palavra-chave for omitida. Em seguida, o logon atual é usado.|  
  
> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que dá suporte à autenticação do Windows, especifique **Trusted_Connection = Sim** ou **segurança integrada = SSPI** , em vez de ID de usuário e informações de senha na cadeia de conexão.  
  
## <a name="command-text"></a>Texto do comando  
 Uma cadeia de caracteres de texto de comando de quatro partes é reconhecida pelo provedor na seguinte sintaxe:  
  
```vb
"Root; Filter; Attributes[; Scope]"  
```  
  
|Valor|Descrição|  
|-----------|-----------------|  
|*Básica*|Indica o objeto **ADsPath** do qual iniciar a pesquisa (ou seja, a raiz da pesquisa).|  
|*Filter*|Indica o filtro de pesquisa no formato RFC 1960.|  
|*Atributos*|Indica uma lista delimitada por vírgulas de atributos a serem retornados.|  
|*Escopo*|Opcional. Uma **cadeia de caracteres** que especifica o escopo da pesquisa. Pode ser um dos seguintes:<br /><br /> -Base-pesquise somente o objeto base (raiz da pesquisa).<br />-Onelevet-Pesquisar apenas um nível.<br />-Subtree – Pesquise toda a subárvore.|  
  
 Por exemplo:  
  
```vb
"<LDAP://DC=ArcadiaBay,DC=COM>;(objectClass=*);sn, givenName; subtree"  
```  
  
 O provedor também dá suporte ao SQL SELECT para texto de comando. Por exemplo:  
  
```vb
"SELECT title, telephoneNumber From 'LDAP://DC=Microsoft, DC=COM' WHERE   
objectClass='user' AND objectCategory='Person'"  
```  
  
## <a name="remarks"></a>Comentários  
 O provedor não aceita chamadas de procedimento armazenado ou nomes de tabela simples (por exemplo, a propriedade [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) será sempre **adCmdText**). Consulte a documentação de interfaces de serviço Active Directory para obter uma descrição mais completa dos elementos de texto do comando.  
  
## <a name="recordset-behavior"></a>Comportamento do conjunto de registros  
 As tabelas a seguir listam os recursos disponíveis em um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) aberto usando esse provedor. Somente o tipo de cursor estático (**adOpenStatic**) está disponível.  
  
 Para obter mais informações sobre o comportamento do **conjunto de registros** para a configuração do provedor, execute o método de [suporte](../../../ado/reference/ado-api/supports-method.md) e enumere a coleção [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) do **conjunto de registros** para determinar se as propriedades dinâmicas específicas do provedor estão presentes.  
  
 **Disponibilidade das propriedades padrão do conjunto de registros ADO:**  
  
|Propriedade|Disponibilidade|  
|--------------|------------------|  
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|leitura/gravação|  
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|leitura/gravação|  
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|somente leitura|  
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|somente leitura|  
|[Indicador](../../../ado/reference/ado-api/bookmark-property-ado.md)|leitura/gravação|  
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|leitura/gravação|  
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|sempre **adUseServer**|  
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|sempre **adOpenStatic**|  
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|sempre **adEditNone**|  
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|somente leitura|  
|[Filter](../../../ado/reference/ado-api/filter-property.md)|leitura/gravação|  
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|leitura/gravação|  
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|não disponível|  
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|leitura/gravação|  
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|somente leitura|  
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|leitura/gravação|  
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|somente leitura|  
|[Fonte](../../../ado/reference/ado-api/source-property-ado-recordset.md)|leitura/gravação|  
|[State](../../../ado/reference/ado-api/state-property-ado.md)|somente leitura|  
|[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)|somente leitura|  
  
 **Disponibilidade de métodos Recordset padrão do ADO:**  
  
|Método|Disponível?|  
|------------|----------------|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|Não|  
|[Cancelar](../../../ado/reference/ado-api/cancel-method-ado.md)|Não|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|Não|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|Não|  
|[Clonar](../../../ado/reference/ado-api/clone-method-ado.md)|Sim|  
|[Fechar](../../../ado/reference/ado-api/close-method-ado.md)|Sim|  
|[Delete (excluir)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|Não|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Sim|  
|[Mover](../../../ado/reference/ado-api/move-method-ado.md)|Sim|  
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sim|  
|[Velas](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sim|  
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sim|  
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sim|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Sim|  
|[Abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Sim|  
|[Repita](../../../ado/reference/ado-api/requery-method.md)|Sim|  
|[Sincronizar novamente](../../../ado/reference/ado-api/resync-method.md)|Sim|  
|[Suporta](../../../ado/reference/ado-api/supports-method.md)|Sim|  
|[Atualização](../../../ado/reference/ado-api/update-method.md)|Não|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|Não|  
  
 Para obter mais informações sobre a ADSI e as especificidades do provedor, consulte a documentação de interfaces de serviço Active Directory ou visite a página da Web ADSI.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade CommandType (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)   
 [Propriedade ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Propriedade Provider (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)
