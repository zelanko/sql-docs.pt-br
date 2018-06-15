---
title: Abra o método (registro de ADO) | Microsoft Docs
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
- _Record::raw_Open
- _Record::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: ab79a623-88a9-40b6-a017-a658bf19b778
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa486265426f52dfd5986c6d173bcd1ffdb45210
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280505"
---
# <a name="open-method-ado-record"></a>Método Open (ADO registro)
Abre um existente [registro](../../../ado/reference/ado-api/record-object-ado.md) de objeto ou cria um novo item representado pelo **registro**, como um arquivo ou diretório.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Open Source, ActiveConnection, Mode, CreateOptions, Options, UserName, Password  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Origem*  
 Opcional. Um **Variant** que pode representar a URL da entidade a ser representado por esse **registro** objeto, um **comando**, aberto [registros](../../../ado/reference/ado-api/recordset-object-ado.md) ou outro **registro** objeto, uma cadeia de caracteres que contém uma instrução SQL SELECT ou um nome de tabela.  
  
 *ActiveConnection*  
 Opcional. Um **Variant** que representa a cadeia de conexão ou abra [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
 *Modo*  
 Opcional. Um [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) valor que especifica o modo de acesso para os resultantes **registro** objeto. Valor padrão é **adModeUnknown**.  
  
 *CreateOptions*  
 Opcional. Um [RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md) valor que especifica se um arquivo ou diretório existente deve ser aberto ou se um novo arquivo ou diretório deve ser criado. Valor padrão é **adFailIfNotExists**. Se definido como o valor padrão, o modo de acesso é obtido o [modo](../../../ado/reference/ado-api/mode-property-ado.md) propriedade. Esse parâmetro é ignorado quando o *fonte* parâmetro não contém uma URL.  
  
 *Opções*  
 Opcional. Um [RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md) valor que especifica opções para abrir o **registro**. Valor padrão é **adOpenRecordUnspecified**. Esses valores podem ser combinados.  
  
 *UserName*  
 Opcional. Um **cadeia de caracteres** valor que contém a ID de usuário que, se necessário, conceda acesso ao *fonte*.  
  
 *Senha*  
 Opcional. Um **cadeia de caracteres** valor que contém a senha, se necessário, verifica *nome de usuário*.  
  
## <a name="remarks"></a>Remarks  
 *Origem* pode ser:  
  
-   UMA URL. Se o protocolo para a URL é http, o provedor de Internet será invocado por padrão. Se a URL aponta para um nó que contém um script executável (como um. Página ASP), um **registro** que contém a origem em vez de executado conteúdo é aberto por padrão. Use o *opções* argumento para modificar esse comportamento.  
  
-   Um **registro** objeto. Um **registro** objeto aberto de outro **registro** será clone original **registro** objeto.  
  
-   Um **comando** objeto. Aberto **registro** objeto representa a única linha retornada, executando o **comando**. Se os resultados contêm mais de uma única linha, o conteúdo da primeira linha é colocado no registro e erro pode ser adicionado para o **erros** coleção.  
  
-   Uma instrução SQL SELECT. Aberto **registro** objeto representa a única linha retornada, executando o conteúdo da cadeia de caracteres. Se os resultados contêm mais de uma única linha, o conteúdo da primeira linha é colocado no registro e erro pode ser adicionado para o **erros** coleção.  
  
-   Um nome de tabela.  
  
 Se o **registro** objeto representa uma entidade que não pode ser acessada com uma URL (por exemplo, uma linha de um **registros** derivado de um banco de dados), os valores dos dois a [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)propriedade e o campo acessado com o **adRecordURL** constante são nulos.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [Absolute e URLs relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método Open (Conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método Open (fluxo de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)
