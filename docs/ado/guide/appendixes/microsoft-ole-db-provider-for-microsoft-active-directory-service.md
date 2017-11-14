---
title: Provedor Microsoft OLE DB para o Microsoft Active Directory Service | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADSI provider [ADO]
- Active Directory Service Interfaces provider [ADO]
- providers [ADO], OLE DB provider for Active Directory service
- OLE DB provider for Active Directory service [ADO]
ms.assetid: f9e81452-5675-4cfc-9949-cfbd2fe57534
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cc6946f6944cf37f85759847f2c8db852d120461
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-ole-db-provider-for-microsoft-active-directory-service"></a>Provedor Microsoft OLE DB para o serviço do Microsoft Active Directory
O provedor do Active Directory Service Interfaces (ADSI) permite que o ADO conectar-se aos serviços de diretório heterogêneos por meio de ADSI. Isso fornece aplicativos ADO acesso somente leitura para os serviços de diretório do Microsoft Windows NT 4.0 e o Microsoft Windows 2000, além de qualquer serviço de diretório compatível com LDAP e serviços de diretório Novell. ADSI é baseado em um modelo de provedor, para que se houver um novo provedor fornecendo acesse outro diretório, o aplicativo ADO poderão acessá-lo diretamente. O provedor ADSI é free-thread e Unicode habilitado.  
  
## <a name="connection-string-parameters"></a>Parâmetros de cadeia de caracteres de Conexão  
 Para se conectar ao provedor, defina o **provedor** argumento o [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade para o seguinte:  
  
```  
ADSDSOObject  
```  
  
 Lendo o [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade retornará essa cadeia de caracteres.  
  
## <a name="typical-connection-string"></a>Cadeia de caracteres de Conexão típica  
 Uma cadeia de caracteres de conexão típica para esse provedor é o seguinte:  
  
```  
"Provider=ADSDSOObject;User ID=MyUserID;Password=MyPassword;"  
```  
  
 A cadeia de caracteres consiste das seguintes palavras-chave.  
  
|Palavra-chave|Description|  
|-------------|-----------------|  
|**Provedor**|Especifica o provedor OLE DB para o serviço do Active Directory.|  
|**ID de usuário**|Especifica o nome de usuário. Se essa palavra-chave for omitida, o logon atual é usado.|  
|**Senha**|Especifica a senha do usuário. Se essa palavra-chave for omitida. Em seguida, o logon atual é usado.|  
  
> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que oferece suporte à autenticação do Windows, você deve especificar **Trusted_Connection = yes** ou **segurança integrada = SSPI** em vez de ID de usuário e senha informações na cadeia de conexão.  
  
## <a name="command-text"></a>Texto de comando  
 Uma cadeia de caracteres de texto do comando de quatro partes é reconhecida pelo provedor na sintaxe a seguir:  
  
```  
"Root; Filter; Attributes[; Scope]"  
```  
  
|Valor|Description|  
|-----------|-----------------|  
|*Root*|Indica o **ADsPath** objeto do qual iniciar a pesquisa (ou seja, a raiz da pesquisa).|  
|*Filter*|Indica o filtro de pesquisa no formato RFC 1960.|  
|*Atributos*|Indica uma lista delimitada por vírgulas de atributos a serem retornados.|  
|*Escopo*|Opcional. Um **cadeia de caracteres** que especifica o escopo da pesquisa. Pode ser uma destas opções:<br /><br /> -Base – Pesquisa somente o objeto base (raiz da pesquisa).<br />-OneLevel – Pesquisa apenas um nível.<br />-Subárvore, Pesquisa a subárvore inteira.|  
  
 Por exemplo:  
  
```  
"<LDAP://DC=ArcadiaBay,DC=COM>;(objectClass=*);sn, givenName; subtree"  
```  
  
 O provedor também dá suporte a SQL SELECT para o texto do comando. Por exemplo:  
  
```  
"SELECT title, telephoneNumber From 'LDAP://DC=Microsoft, DC=COM' WHERE   
objectClass='user' AND objectCategory='Person'"  
```  
  
## <a name="remarks"></a>Comentários  
 O provedor não aceita chamadas de procedimento armazenado ou nomes de tabela simples (por exemplo, o [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) propriedade sempre será **adCmdText**). Consulte a documentação de Interfaces de serviço do Active Directory para obter uma descrição mais completa dos elementos de texto de comando.  
  
## <a name="recordset-behavior"></a>Comportamento do conjunto de registros  
 As tabelas a seguir listam os recursos disponíveis em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto aberto usando esse provedor. O tipo de cursor estático (**adOpenStatic**) está disponível.  
  
 Para obter mais informações sobre **registros** comportamento para a sua configuração de provedor, execute o [dá suporte a](../../../ado/reference/ado-api/supports-method.md) método e enumerar o [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção do  **Conjunto de registros** para determinar se as propriedades dinâmicas específicos do provedor estão presentes.  
  
 **Disponibilidade de propriedades de conjunto de registros ADO padrão:**  
  
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
|[Origem](../../../ado/reference/ado-api/source-property-ado-recordset.md)|leitura/gravação|  
|[Estado](../../../ado/reference/ado-api/state-property-ado.md)|somente leitura|  
|[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)|somente leitura|  
  
 **Disponibilidade dos métodos de conjunto de registros ADO padrão:**  
  
|Método|Está disponível?|  
|------------|----------------|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|Não|  
|[Cancelar](../../../ado/reference/ado-api/cancel-method-ado.md)|Não|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|Não|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|Não|  
|[Clone](../../../ado/reference/ado-api/clone-method-ado.md)|Sim|  
|[Fechar](../../../ado/reference/ado-api/close-method-ado.md)|Sim|  
|[Delete (excluir)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|Não|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Sim|  
|[Migrar](../../../ado/reference/ado-api/move-method-ado.md)|Sim|  
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sim|  
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sim|  
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sim|  
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sim|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Sim|  
|[Abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Sim|  
|[Repetir](../../../ado/reference/ado-api/requery-method.md)|Sim|  
|[Ressincronização](../../../ado/reference/ado-api/resync-method.md)|Sim|  
|[Dá suporte a](../../../ado/reference/ado-api/supports-method.md)|Sim|  
|[Update (atualizar)](../../../ado/reference/ado-api/update-method.md)|Não|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|Não|  
  
 Para obter mais informações sobre o ADSI e as particularidades do provedor, consulte a documentação de Interfaces de serviço do Active Directory ou visite a página da Web do ADSI.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade CommandType (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)   
 [Propriedade ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)   
 [Coleção de propriedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Propriedade do provedor (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)

