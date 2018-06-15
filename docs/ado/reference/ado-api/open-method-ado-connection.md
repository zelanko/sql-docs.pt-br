---
title: Abra o método (Conexão ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_Open
- Connection15::Open
- _Connection::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 663defab-5545-4973-9036-24d5882c9737
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8035a40949e269fd8d8b039eb1931e8ed17c73c7
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280005"
---
# <a name="open-method-ado-connection"></a>Método Open (Conexão ADO)
Abre uma conexão a uma fonte de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ConnectionString*  
 Opcional. Um **cadeia de caracteres** valor que contém informações de conexão. Consulte o [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade para obter detalhes sobre as configurações válidas.  
  
 *UserID*  
 Opcional. Um **cadeia de caracteres** valor que contém um nome de usuário a ser usado ao estabelecer a conexão.  
  
 *Senha*  
 Opcional. Um **cadeia de caracteres** valor que contém uma senha para usar ao estabelecer a conexão.  
  
 *Opções*  
 Opcional. Um [ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md) valor que determina se esse método deve retornar depois (de forma síncrona) ou antes (de forma assíncrona) a conexão é estabelecida.  
  
## <a name="remarks"></a>Remarks  
 Usando o **abrir** método em um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto estabelece a conexão física com uma fonte de dados. Depois que esse método é concluído com êxito, a conexão está ativa e você pode executar comandos em relação a ela e processar os resultados.  
  
 Use opcional *ConnectionString* argumento para especificar uma cadeia de conexão que contém uma série de *argumento* *= valor* instruções separadas por ponto e vírgula, ou um recursos de arquivo ou diretório identificado por uma URL. O **ConnectionString** propriedade herda automaticamente o valor usado para o *ConnectionString* argumento. Portanto, você pode definir o **ConnectionString** propriedade o **Conexão** objeto antes de abri-lo ou usar o *ConnectionString* argumento para definir ou substituir os parâmetros de conexão atual durante a **abrir** chamada de método.  
  
 Se você passar o usuário e senha informações ambos o *ConnectionString* argumento e na opcional *UserID* e *senha* argumentos, o *UserID*  e *senha* argumentos substituirão os valores especificados na *ConnectionString*.  
  
 Quando você ter concluído suas operações em aberto **Conexão**, use o [fechar](../../../ado/reference/ado-api/close-method-ado.md) associados de método para liberar quaisquer recursos do sistema. Fechar um objeto não o remove da memória; Você pode alterar suas configurações de propriedade e usar o **abrir** método para abri-lo novamente mais tarde. Para eliminar completamente um objeto da memória, defina a variável de objeto para *nada*.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** quando usado em um cliente **Conexão** objeto, o **abrir** método realmente não estabelecer uma conexão ao servidor até que um [conjunto de registros ](../../../ado/reference/ado-api/recordset-object-ado.md) é aberta no **Conexão** objeto.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [Absolute e URLs relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo dos métodos de abertura e fechamento (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Exemplo dos métodos de abertura e fechamento (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Exemplo dos métodos de abertura e fechamento (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Método Open (ADO registro)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método Open (fluxo de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)
