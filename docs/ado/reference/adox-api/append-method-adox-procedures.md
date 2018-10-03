---
title: Método (procedimentos do ADOX) append | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedures::Append
- Procedures::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 38e3492c-c1e1-42e3-a71a-befdc90204db
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 348b2876e4293ad912383859ace47e462da31bcf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47707951"
---
# <a name="append-method-adox-procedures"></a>Método Append (Procedimentos do ADOX)
Adiciona um novo [procedimento](../../../ado/reference/adox-api/procedure-object-adox.md) do objeto para o [procedimentos](../../../ado/reference/adox-api/procedures-collection-adox.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Nome*  
 Um **cadeia de caracteres** valor que especifica o nome do procedimento para criar e anexar.  
  
 *Comando*  
 ADO [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto que representa o procedimento para criar e anexar.  
  
## <a name="remarks"></a>Comentários  
 Cria um novo procedimento na fonte de dados com o nome e atributos especificados na **comando** objeto.  
  
 Se o texto do comando que especifica o usuário representa uma exibição em vez de um procedimento, o comportamento depende do provedor que está sendo usado. **Acrescentar** falhará se o provedor não dá suporte a comandos de persistência.  
  
> [!NOTE]
>  Ao usar o provedor OLE DB para Microsoft Jet, o **procedimentos** coleção **Append** método permitirá que você especifique uma **exibição** em vez de um  **Procedimento** no *comando* parâmetro. O **modo de exibição** será adicionado à fonte de dados e será adicionado à **procedimentos** coleção. Após o **Append**, se o **procedimentos** e **modos de exibição** coleções são atualizadas, o **exibição** não será o **Procedimentos** coleta e aparecerão na **modos de exibição** coleção.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Procedures (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Append de procedimentos de exemplo do método (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Acrescentar o método (colunas do ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Acrescentar o método (grupos do ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Acrescentar o método (índices do ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Acrescentar o método (chaves do ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Acrescentar o método (tabelas do ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Acrescentar o método (usuários do ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
