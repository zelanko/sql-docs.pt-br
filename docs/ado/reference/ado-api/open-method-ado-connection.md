---
title: Método (Conexão ADO) Open | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_Open
- Connection15::Open
- _Connection::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 663defab-5545-4973-9036-24d5882c9737
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15115313613ea8f86dd2267c6be3c231cab92503
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931939"
---
# <a name="open-method-ado-connection"></a>Método Open (conexão ADO)
Abre uma conexão a uma fonte de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ConnectionString*  
 Opcional. Um **cadeia de caracteres** valor que contém informações de conexão. Consulte a [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade para obter detalhes sobre as configurações válidas.  
  
 *UserID*  
 Opcional. Um **cadeia de caracteres** valor que contém um nome de usuário a ser usada ao estabelecer a conexão.  
  
 *Senha*  
 Opcional. Um **cadeia de caracteres** valor que contém uma senha a ser usada ao estabelecer a conexão.  
  
 *Opções*  
 Opcional. Um [ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md) valor que determina se esse método deve retornar após (sincronicamente) ou antes (de forma assíncrona) a conexão seja estabelecida.  
  
## <a name="remarks"></a>Comentários  
 Usando o **aberto** método em um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto estabelece a conexão física com uma fonte de dados. Após esse método concluída com êxito, a conexão está funcionando e você pode emitir comandos em relação a ela e processar os resultados.  
  
 Usar a opção *ConnectionString* argumento para especificar uma cadeia de conexão que contém uma série de *argumento* *= valor* instruções separadas por ponto e vírgula, ou um recurso de arquivo ou diretório identificado com uma URL. O **ConnectionString** propriedade herda automaticamente o valor usado para o *ConnectionString* argumento. Portanto, você pode definir a **ConnectionString** propriedade da **Conexão** do objeto antes de abri-lo ou usar o *ConnectionString* argumento para definir ou substituir os parâmetros de conexão atual durante o **abrir** chamada de método.  
  
 Se você passar a senha informações de usuário e os dois na *ConnectionString* argumento e na opcional *UserID* e *senha* argumentos, o *UserID*  e *senha* argumentos substituirão os valores especificados na *ConnectionString*.  
  
 Quando você ter concluído suas operações ao longo de um aberto **Conexão**, use o [fechar](../../../ado/reference/ado-api/close-method-ado.md) associado de método para liberar todos os recursos do sistema. Um objeto de fechamento não o remove da memória; Você pode alterar suas configurações de propriedade e usar o **abrir** método para abri-lo novamente mais tarde. Para eliminar completamente um objeto da memória, defina a variável de objeto para *nada*.  
  
> [!NOTE]
>  **Uso do serviço de dados remotos** quando usado em um lado do cliente **Conexão** objeto, o **abrir** método, na verdade, não estabelece uma conexão com o servidor até que um [conjunto de registros ](../../../ado/reference/ado-api/recordset-object-ado.md) é aberta sobre a **Conexão** objeto.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [absoluta e relativa URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo dos métodos Open e Close (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Exemplo dos métodos Open e Close (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Exemplo dos métodos Open e Close (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Método Open (registro ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método Open (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)
