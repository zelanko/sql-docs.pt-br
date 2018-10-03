---
title: Método OpenSchema | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::OpenSchema
- Connection15::raw_OpenSchema
helpviewer_keywords:
- OpenSchema method [ADO]
ms.assetid: 850cf3ce-f18f-4e7c-8597-96c1dc504866
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3481d9b7c186f3492e403b6881f4ffafbe90912b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787275"
---
# <a name="openschema-method"></a>Método OpenSchema
Obtém informações de esquema de banco de dados do provedor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set recordset = connection.OpenSchema(QueryType, Criteria, SchemaID)  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto que contém informações de esquema. O **Recordset** será aberto como um cursor de somente leitura, estático. O *QueryType* determina quais colunas são exibidas na **conjunto de registros**.  
  
#### <a name="parameters"></a>Parâmetros  
 *QueryType*  
 Qualquer [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) valor que representa o tipo de consulta de esquema a ser executada.  
  
 *Critérios*  
 Opcional. Uma matriz de restrições de consulta para cada *QueryType* opção, conforme listado na [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md).  
  
 *SchemaID*  
 O GUID de uma consulta de esquema do provedor não definido pela especificação do OLE DB. Esse parâmetro é necessário se *QueryType* é definido como **adSchemaProviderSpecific**; caso contrário, ele não é usado.  
  
## <a name="remarks"></a>Comentários  
 O **OpenSchema** método retorna um nome bastante auto-explicativo informações sobre a fonte de dados, como o que são tabelas na fonte de dados, as colunas nas tabelas, e os tipos de dados com suporte.  
  
 O *QueryType* argumento é um GUID que indica as colunas (esquemas) é retornado. A especificação OLE DB tem uma lista completa de esquemas.  
  
 O *critérios* argumento limita os resultados de uma consulta de esquema. *Critérios* Especifica uma matriz de valores que devem ocorrer em um subconjunto correspondente de colunas, chamadas colunas de restrição, no resultante **conjunto de registros**.  
  
 A constante **adSchemaProviderSpecific** é usado para o *QueryType* argumento se o provedor define suas próprias consultas de esquema não padrão fora de tais listados anteriormente. Quando essa constante é usada, o *SchemaID* argumento é obrigatório para transmitir o GUID do esquema de consulta a executar. Se *QueryType* é definido como **adSchemaProviderSpecific** mas *SchemaID* não for fornecido, ocorrerá um erro.  
  
 Provedores não são necessários para dar suporte a todas as consultas de esquema padrão de OLE DB. Especificamente, apenas **adSchemaTables**, **adSchemaColumns**, e **adSchemaProviderTypes** são necessários para a especificação OLE DB. No entanto, o provedor não é necessário para dar suporte a *critérios* restrições listadas anteriormente para essas consultas de esquema.  
  
> [!NOTE]
>  **Uso do serviço de dados remotos** as **OpenSchema** método não está disponível em um lado do cliente [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
> [!NOTE]
>  No Visual Basic, as colunas que têm um inteiro sem sinal de quatro bytes (DBTYPE UI4) na **conjunto de registros** retornados do **OpenSchema** método no **Conexão** objeto não é possível ser comparada a outras variáveis. Para obter mais informações sobre tipos de dados OLE DB, consulte [tipos de dados no OLE DB (OLE DB)](http://msdn.microsoft.com/6039292f-74e0-49b2-b133-17bc117ebf6a) e [tipos de dados do apêndice a:](http://msdn.microsoft.com/e3a0533a-2196-4eb0-a31e-92fe9556ada6) na referência do Microsoft OLE DB do programador.  
  
> [!NOTE]
>  **Os usuários do Visual C/C++** quando não estiver usando cursores do lado do cliente, recuperar o "ORDINAL_POSITION" de um esquema de coluna no ADO retorna uma variante do tipo VT_R8 no MDAC 2.7, MDAC 2.8 e Windows Data Access Components (Windows DAC) 6.0, enquanto o tipo usado no MDAC 2.6 era VT_I4. Programas escritos para o MDAC 2.6 que procuram somente uma variante retornado do tipo que vt_i4 obteria um zero para cada ordinal se executados no MDAC 2.7, MDAC 2.8 e 6.0 do Windows DAC sem modificação. Essa alteração foi feita porque o tipo de dados OLE DB retorna é DBTYPE_UI4 e no tipo VT_I4 assinado não há espaço suficiente para conter todos os possíveis valores sem truncamento, possivelmente, ocorrendo e, assim, causando uma perda de dados.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método OpenSchema (VB)](../../../ado/reference/ado-api/openschema-method-example-vb.md)   
 [Exemplo do método OpenSchema (VC + +)](../../../ado/reference/ado-api/openschema-method-example-vc.md)   
 [Método Open (Conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Método Open (registro ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método Open (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
