---
title: Método OpenSchema | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::OpenSchema
- Connection15::raw_OpenSchema
helpviewer_keywords:
- OpenSchema method [ADO]
ms.assetid: 850cf3ce-f18f-4e7c-8597-96c1dc504866
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 52eaf3a58ae7f6eeaddecb943b5a129dec5e44e0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="openschema-method"></a>Método OpenSchema
Obtém informações de esquema de banco de dados do provedor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set recordset = connection.OpenSchema(QueryType, Criteria, SchemaID)  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto que contém informações de esquema. O **registros** será aberta como um cursor somente leitura, estático. O *QueryType* determina quais colunas são exibidas no **registros**.  
  
#### <a name="parameters"></a>Parâmetros  
 *QueryType*  
 Qualquer [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) valor que representa o tipo de consulta de esquema para executar.  
  
 *Critérios*  
 Opcional. Uma matriz de restrições de consulta para cada *QueryType* opção, conforme listado na [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md).  
  
 *SchemaID*  
 O GUID de uma consulta de esquema do provedor não é definida pela especificação do OLE DB. Esse parâmetro é necessário se *QueryType* é definido como **adSchemaProviderSpecific**; caso contrário, ele não é usado.  
  
## <a name="remarks"></a>Remarks  
 O **OpenSchema** método retorna uma informações sobre a fonte de dados, como o que são tabelas na fonte de dados, as colunas nas tabelas, e os tipos de dados com suporte.  
  
 O *QueryType* argumento é um GUID que indica as colunas (esquemas) é retornado. A especificação OLE DB tem uma lista completa de esquemas.  
  
 O *critérios* argumento limita os resultados de uma consulta de esquema. *Critérios de* Especifica uma matriz de valores que devem ocorrer em um subconjunto correspondente de colunas, chamadas colunas de restrição, no resultante **registros**.  
  
 A constante **adSchemaProviderSpecific** é usado para o *QueryType* argumento se o provedor define suas próprias consultas de esquema padrão fora de tais listadas anteriormente. Quando essa constante é usado, o *SchemaID* argumento é necessário para passar o GUID da consulta de esquema para executar. Se *QueryType* é definido como **adSchemaProviderSpecific** mas *SchemaID* não for fornecido, ocorrerá um erro.  
  
 Provedores não são necessários para dar suporte a todas as consultas de esquema padrão de OLE DB. Especificamente, apenas **adSchemaTables**, **adSchemaColumns**, e **adSchemaProviderTypes** necessários para a especificação OLE DB. No entanto, o provedor não é necessário para dar suporte a *critérios* as restrições listadas anteriormente para as consultas de esquema.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** o **OpenSchema** método não está disponível em um cliente [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
> [!NOTE]
>  No Visual Basic, colunas que têm um inteiro não assinado de quatro bytes (DBTYPE UI4) no **registros** retornado do **OpenSchema** método no **Conexão** o objeto não pode comparado com outras variáveis. Para obter mais informações sobre tipos de dados OLE DB, consulte [tipos de dados OLE DB (OLE DB)](http://msdn.microsoft.com/en-us/6039292f-74e0-49b2-b133-17bc117ebf6a) e [tipos de dados do apêndice a:](http://msdn.microsoft.com/en-us/e3a0533a-2196-4eb0-a31e-92fe9556ada6) de referência Microsoft OLE DB do programador.  
  
> [!NOTE]
>  **Os usuários do Visual C/C++** ao não usar cursores do lado do cliente, recuperar "ORDINAL_POSITION" de um esquema de coluna no ADO retorna uma variante do tipo VT_R8 no MDAC 2.7, MDAC 2.8 e Windows Data Access Components (Windows DAC) 6.0, enquanto o tipo usado no MDAC 2.6 foi VT_I4. Programas escritos para o MDAC 2.6 que procuram somente uma variante retornada do tipo que vt_i4 receberia um zero para cada ordinal se executados no Windows DAC 6.0, MDAC 2.8 e MDAC 2.7 sem modificação. Essa alteração foi feita porque o tipo de dados OLE DB retorna DBTYPE_UI4 e no tipo VT_I4 assinado não há espaço suficiente para conter todos os possíveis valores sem truncamento possivelmente ocorrendo e causando uma perda de dados.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método OpenSchema (VB)](../../../ado/reference/ado-api/openschema-method-example-vb.md)   
 [Exemplo do método OpenSchema (VC + +)](../../../ado/reference/ado-api/openschema-method-example-vc.md)   
 [Método Open (Conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Método Open (ADO registro)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método Open (fluxo de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
