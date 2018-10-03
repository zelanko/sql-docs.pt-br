---
title: Método (registro ADO) Open | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_Open
- _Record::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: ab79a623-88a9-40b6-a017-a658bf19b778
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4d105d648c7877e7099dea637c2a2c6a094985f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47675454"
---
# <a name="open-method-ado-record"></a>Método Open (Registro do ADO)
Abre um existente [registro](../../../ado/reference/ado-api/record-object-ado.md) do objeto ou cria um novo item representado pelo **registro**, como um arquivo ou diretório.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Open Source, ActiveConnection, Mode, CreateOptions, Options, UserName, Password  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Origem*  
 Opcional. Um **Variant** que pode representar a URL da entidade a ser representado por esse **registro** objeto, uma **comando**, um aberto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ou outra **registro** object, uma cadeia de caracteres que contém uma instrução SQL SELECT ou um nome de tabela.  
  
 *ActiveConnection*  
 Opcional. Um **Variant** que representa a cadeia de conexão ou abra [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
 *Modo*  
 Opcional. Um [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) valor que especifica o modo de acesso para o resultante **registro** objeto. Valor padrão é **adModeUnknown**.  
  
 *CreateOptions*  
 Opcional. Um [RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md) valor que especifica se um arquivo ou diretório existente deve ser aberto ou um novo arquivo ou diretório deve ser criado. Valor padrão é **adFailIfNotExists**. Se definido como o valor padrão, o modo de acesso é obtido a [modo](../../../ado/reference/ado-api/mode-property-ado.md) propriedade. Esse parâmetro é ignorado quando o *origem* parâmetro não contém uma URL.  
  
 *Opções*  
 Opcional. Um [RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md) valor que especifica opções para abrir o **registro**. Valor padrão é **adOpenRecordUnspecified**. Esses valores podem ser combinados.  
  
 *UserName*  
 Opcional. Um **cadeia de caracteres** valor que contém a ID de usuário que, se for necessário, autoriza o acesso ao *origem*.  
  
 *Senha*  
 Opcional. Um **cadeia de caracteres** valor que contém a senha que, se for necessário, verifica *nome de usuário*.  
  
## <a name="remarks"></a>Comentários  
 *Origem* pode ser:  
  
-   UMA URL. Se o protocolo para a URL é http, o provedor de Internet será invocado por padrão. Se a URL aponta para um nó que contém um script executável (como um. Página ASP), uma **registro** que contém a origem em vez de executado conteúdo é aberta por padrão. Use o *opções* argumento para modificar esse comportamento.  
  
-   Um **registro** objeto. Um **registro** objeto aberto de outro **registro** será clonar original **registro** objeto.  
  
-   Um **comando** objeto. Aberta **registro** objeto representa a única linha retornada, executando o **comando**. Se os resultados contiverem mais de uma única linha, o conteúdo da primeira linha é colocado no registro e pode ser adicionado a um erro para o **erros** coleção.  
  
-   Uma instrução SQL SELECT. Aberta **registro** objeto representa a única linha retornada, executando o conteúdo da cadeia de caracteres. Se os resultados contiverem mais de uma única linha, o conteúdo da primeira linha é colocado no registro e pode ser adicionado a um erro para o **erros** coleção.  
  
-   Um nome de tabela.  
  
 Se o **registro** objeto representa uma entidade que não pode ser acessada com uma URL (por exemplo, uma linha de uma **conjunto de registros** derivado de um banco de dados), os valores de ambos o [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)as propriedades e os campos acessados com o **adRecordURL** constante são nulos.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [absoluta e relativa URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método Open (Conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método Open (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)
