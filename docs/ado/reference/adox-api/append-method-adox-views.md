---
title: Método (exibições do ADOX) append | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Views::raw_Append
- Views::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6070fd58-3237-4c77-a966-5b39ce5d57e4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f5f58ff2f38ff80d90750901b8943efc00f389c6
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718949"
---
# <a name="append-method-adox-views"></a>Método Append (Exibições do ADOX)
Cria um novo [modo de exibição](../../../ado/reference/adox-api/view-object-adox.md) do objeto e anexa-o para o [modos de exibição](../../../ado/reference/adox-api/views-collection-adox.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Views.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Nome*  
 Um **cadeia de caracteres** valor que especifica o nome da exibição a ser criada.  
  
 *Comando*  
 ADO [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto que representa a exibição a ser criada.  
  
## <a name="remarks"></a>Comentários  
 Cria uma nova exibição da fonte de dados com o nome e atributos especificados na **comando** objeto.  
  
 Se o texto do comando que o usuário Especifica representa um procedimento em vez de um modo de exibição, o comportamento depende do provedor. **Acrescentar** falhará se o provedor não dá suporte a comandos de persistência.  
  
> [!NOTE]
>  Ao usar o provedor OLE DB para Microsoft Jet, o **modos de exibição** coleção **Append** método permitirá que você especifique uma **procedimento** em vez de um **exibição**  no *comando* parâmetro. O **procedimento** será adicionado à fonte de dados e será adicionado à **modos de exibição** coleção. Após o **Append**, se o **procedimentos** e **modos de exibição** coleções são atualizadas, o **procedimento** não será o **Modos de exibição** coleta e aparecerão na **procedimentos** coleção.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Append de exibições de exemplo do método (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Acrescentar o método (colunas do ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Acrescentar o método (grupos do ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Acrescentar o método (índices do ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Acrescentar o método (chaves do ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Acrescentar o método (procedimentos do ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Acrescentar o método (tabelas do ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Método Append (Usuários do ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)
