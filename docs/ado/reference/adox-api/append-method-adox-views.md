---
title: "Método (ADOX exibições) append | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Views::raw_Append
- Views::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6070fd58-3237-4c77-a966-5b39ce5d57e4
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 535f25f475f6357d467e2f7ac19a96ed6eea1605
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="append-method-adox-views"></a>Método (ADOX exibições) append
Cria um novo [exibição](../../../ado/reference/adox-api/view-object-adox.md) do objeto e anexa-o para o [exibições](../../../ado/reference/adox-api/views-collection-adox.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Views.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Nome*  
 Um **cadeia de caracteres** valor que especifica o nome da exibição a ser criada.  
  
 *Comando*  
 ADO [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto que representa o modo de exibição para criar.  
  
## <a name="remarks"></a>Comentários  
 Cria uma nova exibição da fonte de dados com o nome e atributos especificados no **comando** objeto.  
  
 Se o texto do comando que especifica o usuário representa um procedimento em vez de um modo de exibição, o comportamento depende do provedor. **Acrescentar** falhará se o provedor não oferece suporte a comandos persistentes.  
  
> [!NOTE]
>  Ao usar o provedor OLE DB para Microsoft Jet, o **exibições** coleção **Append** método permitirá que você especifique um **procedimento** em vez de **exibição ** no *comando* parâmetro. O **procedimento** será adicionado à fonte de dados e será adicionado ao **exibições** coleção. Após o **Append**, se o **procedimentos** e **exibições** coleções são atualizadas, o **procedimento** não será o **Exibições** coleta e aparecerão no **procedimentos** coleção.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de acrescentar o exemplo de método (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Acrescente o método (ADOX colunas)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [(Grupos de ADOX) do método append](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Método (ADOX índices) append](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [(ADOX chaves) do método append](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Acrescente o método (ADOX procedimentos)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [(Tabelas ADOX) do método append](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Método Append (Usuários do ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)
