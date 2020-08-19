---
description: Método OpenSchema
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1b0a92e7079338e290f228603767d6d15a3a351e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442918"
---
# <a name="openschema-method"></a>Método OpenSchema
Obtém informações de esquema de banco de dados do provedor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set recordset = connection.OpenSchema(QueryType, Criteria, SchemaID)  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) que contém informações de esquema. O **conjunto de registros** será aberto como um cursor estático somente leitura. O *QueryType* determina quais colunas aparecem no **conjunto de registros**.  
  
#### <a name="parameters"></a>Parâmetros  
 *QueryType*  
 Qualquer valor de [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) que representa o tipo de consulta de esquema a ser executado.  
  
 *Critérios*  
 Opcional. Uma matriz de restrições de consulta para cada opção *QueryType* , conforme listado em [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md).  
  
 *SchemaId*  
 O GUID de uma consulta de esquema de provedor não definida pela especificação de OLE DB. Esse parâmetro será necessário se *QueryType* for definido como **adSchemaProviderSpecific**; caso contrário, ele não será usado.  
  
## <a name="remarks"></a>Comentários  
 O método **OpenSchema** retorna informações autodescritivas sobre a fonte de dados, como quais tabelas estão na fonte de dados, as colunas nas tabelas e os tipos de dados com suporte.  
  
 O argumento *QueryType* é um GUID que indica as colunas (esquemas) retornadas. A especificação de OLE DB tem uma lista completa de esquemas.  
  
 O argumento de *critérios* limita os resultados de uma consulta de esquema. *Critérios* especifica uma matriz de valores que deve ocorrer em um subconjunto correspondente de colunas, chamadas de colunas de restrição, no **conjunto de registros**resultante.  
  
 A constante **adSchemaProviderSpecific** será usada para o argumento *QueryType* se o provedor definir suas próprias consultas de esquema não padrão fora daquelas listadas anteriormente. Quando essa constante é usada, o argumento *SchemaId* é necessário para passar o GUID da consulta de esquema a ser executada. Se *QueryType* for definido como **AdSchemaProviderSpecific** , mas *SchemaId* não for fornecido, ocorrerá um erro.  
  
 Os provedores não são necessários para dar suporte a todas as OLE DB consultas de esquema padrão. Especificamente, somente **adSchemaTables**, **adSchemaColumns**e **adSchemaProviderTypes** são exigidos pela especificação de OLE DB. No entanto, o provedor não precisa dar suporte às restrições de *critérios* listadas anteriormente para essas consultas de esquema.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** O método **OpenSchema** não está disponível em um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) do lado do cliente.  
  
> [!NOTE]
>  Em Visual Basic, as colunas que têm um inteiro não assinado de quatro bytes (DBTYPE UI4) no **conjunto de registros** retornado do método **OpenSchema** no objeto de **conexão** não podem ser comparadas com outras variáveis. Para obter mais informações sobre tipos de dados OLE DB, consulte [tipos de dados em OLE DB (OLE DB)](https://msdn.microsoft.com/6039292f-74e0-49b2-b133-17bc117ebf6a) e [Apêndice A: tipos de dados](https://msdn.microsoft.com/e3a0533a-2196-4eb0-a31e-92fe9556ada6) na referência do programador de OLE DB da Microsoft.  
  
> [!NOTE]
>  **Usuários do Visual C/C++** Quando não usar cursores do lado do cliente, recuperar o "ORDINAL_POSITION" de um esquema de coluna no ADO retorna uma variante do tipo VT_R8 no MDAC 2,7, no MDAC 2,8 e no Windows Data Access Components (Windows DAC) 6,0, enquanto o tipo usado no MDAC 2,6 foi VT_I4. Os programas escritos para o MDAC 2,6 que procuram apenas uma variante retornada do tipo VT_I4 obterão um zero para cada ordinal se forem executados em MDAC 2,7, MDAC 2,8 e Windows DAC 6,0 sem modificação. Essa alteração foi feita porque o tipo de dados que OLE DB retorna é DBTYPE_UI4 e, no tipo de VT_I4 assinado, não há espaço suficiente para conter todos os valores possíveis sem que o truncamento esteja ocorrendo e causando uma perda de dados.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método OpenSchema (VB)](../../../ado/reference/ado-api/openschema-method-example-vb.md)   
 [Exemplo do método OpenSchema (VC + +)](../../../ado/reference/ado-api/openschema-method-example-vc.md)   
 [Método Open (conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Método Open (registro ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método Open (fluxo ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
