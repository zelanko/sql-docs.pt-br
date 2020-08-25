---
description: URLs absolutas e relativas
title: URLs absolutas e relativas | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- relative URLs [ADO]
- absolute URLs [ADO]
- URLs [ADO]
ms.assetid: 6a34a7ef-50cc-4c3d-82f7-106b9a8f3caf
author: rothja
ms.author: jroth
ms.openlocfilehash: 285fba254c025268abc9ea93f6d6e53e39a87aca
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806727"
---
# <a name="absolute-and-relative-urls"></a>URLs absolutas e relativas
Uma URL especifica o local de um destino armazenado em um computador local ou em rede. O destino pode ser um arquivo, diretório, página HTML, imagem, programa e assim por diante.  
  
 Uma *URL absoluta* contém todas as informações necessárias para localizar um recurso.  
  
 Uma *URL relativa* localiza um recurso usando uma URL absoluta como um ponto de partida. Na verdade, a "URL completa" do destino é especificada concatenando as URLs absolutas e relativas.  
  
 Uma *URL absoluta* usa o seguinte formato: *Scheme://Server/Path/Resource*  
  
 Uma URL relativa normalmente consiste apenas no *caminho*e, opcionalmente, no *recurso*, mas sem *esquema* ou *servidor*. As tabelas a seguir definem as partes individuais do formato de URL completo.  
  
 *esquema*  
 Especifica como o *recurso* deve ser acessado.  
  
 *server*  
 Especifica o nome do computador em que o *recurso* está localizado.  
  
 *path*  
 Especifica a sequência de diretórios que levam ao destino. Se o *recurso* for omitido, o destino será o último diretório no *caminho*.  
  
 *Kit*  
 Se incluído, *recurso* é o destino e normalmente é o nome de um arquivo. Pode ser um *arquivo simples,* contendo um único fluxo binário de bytes ou um *documento estruturado,* contendo um ou mais armazenamentos e fluxos binários de bytes.  
  
## <a name="url-scheme-registration"></a>Registro de esquema de URL  
 Se um provedor oferecer suporte a URLs, o provedor registrará um ou mais esquemas de URL. Registro significa que qualquer URL que usa o esquema invocará automaticamente o provedor registrado. Por exemplo, o esquema *http* é registrado no [provedor de OLE DB da Microsoft para publicação na Internet](../appendixes/microsoft-ole-db-provider-for-internet-publishing.md). O ADO assume que todas as URLs prefixadas com "http" representam arquivos ou pastas da Web a serem usadas com o provedor de publicação da Internet. Para obter informações sobre os esquemas registrados por seu provedor, consulte a documentação do provedor.  
  
## <a name="defining-context-with-a-url"></a>Definindo o contexto com uma URL  
 Uma função de uma conexão aberta, representada por um objeto de [conexão](../../reference/ado-api/connection-object-ado.md) , é restringir as operações subsequentes à fonte de dados representada por essa conexão. Ou seja, a conexão define o contexto para operações subsequentes.  
  
 Com o ADO 2,7 ou posterior, uma URL absoluta também pode definir um contexto. Por exemplo, quando um objeto de [registro](../../reference/ado-api/record-object-ado.md) é aberto com uma URL absoluta, um objeto de **conexão** é criado implicitamente para representar o recurso especificado pela URL.  
  
 Uma URL absoluta que define um contexto pode ser especificada no parâmetro *ActiveConnection* do método **Record** Object [Open](../../reference/ado-api/open-method-ado-record.md) . Uma URL absoluta também pode ser especificada como o valor da palavra-chave "URL =" no parâmetro do [método](../../reference/ado-api/open-method-ado-connection.md) *ConnectionString* do objeto de **conexão** e o parâmetro *ActiveConnection* do método [Open](../../reference/ado-api/open-method-ado-recordset.md) do objeto [Recordset](../../reference/ado-api/recordset-object-ado.md) .  
  
 O contexto também pode ser definido abrindo um **registro** ou objeto **Recordset** que representa um diretório, pois esses objetos já têm um objeto de **conexão** implicitamente ou explicitamente declarado que especifica o contexto.  
  
## <a name="scoped-operations"></a>Operações com escopo  
 O contexto também define o escopo, ou seja, o diretório e seus subdiretórios que podem participar de operações subsequentes. O objeto **Record** tem vários métodos com escopo que operam em um diretório e em todos os seus subdiretórios. Esses métodos incluem [CopyRecord](../../reference/ado-api/copyrecord-method-ado.md), [MoveRecord](../../reference/ado-api/moverecord-method-ado.md)e [DeleteRecord](../../reference/ado-api/deleterecord-method-ado.md).  
  
## <a name="relative-urls-as-command-text"></a>URLs relativas como texto de comando  
 Você pode especificar um comando a ser executado na fonte de dados digitando uma cadeia de caracteres no parâmetro *CommandText* do método [Execute](../../reference/ado-api/execute-method-ado-connection.md) do objeto de **conexão** e no parâmetro *Source* do método [Open](../../reference/ado-api/open-method-ado-recordset.md) do objeto **Recordset** .  
  
 Uma URL relativa pode ser especificada no parâmetro *CommandText* ou *Source* . Na verdade, a URL relativa não representa um comando, como um comando SQL; Ele simplesmente especifica os parâmetros. O contexto da conexão ativa deve ser uma URL absoluta e o parâmetro de *opção* deve ser definido como **adCmdTableDirect**.  
  
 Por exemplo, o exemplo de código a seguir mostra como abrir um **conjunto de registros** no arquivo de Readme25.txt do diretório WinNT/system32:  
  
```  
recordset.Open "system32/Readme25.txt", "URL=https://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
 A URL absoluta na cadeia de conexão especifica o servidor ( `YourServer` ) e o caminho ( `Winnt` ). Essa URL também define o contexto.  
  
 A URL relativa no texto do comando usa a URL absoluta como um ponto de partida e especifica o restante do caminho ( `system32` ) e o arquivo a ser aberto ( `Readme25.txt` ).  
  
 O campo de opções ( `adCmdTableDirect` ) indica que o tipo de comando é uma URL relativa.  
  
 Como outro exemplo, o código a seguir abrirá um **conjunto de registros** no conteúdo do `Winnt` diretório:  
  
```  
recordset.Open "", "URL=https://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
## <a name="ole-db-provider-supplied-url-schemes"></a>Esquemas de URL fornecidos pelo provedor de OLE DB  
 A parte principal de uma URL totalmente qualificada é o *esquema* usado para acessar o recurso identificado pelo restante da URL. Os exemplos são HTTP (Hypertext Transfer Protocol) e FTP (protocolo FTP).  
  
 O ADO dá suporte a provedores de OLE DB que reconhecem seus próprios esquemas de URL. Por exemplo, o [provedor de OLE DB da Microsoft para publicação na Internet](../appendixes/microsoft-ole-db-provider-for-internet-publishing.md)*,* que acessa os arquivos "publicados" do Windows 2000, reconhece o esquema http existente.  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto de conexão (ADO)](../../reference/ado-api/connection-object-ado.md)   
 [Objeto Record (ADO)](../../reference/ado-api/record-object-ado.md)   
 [Objeto Recordset (ADO)](../../reference/ado-api/recordset-object-ado.md)