---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f15c5890300687a2d587a58a586d00bf2c8d0fd8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926361"
---
# <a name="absolute-and-relative-urls"></a>URLs absolutas e relativas
Uma URL especifica o local de um destino armazenado em um computador local ou em rede. O destino pode ser um arquivo, diretório, página HTML, imagem, programa e assim por diante.  
  
 Uma *URL absoluta* contém todas as informações necessárias para localizar um recurso.  
  
 Um *URL relativa* localiza um recurso usando uma URL absoluta como ponto de partida. Na verdade, o "preenchimento URL" de destino é especificado, concatenando as URLs absolutas e relativas.  
  
 Uma *URL absoluta* usa o seguinte formato: *scheme://server/path/resource*  
  
 Uma URL relativa normalmente consiste em apenas o *caminho*e, opcionalmente, o *resource*, mas nenhum *esquema* ou *server*. As tabelas a seguir definem as partes individuais do formato da URL completa.  
  
 *scheme*  
 Especifica como o *recurso* deve ser acessado.  
  
 *server*  
 Especifica o nome do computador no qual o *recurso* está localizado.  
  
 *path*  
 Especifica a sequência de diretórios que levam ao destino. Se *resource* é omitido, o destino é o último diretório na *caminho*.  
  
 *resource*  
 Se for incluído, *recurso* é o destino e normalmente é o nome de um arquivo. Pode ser um *arquivo simple,* que contém um único fluxo binário de bytes, ou um *documento estruturado,* que contém um ou mais armazenamentos e fluxos binários de bytes.  
  
## <a name="url-scheme-registration"></a>Registro de esquema de URL  
 Se um provedor dá suporte a URLs, o provedor será registrado um ou mais esquemas de URL. Registro significa que todas as URLs usando o esquema automaticamente chamará o provedor registrado. Por exemplo, o *http* esquema está registrada para o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). ADO pressupõe que todas as URLs prefixadas com "http" representam pastas da Web ou arquivos a serem usados com o provedor de publicação de Internet. Para obter informações sobre os esquemas registrados pelo seu provedor, consulte a documentação do provedor.  
  
## <a name="defining-context-with-a-url"></a>A definição de contexto com uma URL  
 Uma função de uma conexão aberta, representado por um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) do objeto, é restringir as operações subsequentes para a fonte de dados representado por essa conexão. Ou seja, a conexão define o contexto para operações subsequentes.  
  
 Com o ADO 2.7 ou posterior, uma URL absoluta também pode definir um contexto. Por exemplo, quando um [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto é aberto com uma URL absoluta, um **Conexão** objeto é criado implicitamente para representar o recurso especificado pela URL.  
  
 Uma URL absoluta que define um contexto pode ser especificada na *ActiveConnection* parâmetro do **registro** objeto [abrir](../../../ado/reference/ado-api/open-method-ado-record.md) método. Uma URL absoluta também pode ser especificada como o valor da "URL =" palavra-chave na **Conexão** objeto [abra](../../../ado/reference/ado-api/open-method-ado-connection.md) método *ConnectionString* parâmetro e o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto [aberto](../../../ado/reference/ado-api/open-method-ado-recordset.md) método *ActiveConnection* parâmetro.  
  
 Contexto também pode ser definido abrindo uma **registro** ou **conjunto de registros** objeto que representa um diretório, porque esses objetos já tem um implicitamente ou explicitamente declarado **Conexão**  objeto que especifica o contexto.  
  
## <a name="scoped-operations"></a>Operações com escopo  
 O contexto também define o escopo-ou seja, o diretório e seus subdiretórios que podem participar em operações subsequentes. O **registro** objeto tem vários métodos com escopo definido que operam em um diretório e todos os seus subdiretórios. Esses métodos incluem [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md), [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md), e [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md).  
  
## <a name="relative-urls-as-command-text"></a>URLs relativas como texto de comando  
 Você pode especificar um comando a ser executado na fonte de dados digitando uma cadeia de caracteres a *CommandText* parâmetro do **Conexão** do objeto [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) método e o  *Código-fonte* parâmetro do **conjunto de registros** do objeto [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) método.  
  
 Uma URL relativa pode ser especificada na *CommandText* ou *origem* parâmetro. A URL relativa, na verdade, não representam um comando, como um comando SQL; ela simplesmente especifica os parâmetros. O contexto de conexão do Active Directory deve ser uma URL absoluta e o *opção* parâmetro deve ser definido como **adCmdTableDirect**.  
  
 Por exemplo, o exemplo de código a seguir mostra como abrir um **Recordset** no arquivo do diretório system32/Winnt Readme25.txt:  
  
```  
recordset.Open "system32/Readme25.txt", "URL=https://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
 A URL absoluta na cadeia de conexão Especifica o servidor (`YourServer`) e o caminho (`Winnt`). Essa URL também define o contexto.  
  
 A URL relativa no texto do comando usa a URL absoluta como um ponto de partida e especifica o restante do caminho (`system32`) e o arquivo a ser aberto (`Readme25.txt`).  
  
 O campo options (`adCmdTableDirect`) indica que o tipo de comando é uma URL relativa.  
  
 Como outro exemplo, o código a seguir será aberta uma **conjunto de registros** no conteúdo do `Winnt` diretório:  
  
```  
recordset.Open "", "URL=https://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
## <a name="ole-db-provider-supplied-url-schemes"></a>Esquemas de URL fornecido pelo provedor do OLE DB  
 É a parte à esquerda de uma URL totalmente qualificada a *esquema* que é usado para acessar o recurso identificado pelo restante da URL. Os exemplos são HTTP (Hypertext Transfer Protocol) e FTP (File Transfer Protocol).  
  
 ADO dá suporte a provedores OLE DB que reconhecem a seus próprios esquemas de URL. Por exemplo, o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md) *,* que acessa arquivos "publicados" do Windows 2000, reconhece o esquema HTTP existente.  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
