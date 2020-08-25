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
ms.openlocfilehash: 3f416d8223e828d724f1eabbe4ab82061204af0f
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771405"
---
# <a name="append-method-adox-procedures"></a>Método Append (Procedimentos do ADOX)
Adiciona um novo objeto de [procedimento](./procedure-object-adox.md) à coleção de [procedimentos](./procedures-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Nome*  
 Um valor de **cadeia de caracteres** que especifica o nome do procedimento a ser criado e acrescentado.  
  
 *Comando*  
 Um objeto de [comando](../ado-api/command-object-ado.md) ADO que representa o procedimento para criar e acrescentar.  
  
## <a name="remarks"></a>Comentários  
 Cria um novo procedimento na fonte de dados com o nome e os atributos especificados no objeto **Command** .  
  
 Se o texto do comando que o usuário especifica representa uma exibição em vez de um procedimento, o comportamento depende do provedor que está sendo usado. **Append** falhará se o provedor não der suporte a comandos persistentes.  
  
> [!NOTE]
>  Ao usar o provedor de OLE DB para o Microsoft Jet, o método de **acréscimo** da coleção **procedures** permitirá que você especifique uma **exibição** em vez de um **procedimento** no parâmetro *Command* . O **modo de exibição** será adicionado à fonte de dados e será adicionado à coleção de **procedimentos** . Após o **acréscimo**, se as coleções de **procedimentos** e **exibições** forem atualizadas, a **exibição** não estará mais na coleção de **procedimentos** e aparecerá na coleção **views** .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Procedures (ADOX)](./procedures-collection-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Append Procedures (VB)](./procedures-append-method-example-vb.md)   
 [Método Append (colunas ADOX)](./append-method-adox-columns.md)   
 [Método Append (grupos ADOX)](./append-method-adox-groups.md)   
 [Método Append (índices ADOX)](./append-method-adox-indexes.md)   
 [Método Append (chaves ADOX)](./append-method-adox-keys.md)   
 [Método Append (tabelas ADOX)](./append-method-adox-tables.md)   
 [Método Append (usuários do ADOX)](./append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](./append-method-adox-views.md)