---
title: Método Open (conexão ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 31ce05ce069e0eb3e7d6431b296f40824a8acd3a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762197"
---
# <a name="open-method-ado-connection"></a>Método Open (conexão ADO)
Abre uma conexão com uma fonte de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ConnectionString*  
 Opcional. Um valor de **cadeia de caracteres** que contém informações de conexão. Consulte a propriedade [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) para obter detalhes sobre as configurações válidas.  
  
 *ID*  
 Opcional. Um valor de **cadeia de caracteres** que contém um nome de usuário a ser usado ao estabelecer a conexão.  
  
 *Senha*  
 Opcional. Um valor de **cadeia de caracteres** que contém uma senha a ser usada ao estabelecer a conexão.  
  
 *Opções*  
 Opcional. Um valor [ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md) que determina se esse método deve retornar após (de forma síncrona) ou antes (assincronamente) que a conexão seja estabelecida.  
  
## <a name="remarks"></a>Comentários  
 O uso do método **Open** em um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) estabelece a conexão física com uma fonte de dados. Depois que esse método for concluído com êxito, a conexão estará ativa e você poderá emitir comandos para ele e processar os resultados.  
  
 Use o argumento *ConnectionString* opcional para especificar uma cadeia de conexão que contém uma série de instruções *Argument* *= Value* separadas por ponto e vírgula, ou um recurso de arquivo ou diretório identificado com uma URL. A propriedade **ConnectionString** herda automaticamente o valor usado para o argumento *ConnectionString* . Portanto, você pode definir a propriedade **ConnectionString** do objeto de **conexão** antes de abri-lo ou usar o argumento *ConnectionString* para definir ou substituir os parâmetros de conexão atuais durante a chamada do método **Open** .  
  
 Se você passar informações de usuário e senha tanto no argumento *ConnectionString* quanto nos argumentos de *userid* e *senha* opcionais, os argumentos *userid* e *password* substituirão os valores especificados em *ConnectionString*.  
  
 Quando você tiver concluído suas operações em uma **conexão**aberta, use o método [Close](../../../ado/reference/ado-api/close-method-ado.md) para liberar todos os recursos do sistema associados. Fechar um objeto não o Remove da memória; Você pode alterar suas configurações de propriedade e usar o método **Open** para abri-lo novamente mais tarde. Para eliminar completamente um objeto da memória, defina a variável de objeto como *Nothing*.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** Quando usado em um objeto de **conexão** do lado do cliente, o método **Open** não estabelece realmente uma conexão com o servidor até que um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) seja aberto no objeto **Connection** .  
  
> [!NOTE]
>  As URLs que usam o esquema http invocarão automaticamente o [provedor do Microsoft OLE DB para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [URLs absolutas e relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Open e Close (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Exemplo dos métodos Open e Close (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Exemplo dos métodos Open e Close (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Método Open (registro ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método Open (fluxo ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)
