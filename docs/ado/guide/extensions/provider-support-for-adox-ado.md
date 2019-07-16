---
title: Suporte do provedor para ADOX (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADOX provider support [ADO]
ms.assetid: 64234ce5-dc46-4c8a-a316-61956b6b9abb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b07f4563d54254310c08c8c132d0729b8ccdc6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923212"
---
# <a name="provider-support-for-adox-ado"></a>Suporte do provedor para ADOX (ADO)
Determinados recursos do ADOX não têm suportados, dependendo do seu provedor de dados OLE DB. ADOX é totalmente compatível com o [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md). Recursos sem suporte com o [Microsoft OLE DB Provider para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), o [Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md), ou o [Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) são listadas nas tabelas a seguir. Não há suporte para ADOX por outros provedores de OLE DB do Microsoft.  
  
## <a name="microsoft-ole-db-provider-for-sql-server"></a>Provedor Microsoft OLE DB para SQL Server  
  
|Objeto ou coleção|Restrição de uso|  
|--------------------------|-----------------------|  
|**Tabelas** coleção|Propriedades são leitura/gravação antes da criação do objeto e somente leitura ao fazer referência a um objeto existente.|  
|**Modos de exibição** coleção|**Modos de exibição** não tem suporte.|  
|**Procedimentos** coleção|O **Append** e **excluir** métodos não têm suporte.|  
|**Procedimento** objeto|O **comando** não há suporte para a propriedade.|  
|**Chaves** coleção|O **Append** e **excluir** métodos não têm suporte.|  
|**Os usuários** coleção|**Os usuários** não tem suporte.|  
|**Grupos de** coleção|**Grupos de** não tem suporte.|  
  
## <a name="microsoft-ole-db-provider-for-odbc"></a>Microsoft OLE DB Provider para ODBC  
  
|Objeto ou coleção|Restrição de uso|  
|--------------------------|-----------------------|  
|**Catálogo** objeto|O **criar** não há suporte para o método.|  
|**Tabelas** coleção|O **Append** e **excluir** métodos não têm suporte. Propriedades são leitura/gravação antes da criação do objeto e somente leitura ao fazer referência a um objeto existente.|  
|**Procedimentos** coleção|O **Append** e **excluir** métodos não têm suporte.|  
|**Procedimento** objeto|O **comando** não há suporte para a propriedade.|  
|**Índices** coleção|O **Append** e **excluir** métodos não têm suporte.|  
|**Chaves** coleção|O **Append** e **excluir** métodos não têm suporte.|  
|**Os usuários** coleção|**Os usuários** não tem suporte.|  
|**Grupos de** coleção|**Grupos de** não tem suporte.|  
  
## <a name="microsoft-ole-db-provider-for-oracle"></a>Microsoft OLE DB Provider for Oracle  
  
|Objeto ou coleção|Restrição de uso|  
|--------------------------|-----------------------|  
|**Catálogo** objeto|O **criar** não há suporte para o método.|  
|**Tabelas** coleção|O **Append** e **excluir** métodos não têm suporte. Propriedades são leitura/gravação antes da criação do objeto e somente leitura ao fazer referência a um objeto existente.|  
|**Modos de exibição** coleção|O **Append** e **excluir** métodos não têm suporte.|  
|**Modo de exibição** objeto|O **comando** não há suporte para a propriedade.|  
|**Procedimentos** objeto|O **Append** e **excluir** métodos não têm suporte.|  
|**Procedimento** objeto|O **comando** não há suporte para a propriedade.|  
|**Índices** coleção|O **Append** e **excluir** métodos não têm suporte.|  
|**Chaves** coleção|O **Append** e **excluir** métodos não têm suporte.|  
|**Os usuários** coleção|**Os usuários** não tem suporte.|  
|**Grupos de** coleção|**Grupos de** não tem suporte.|
