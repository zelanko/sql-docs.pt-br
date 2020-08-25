---
description: Provedor do Microsoft OLE DB para Microsoft Active Directory Service
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c196b790299c4c241e5c8eda762b43115b71a038
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806580"
---
# <a name="microsoft-ole-db-provider-for-microsoft-active-directory-service"></a>Provedor do Microsoft OLE DB para Microsoft Active Directory Service
O provedor de interfaces do serviço de Active Directory (ADSI) permite que o ADO se conecte a serviços de diretório heterogêneos por meio de ADSI. Isso fornece aos aplicativos ADO acesso somente leitura aos serviços de diretório do Microsoft Windows NT 4,0 e do Microsoft Windows 2000, além de qualquer serviço de diretório compatível com LDAP e serviços de Diretório Novell. A própria ADSI se baseia em um modelo de provedor, de modo que, se houver um novo provedor que dê acesso a outro diretório, o aplicativo ADO poderá acessá-lo diretamente. O provedor ADSI está livre de threads e Unicode habilitado.  
  
## <a name="connection-string-parameters"></a>Parâmetros de cadeia de conexão  
 Para se conectar a esse provedor, defina o argumento do **provedor** da propriedade [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md) para o seguinte:  
  
```vb
ADSDSOObject  
```  
  
 A leitura da propriedade [Provider](../../reference/ado-api/provider-property-ado.md) retornará essa cadeia de caracteres também.  
  
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
|*Escopo*|Opcional. Uma **cadeia de caracteres** que especifica o escopo da pesquisa. Um dos seguintes pode ser feito:<br /><br /> -Base-pesquise somente o objeto base (raiz da pesquisa).<br />-Onelevet-Pesquisar apenas um nível.<br />-Subtree – Pesquise toda a subárvore.|  
  
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
 O provedor não aceita chamadas de procedimento armazenado ou nomes de tabela simples (por exemplo, a propriedade [CommandType](../../reference/ado-api/commandtype-property-ado.md) será sempre **adCmdText**). Consulte a documentação de interfaces de serviço Active Directory para obter uma descrição mais completa dos elementos de texto do comando.  
  
## <a name="recordset-behavior"></a>Comportamento do conjunto de registros  
 As tabelas a seguir listam os recursos disponíveis em um objeto [Recordset](../../reference/ado-api/recordset-object-ado.md) aberto usando esse provedor. Somente o tipo de cursor estático (**adOpenStatic**) está disponível.  
  
 Para obter mais informações sobre o comportamento do **conjunto de registros** para a configuração do provedor, execute o método de [suporte](../../reference/ado-api/supports-method.md) e enumere a coleção [Properties](../../reference/ado-api/properties-collection-ado.md) do **conjunto de registros** para determinar se as propriedades dinâmicas específicas do provedor estão presentes.  
  
 **Disponibilidade das propriedades padrão do conjunto de registros ADO:**  
  
|Propriedade|Disponibilidade|  
|--------------|------------------|  
|[AbsolutePage](../../reference/ado-api/absolutepage-property-ado.md)|leitura/gravação|  
|[AbsolutePosition](../../reference/ado-api/absoluteposition-property-ado.md)|leitura/gravação|  
|[ActiveConnection](../../reference/ado-api/activeconnection-property-ado.md)|somente leitura|  
|[BOF](../../reference/ado-api/bof-eof-properties-ado.md)|somente leitura|  
|[Indicador](../../reference/ado-api/bookmark-property-ado.md)|leitura/gravação|  
|[CacheSize](../../reference/ado-api/cachesize-property-ado.md)|leitura/gravação|  
|[CursorLocation](../../reference/ado-api/cursorlocation-property-ado.md)|sempre **adUseServer**|  
|[CursorType](../../reference/ado-api/cursortype-property-ado.md)|sempre **adOpenStatic**|  
|[EditMode](../../reference/ado-api/editmode-property.md)|sempre **adEditNone**|  
|[EOF](../../reference/ado-api/bof-eof-properties-ado.md)|somente leitura|  
|[Filter](../../reference/ado-api/filter-property.md)|leitura/gravação|  
|[LockType](../../reference/ado-api/locktype-property-ado.md)|leitura/gravação|  
|[MarshalOptions](../../reference/ado-api/marshaloptions-property-ado.md)|não disponível|  
|[MaxRecords](../../reference/ado-api/maxrecords-property-ado.md)|leitura/gravação|  
|[PageCount](../../reference/ado-api/pagecount-property-ado.md)|somente leitura|  
|[PageSize](../../reference/ado-api/pagesize-property-ado.md)|leitura/gravação|  
|[RecordCount](../../reference/ado-api/recordcount-property-ado.md)|somente leitura|  
|[Origem](../../reference/ado-api/source-property-ado-recordset.md)|leitura/gravação|  
|[State](../../reference/ado-api/state-property-ado.md)|somente leitura|  
|[Status](../../reference/ado-api/status-property-ado-recordset.md)|somente leitura|  
  
 **Disponibilidade de métodos Recordset padrão do ADO:**  
  
|Método|Disponível?|  
|------------|----------------|  
|[AddNew](../../reference/ado-api/addnew-method-ado.md)|No|  
|[Cancelar](../../reference/ado-api/cancel-method-ado.md)|No|  
|[CancelBatch](../../reference/ado-api/cancelbatch-method-ado.md)|No|  
|[CancelUpdate](../../reference/ado-api/cancelupdate-method-ado.md)|No|  
|[Clone](../../reference/ado-api/clone-method-ado.md)|Yes|  
|[Fechar](../../reference/ado-api/close-method-ado.md)|Yes|  
|[Delete (excluir)](../../reference/ado-api/delete-method-ado-recordset.md)|No|  
|[GetRows](../../reference/ado-api/getrows-method-ado.md)|Yes|  
|[Mover](../../reference/ado-api/move-method-ado.md)|Yes|  
|[MoveFirst](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Yes|  
|[Velas](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Yes|  
|[MoveNext](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Yes|  
|[MovePrevious](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Yes|  
|[NextRecordset](../../reference/ado-api/nextrecordset-method-ado.md)|Yes|  
|[Abrir](../../reference/ado-api/open-method-ado-recordset.md)|Yes|  
|[Repita](../../reference/ado-api/requery-method.md)|Yes|  
|[Sincronizar novamente](../../reference/ado-api/resync-method.md)|Yes|  
|[Suporta](../../reference/ado-api/supports-method.md)|Yes|  
|[Atualização](../../reference/ado-api/update-method.md)|No|  
|[UpdateBatch](../../reference/ado-api/updatebatch-method.md)|No|  
  
 Para obter mais informações sobre a ADSI e as especificidades do provedor, consulte a documentação de interfaces de serviço Active Directory ou visite a página da Web ADSI.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade CommandType (ADO)](../../reference/ado-api/commandtype-property-ado.md)   
 [Propriedade ConnectionString (ADO)](../../reference/ado-api/connectionstring-property-ado.md)   
 [Coleção Properties (ADO)](../../reference/ado-api/properties-collection-ado.md)   
 [Propriedade Provider (ADO)](../../reference/ado-api/provider-property-ado.md)   
 [Objeto Recordset (ADO)](../../reference/ado-api/recordset-object-ado.md)   
 [Método Supports](../../reference/ado-api/supports-method.md)