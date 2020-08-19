---
description: Método Append (Procedimentos do ADOX)
title: Método Append (procedimentos ADOX) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8571790b596f037bb528df375c43c98b6b77c3a5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440478"
---
# <a name="append-method-adox-procedures"></a>Método Append (Procedimentos do ADOX)
Adiciona um novo objeto de [procedimento](../../../ado/reference/adox-api/procedure-object-adox.md) à coleção de [procedimentos](../../../ado/reference/adox-api/procedures-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Nome*  
 Um valor de **cadeia de caracteres** que especifica o nome do procedimento a ser criado e acrescentado.  
  
 *Comando*  
 Um objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) ADO que representa o procedimento para criar e acrescentar.  
  
## <a name="remarks"></a>Comentários  
 Cria um novo procedimento na fonte de dados com o nome e os atributos especificados no objeto **Command** .  
  
 Se o texto do comando que o usuário especifica representa uma exibição em vez de um procedimento, o comportamento depende do provedor que está sendo usado. **Append** falhará se o provedor não der suporte a comandos persistentes.  
  
> [!NOTE]
>  Ao usar o provedor de OLE DB para o Microsoft Jet, o método de **acréscimo** da coleção **procedures** permitirá que você especifique uma **exibição** em vez de um **procedimento** no parâmetro *Command* . O **modo de exibição** será adicionado à fonte de dados e será adicionado à coleção de **procedimentos** . Após o **acréscimo**, se as coleções de **procedimentos** e **exibições** forem atualizadas, a **exibição** não estará mais na coleção de **procedimentos** e aparecerá na coleção **views** .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Procedures (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Append Procedures (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Método Append (colunas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Método Append (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Método Append (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Método Append (chaves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Método Append (tabelas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Método Append (usuários do ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
